### Updating JXcore binaries

Below are the steps to be taken if you want to update JXcore binaries to Cordova JXcore application. 
They all should be called prior to `cordova plugin add jxcore-cordova/io.jxcore.node/` command.

1. [Compile as a Static Library](https://github.com/jxcore/jxcore/blob/master/doc/Android_Compile.md#compile-as-a-static-library)
2. refresh `jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries` folder:

```bash
$ cd /my/cordova/app
$ rm -f ./jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries/*
$ cp -f /jxcore/repo/out_android/android/bin/* jxcore-cordova/io.jxcore.node/src/android/jxcore-binaries/

```

3. recompile .so files

```bash
$ cd jxcore-cordova/io.jxcore.node/src/android/jni
$ ~/android-ndk-path/ndk-build
$ cd ../../../../../
```
4. add/re-add the plugin 

```bash
cd jxcore-cordova/io.jxcore.node/src/android/jni
~/android-ndk-r10d/ndk-build
cd ../../../../../
```
