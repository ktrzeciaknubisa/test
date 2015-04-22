#### -extract

Boolean value. Default is `false`.

- if not provided, uses the default value.
- if provided, but not followed by any value, it acts as `true`:

    ```bash
    > jx package helloworld.js -extract
    ```

- if provided, and followed by `0` or `no` or `false`, it acts as `false````:

    ```bash
    > jx package helloworld.js -extract 0
    ```

- if provided, and followed by anything else than `0` or `no` or `false`, it acts as `true`:

    ```bash
    > jx package helloworld.js -extract 1
    ```

#### -library

Boolean value. Default is `true`. See also notes above.

#### -fs_reach_sources

Boolean value. Default is `true`. See also notes above.

#### -preInstall or -preinstall

This parameter receives commands separated with commas.

For example, the following command line:

    > jx package helloworld.js -preinstall "mkdir dir1,touch dir1/file.txt"

will get converted to the following array and embedded into JXP project file:

```js
    ...
	"preInstall": [
		"mkdir dir1",
		"touch dir1/file.txt"
	],
	...
```
