# Remote-Settings-Client

A Remote-Settings Client built using Rust to read collection data.

- Read-Only
- Customizable Signature Verification
<!-- - Cross-Platform
- Robust -->
- Rust!

## Example

Below example uses [Viaduct](https://github.com/mozilla/application-services/tree/master/components/viaduct) and [Viaduct-Reqwest](https://github.com/mozilla/application-services/tree/master/components/support/viaduct-reqwest), so your `Cargo.toml` could look like this:

```toml
[dependencies]
log = "0.4.0"
env_logger = "0.7.1"
viaduct = { git = "https://github.com/mozilla/application-services", rev = "61dcc364ac0d6d0816ab88a494bbf20d824b009b"}
viaduct-reqwest = { git = "https://github.com/mozilla/application-services", rev = "61dcc364ac0d6d0816ab88a494bbf20d824b009b"}
```

### Fetching Records from Collection
```rust,no_run
use remote_settings::{Client};
pub use viaduct::{set_backend};
ures to allow for optional signature implementations for user
pub use viaduct_reqwest::ReqwestBackend;

fn main() {
  
  set_backend(&ReqwestBackend).unwrap();

  // we pass None for Verifier parameter to fall back to default verifier implementation
  // here server_url and bucket_name will be set to default values
  let client = Client::builder().collection_name("example-collection").build();
  
  match client.get() {
        Ok(records) => println!("{:?}", records),
        Err(error) => println!("Error fetching/verifying records": {:?}", error)
  };
  ...
}
```

### Logging

Dependencies: [log](https://docs.rs/log), [env_logger](https://docs.rs/env_logger)

```toml
[dependencies]
env_logger = "0.7.1"
```

For logging, run `RUSTLOG={debug/info} cargo run` to see debug/info log messages from the Remote-Settings-Client (error messages are printed by default)

```rust,no_run
fn main() {
  env_logger::init() // initialize logger
}
```

For more examples, go to the [demo project](rs-client-demo)

## License

Licensed under Mozilla Public License, Version 2.0 (https://www.mozilla.org/en-US/MPL/2.0/)
