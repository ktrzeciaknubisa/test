### Updating JXcore binaries

Below are the steps to be taken if you want to update JXcore binaries in your Cordova JXcore application.
They all should be called prior to `cordova plugin add` command.

1. Rebuild JXcore binaries: [Compile as a Static Library](https://github.com/jxcore/jxcore/blob/master/doc/Android_Compile.md#compile-as-a-static-library)
2. Refresh `jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries` folder contents:

    ```bash
    $ cd /my/cordova/app
    $ rm -f ./jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries/*
    $ cp -f /jxcore/repo/out_android/android/bin/* jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries/
    ```

3. Recompile .so files

    ```bash
    $ cd jxcore-cordova/io.jxcore.node/src/android/jni
    $ ~/android-ndk-path/ndk-build
    ```

4. Add/re-add the plugin/platform

    ```bash
    $ cd ../../../../../
    $ cordova plugin add jxcore-cordova/io.jxcore.node/
    $ cordova platforms add android
    ```

5. You may run the app now

    ```bash
    $ cordova run
    ```

