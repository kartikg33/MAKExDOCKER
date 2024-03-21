# MAKExDOCKER
Run make commands to easily launch docker environments for any task, e.g. compilation, installation, hosting, etc...

## How it works
Run `make` from the root directory to build the example Golang project for your local machine (host). 
You will need to have both `make` and `docker` installed for this.
You do NOT need to install any toolchains on your local machine. Instead, install any required toolchains/libraries in your docker environment (see the example given).

## Cross-compiling
By default, `make` will compile for your host machine.
To cross-compile, specify the target platform as follows: `make TARGET=<target>`
Run `make help` to get a full list of supported targets.