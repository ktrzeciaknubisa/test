
# Description

The `install_and_run.sh` script automates the following tasks:

1. creating cordova project
2. downloading JXcore-cordova plugin
3. adding it to the project
4. optionally with applying chosen sample application from `sample` folder

The script assumes, that cordova is already installed as well as android sdk and iOS tools.

# Usage

### Download the scipt

Download `install_and_run.sh` and save into an empty folder.

### Run the script with original sample

```bash
$ ./install_and_run.sh
```

### Run the script with other sample

If you want to launch any of the prepared samples, you may add it's folder name like this:

```bash
$ ./install_and_run.sh "express sample"
```

or

```bash
$ ./install_and_run.sh "express performance sample"
```
