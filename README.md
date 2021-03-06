This crate allows one to generate logs about how tasks are scheduled, in order to generate a
profile of the CPU usage of the binary.

This crate leverages https://github.com/catapult-project/catapult/tree/11513e359cd60e369bbbd1f4f2ef648c1bccabd0/tracing

# Usage

First, import the traits:

```rust
use futures_diagnose_exec::{FutureExt as _, Future01Ext as _};
```

Then whenever you create a `Future`, append `.with_diagnostics("name")`. For example:

```rust
async_std::spawn(future.with_diagnostics("my-task-name"))
```

Then, run your code. A `profile.json` file will be generated in the current working directory.
(TODO: it is highly likely that in the future one will control that through an environment
variable, so if you don't find the file it's likely that we forgot to update this README)

Then, open Chrome and go to the URL `chrome://tracing`, and load the `profile.json`.
