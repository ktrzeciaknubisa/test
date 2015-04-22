#### -extract

Boolean value. Default is `false`.

- if not provided, uses the default value.
- if provided, but not followed by any value, it acts as `true`:

    >> jx package helloworld.js -extract

- if provided, and followed by `0` or `no` or `false`, it acts as `false````:

    ```> jx package helloworld.js -extract 0```

- if provided, and followed by anything else than `0` or `no` or `false`, it acts as `true`:
    ```bash
    > jx package helloworld.js -extract 1
    ```
