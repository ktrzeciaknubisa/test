# Packaging & Code Protection

JXcore introduces a unique feature for packaging of source files and other assets into JX packages.

Let’s assume you have a large project consisting of many files. This feature packs them all into a single file to simplify the distribution. It also protects your server side JavaScript code by keeping all source files inside a package, which makes them more difficult to reach.

JX packages can be easily executed with JXcore, just like regular JavaScript applications:

    > jx helloworld.jx

instead of:

    > jx helloworld.js

## Command

### package

    > jx package javascript_file [name_of_the_package] [options]

You may specify none, one or more of the following options:

* -add [file||folder, file||folder2, ...]
* -slim file||folder, file||folder2, ...
* JXP fields may be also provided here. See below for their description.

The `jx package` command recursively scans the current folder and generates a `JXP` package information file based on all files in that directory.
After that, it compiles the `JXP` file (by invoking `compile` command).

* `javascript_file` - the main file, which will be executed when JX package is launched with JXcore.
* `name_of_the_package` - indicates the name of the package file. For example, giving the value *MyPackage*  will create *mypackage.jx* file.
This value is optional. When not provided, the package name will be evaluated from `javascript_file` parameter (file name without an extension).

Suppose you have a simple *Hello_World* project, with just two files: *helloworld.js* and *index.html*. When you call:

    > jx package helloworld.js "Hello World"

initially, the tool generates `JXP` project file (*helloworld.jxp*). Then it is used as an input for `compile` command,
which will create the output JX package *helloworld.jx*.

Description of the switches:

#### -add

This optional parameter followed by file and/or folder names separated with commas - **explicitly adds** those files/folders into the final JX package.
For example, you may want to package only certain files/folders located at current directory - not the whole its contents.

If you want to pack just one file (e.g. *helloworld.js*) you can provide an `-add` option without a file name.
Thus the following two commands are equivalent:

     > jx package helloworld.js "Hello World" -add

     > jx package helloworld.js "Hello World" -add helloworld.js

Yu can still combine `-add` and `-slim` together, e.g. to add a folder, but exclude its sub-directory, like:

     > jx package helloworld.js "Hello World" -add node_modules -slim node_modules/express

#### -slim

This optional parameter followed by file and/or folder names separated with commas - **prevents adding** those files/folders into the final JX package.

##### wildcards

For both `-add` and `-slim` you can also use wildcards (`*` and `?`) for each file/folder entry.
However if you do so, you'd better wrap them in double quotes, like below:

    > jx package helloworld.js "Hello World" -add "file*.txt"

Otherwise the wildcard expression would be evaluated by shell (before invoking the command) and `-add` option
would receive only first of the matched entries.

Comma separated entries are also valid:

    > jx package helloworld.js "Hello World" -add "file*.txt,*.jpg" -slim "node?modules,dir*"

##### absolute and relative paths

Each single entries provided to `-add` or `-slim` may represent either an absolute path or path relative to current working directory.
Below example defines for the `-slim` option the same path in 3 ways (2 relative and 3rd absolute), which is of course redundant, however illustrates the subject:

     > jx package helloworld.js "Hello World" -slim out,./out,/users/me/folder/out

#### -native

This parameter is optional. When provided, the package will be compiled as a self-executable.
It means, that you can run it directly without `jx` binary.

Also, the output file name will be changed. It will no longer contain *.jx* extension.
In fact, for Unix systems it will not contain any extension at all, while on Windows - it will be an *.exe*.

Thus, you can run it on Unix systems the following way:

    > ./helloworld

On Windows:

    > helloworld.exe

#### -name

String value.

#### -version

String value.

#### -author

String value.

#### -description

String value.

#### -company

String value.

#### -website

String value.

#### -extract

Boolean value. Default is `false`.

- if not provided, uses the default value.
- if provided, but not followed by any value, it acts as `true`:

```bash
> jx package helloworld.js -extract
```

- if provided, and followed by `0` or `no` or `false`, it acts as `false`:

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

### compile

When you already have a `JXP` project file (either created with `package` command or manually), you can call `compile` for generating a JX package.

    > jx compile project_file.jxp -native

