# Escrow-Contract

```rust
public entry fun create_vesting<CoinType>(
        account: &signer,
        receiver: address,
        release_amounts:vector<u64>,
        release_times:vector<u64>,
        total_amount:u64,
        seeds: vector<u8>
    )acquires VestingCap {
```

It defines a public function called **`create_vesting`**, which anyone can call and accepts the following parameters.

- **`account`**: It refers to a signer account that will be used to create the vesting schedule and transfer the funds.
- **`receiver`**: This refers to the address of the account that will receive the released funds from the vesting schedule.
- **`release_amounts`**: A vector of 64-bit integers that represents the amounts that will be released at each vesting time.
- **`release_times`**: A vector of 64-bit integers that represents the times at which each release will occur.
- **`total_amount`**: An 64-bit integer that represents the total amount of funds that will be released over the vesting period.
- **`seeds`**: A vector of bytes that will be used to create a unique identifier.

```rust
				let account_addr = signer::address_of(account);
        let (vesting, vesting_cap) = account::create_resource_account(account, seeds); //resource account
        let vesting_address = signer::address_of(&vesting);
        if (!exists<VestingCap>(account_addr)) {
            move_to(account, VestingCap { vestingMap: simple_map::create() })
        };
        let maps = borrow_global_mut<VestingCap>(account_addr);
        simple_map::add(&mut maps.vestingMap, seeds,vesting_address);
```

First, we use `signer::address_of(account)` to get ****the sender's account address. A new resource account is then created using the `account::create_resource_account(account, seed)` function. This function returns a tuple containing the newly created resource account (`vesting`) and associated capabilities (`vesting_cap`).

The address of the newly created resource account is retrieved using `signer::address_of(&vesting)`. If there is currently no vesting account for `account_addr`, `VestingCap { vestingMap: simple_map::create() } and move_to(account, ...)`.

Finally, add the address of the newly created vesting account to the vesting map with `simple_map::add(&mut maps.vestingMap, seed, vesting_address).`

```rust
				let vesting_signer_from_cap = account::create_signer_with_capability(&vesting_cap);
        let length_of_schedule =  vector::length(&release_amounts);
        let length_of_times = vector::length(&release_times);
        assert!(length_of_schedule==length_of_times,ENO_INSUFFICIENT_FUND);
        let i=0;
        let total_amount_required=0;
        while ( i < length_of_schedule )
        {
            let tmp = *vector::borrow(&release_amounts,i);
            total_amount_required=total_amount_required+tmp;
            i=i+1;
        };
        assert!(total_amount_required==total_amount,ENO_INSUFFICIENT_FUND);
```

A signer with permission to modify a newly created resource account is created using the `account::create_signer_with_capability()` function. A resource account is represented by the `vesting_cap` variable.

The length of the `release_amounts` and `release_times` vectors is determined using the `vector::length()` function.

An assert was made to check that the length of `release_amounts` is equal to the length of `release_times.` If they are not equal, the error code `ENO_INSUFFICIENT_FUND` is raised.
The two variables `I` and `total_amount_required` are initialized to `0`.

A while loop is used to iterate through the elements of the `release_amounts` vector. At each iteration, the value of the current index is borrowed using the `vector::borrow()` function and added to the `total_amount_required` variable.

After the loop, an assertion is made to see if `total_amount_required` equals the `total_amount` parameter. If they are not equal, the error code `ENO_INSUFFICIENT_FUND` is raised.
Typically, this block of code is used to check that the `release_amounts` and `total_amount` inputs match each other. Otherwise, an error is raised, and the function exits without changing any data.

```rust
let released_amount=0;
        let coin_address = coin_address<CoinType>();
        move_to(&vesting_signer_from_cap, VestingSchedule{
        sender:account_addr,
        receiver,
        coin_type:coin_address, 
        release_times,
        release_amounts,
        total_amount,
        resource_cap:vesting_cap,
        released_amount,
        });
        let escrow_addr = signer::address_of(&vesting);
        managed_coin::register<CoinType>(&vesting_signer_from_cap); 
        coin::transfer<CoinType>(account, escrow_addr, total_amount);
    }
```

This block of code creates a new `VestingSchedule` resource account and transfers funds from the calling account to this account. Here is the code analysis.

- let `Released_Amount=0;` Initialize the `Release_Amount` variable to `0`.
- let `coin_address = coin_address();` Gets the `CoinType` address specified in the type parameter.
- `move_to(&vesting_signer_from_cap, vesting schedule{...});` Moves the newly created `VestingSchedule` resource account under the control and management of the signer. This line initializes the `VestingSchedule` resource account with the following fields:
- `From:` The address of the account that initiated the VestingSchedule creation.
- `Recipient:` The address of the recipient of investment funds.
- `coin_type`: Coin type used for vesting schedule.
- `release_times`: A vector of times, in seconds, that an investment can be released.
- `release_amounts`: Vector of amounts to be released at each release moment.
- `total_amount`: Total amount to be transferred.
- `resource_cap:` Ability to manage VestingSchedule resource accounts.
- `Release_Amount`: Amount already released.
- let `escrow_addr = signer::address_of(&vesting);`Gets the account address of the VestingSchedule resource.
- `manage_coin::register(&vesting_signer_from_cap);` Register the `CoinType` with the capability of the signer with the capability to manage the `VestingSchedule` resource account. This ensures that the `CoinType` can be used by the `VestingSchedule.`
- `coin::transfer(account, escrow_addr, total_amount);` Transfers the total amount of funds from the calling account to the `VestingSchedule` resource account. This ensures the availability of investment funds.