When `-native` switch is provided, it overrides `native` parameter value from a `JXP` file.

## Hiding body of functions

As of JXcore v Beta-0.3.0.0 (open source version) this feature is no longer available.

## JX package

### About JX package file

The JX package file is what you get as a result of compilation and packaging your project.
It’s a binary file used only by `jx` executable.
Contains all of the script files of your project, as well as assets, which can be considered as static resources.

### Compiling

See `compile` command.

### Launching

JX packages can be executed as follows:

    > jx my_project.jx

Obviously, you need to have JXcore installed first. For this, please visit [Downloads](http://jxcore.com/downloads/) page.

You can also run the package in multiple instances.

    > jx mt my_project.jx

or

    > jx mt-keep my_project.jx

## JXP project file

The JXP file is a JX package description. It contains information about the package.
This is also the input file for the compilation of JX file.
It means, if you want to package your project into a JX package, you need to create JXP project file first.

You can do it either manually or by using `package` command.

### Excluding folders

See `package` command with `-slim` switch.

### File structure

The JXP project file is a simple text file that contains package description written as json literal object:

```js
{
    "name": "Hello World",
    "version": "1.0",
    "author": "",
    "description": "",
    "company": "",
    "website" : "",
    "package": null,
    "startup": "helloworld.js",
    "execute": null,
    "extract": false,
    "output": "helloworld.jx",
    "files": [
        "helloworld.js"
    ],
    "assets": [
        "index.html"
    ],
    "library": false,
    "license_file": null,
    "readme_file": null,
    "preInstall" : [
        "mkdir new_folder"
    ],
    "fs_reach_sources": true,
    "native" : true
}
```

You can access this object in a runtime of your JX package by:

```js
var obj = exports.$JXP;
```

And the single field:

```js
var name = obj.name;
```

Below you can find explanation for all supported fields:

* **name**, **version**, **author**, **description**, **company**, **website**
These are all string values.
* **startup**
Name of the main project file. If execute parameter is not defined, this file will be executed first when you run the package.
* **execute**
Name of the main execution file. If this parameter is omitted or null – the value from startup will be used.
This parameter has different meaning depending on the library value.
When the package is compiled with `library` = `false`, and you run the compiled package, this execute file will be executed first.
If `library` is `true`, and the package is called with `require()` method, the execute file will be returned by the latter.
* **extract**
This is a boolean value: true or false. When it's set to true, all package contents will be extracted at first run of the compiled package. There will be a new folder created with the name parameter. All files and assets embedded inside the package will be saved with full directory structure preserved.
* **output**
Name of the output JX package.
* **files**
This is an array, where you can define, which script files from your project will be included into the JX package. Only `*.js` and `*.json` files are allowed here.
* **assets**
This is the array with static resource files. You can embed any asset file into the `jx` package.
* **library**
It is a boolean value: true or false. Value set to true means that JX package can be treated as a library and it can be used from inside another JX package (with `require()` method).
Setting this value to false is a good way of preventing its usage as an external module (and then `require()` will not be possible).
* **licence_file**
Name of the file containing the licensing information – it is generally a simple text file. If this parameter is omitted or null and if a file named “LICENSE” exists in the directory from where you compile the package – it will be embedded automatically.
* **readme_file**
Name of the file containing additional notes about the package. If this parameter is omitted or null and if a file named “README” or “README.md” exists in the directory from where you compile the package – it will be embedded automatically.
When a license or readme file is specified, it can be also displayed in a console window directly from the package.

For example, running the following command:

    > jx package.jx license

will display the licence file to the console without executing the package. The same applies to:

    > jx package.jx readme

* **preInstall**
This is an array, where you can define system commands to be executed right before jx package execution.
For example, this might be creating a folder, installing an additional package/module or just anything.
Commands are executed in the same order as the array is defined.

There is a special keyword `JX_BINARY` which is replaced during runtime with current `jx` executable path.

For example, we have the following commands in JXP file:

```js
"preInstall" : [
    "which JX_BINARY > log.txt",
    "JX_BINARY -jxv >> log.txt"
]
```

Those commands will be executed for the first time, when we run the package:

    > jx package.jx

or

```js
var module = require("./package.jx");
```

In this example, the first commands writes the full path string of jx binary to the *log.txt* file, while the second one - executes `jx -jxv`
and appends the result (the jx version number) to the same file.

When all of the commands are executed, there will be a file created `your_module.installed` preventing subsequent execution of pre-install section.
If you want to run it again, simply remove that file.

* **custom_fields**

You can also define your own constants, as many as you want, for example:

```js
{
    // ...
    // ...
    // ...
    field1 : "one",
    myField2 : "two",
    someObject : {
        PI : 3.14159265359,
        userArray : [ 1, 2 ]
    },
    Release : true
}
```

Similarly, accessing those values in a runtime of your JX package is also easy:

```js
var pi = exports.$JXP.someObject.PI;
```

One of the usage examples for those custom fields can be:

```js
if (exports.$JXP.Release) {
    console.log("This is the final release of the product.");
} else {
    console.log("This code is still under development.");
}
```

However, `files` members are not accessible from exports.$JXP.

* **fs_reach_sources**
Normally, `fs` can not reach the JavaScript files inside the package. If you need to access all the JavaScript files using `fs` module, you should set this parameter to 'true'. Otherwise you can either set it to 'false' or give the list of files expected to be reachable by 'fs' module. (i.e. { "lib/testfile.js":true, "lib/test2.js":true } )

* **native**
When this parameter is set to 'true', the compilation process creates standalone, self-executable binary rather than a package.
It acts exactly as `jx package` command called with [`-native`](jxcore-feature-packaging-code-protection.html#jxcore_feature_packaging_code_protection_native) switch.

### Supported file types

You can embed any asset file (text and binary) into the `jx` package and it will be
placed automatically into the `assets` array of `JXP` project file during execution of `jx package` command.

However, there are two file types, which are treated by JXcore as source files rather than assets:

* js
* json

The difference is, that source files cannot be read from a package during runtime.
This is a security feature of JXcore packaging.
For more information see [Accessing Files and Assets from a Package](#jxcore_feature_packaging_code_protection_files).

The `jx package` puts them into the `files` array of `JXP` project file during execution of `jx package` command.

Even if you would edit the `JXP` project file manually and add `js` files into the `assets` array, JXcore removes them from the `assets` and treats them as source files.

## Accessing Files and Assets from a Package

### assets

There are a few native methods in the [FileSystem](fs.markdown) module that you can use to access assets embedded inside a JX package.

* `readFile()`
* `readFileSync()`
* `readdir()`
* `readdirSync()`

When called, each of these methods tries to find a given file or a folder in the real file system in the first place.
If nothing is found, JXcore searches through assets from the JX package.

Assets can always be referenced relatively to `__dirname` or `./`.

Let's consider a JX package containing the following directory structure:

- folder
  - file2.html
  - module.js
- index.html
- package.json
- test.js

After creating a package with the command:

    > jx package test.js my_package

we can access the assets of the package from inside the *test.js* file, and this would be like this:

```js
var fs = require('fs');

// gets index.html file from package's assets, if it does not exists on the disk.
var index = fs.readFileSync(__dirname + '/index.html');

// asset from subfolder:
var file = fs.readFileSync(__dirname + '/folder/file2.html');
```

The following sample works as expected, returns the directory contents of the file system. `readdir()` and `readdirSync()`
return from the JX package only when the given path does not exist on real file system. Calling one of these methods for the main
folder of the JX package will return the results from actual file system. In order to reach asset files using one of these
methods, you should consider putting them in a sub folder.

```js
var fs = require('fs');
var index1 = fs.readdirSync('./folder');
```

### files

`readFile()` and `readFileSync()` methods can be used to reach any files inside a JX package except for the source files.
JavaScript files inside a JX package can be accessed only by using `require()` method. In other words,
you can not read the source files using `readFile()` or `readFileSync()`.

Example below shows how to load *module.js* file contained inside *folder* directory of JX package:

```js
var lib = require("./folder/module.js");
console.log("lib.value", lib.value);
```


