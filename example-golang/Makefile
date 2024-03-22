# set current directory
CURR_DIR:=$(shell pwd)

SUPPORTED_TARGETS := host rpi3
### CONTRIBUTE: add additional supported platforms to this list, e.g. beaglebone, rpi4, bananapi, etc...

####### DO NOT USE TAB INDENTS HERE AS MAKEFILE MISTAKES TAB INDENTS FOR BUILD COMMANDS #######

# check if target is in list of supported targets, else issue error
ifndef $(TARGET)
# Set target to host if not already specified
TARGET = host
else ifeq ($(filter $(TARGET),$(SUPPORTED_TARGETS)),)
$(error '$(TARGET)' does not exist in list '$(SUPPORTED_TARGETS)')
endif

### setup GO ENV variables for the defined target

ifeq ($(TARGET),host)
# get host BUILDARCH details from shell
BUILDARCH = $(shell uname -m)
BUILDOS = $(shell echo $(shell uname -o) | tr A-Z a-z)
endif

ifeq ($(TARGET),rpi3)
# hardcoded config for raspberry pi 3
BUILDARCH = arm64
BUILDOS = linux
endif

### CONTRIBUTE: add additional supported platforms here

# Exit if BUILDARCH and BUILDOS not set
ifndef BUILDARCH
$(error BUILDARCH env variable not set!)
endif
ifndef BUILDOS
$(error BUILDOS env variable not set!)
endif

###############################################################################
# Make targets
###############################################################################

.PHONY: build depends test run ipk help

default: help

# help
help:
	$(info Usage:)
	$(info   make build [TARGET=<target>], where <target> is one of: $(SUPPORTED_TARGETS))
	$(info   make depends)
	$(info   make test)
	$(info   make run)

# builds binary
build:
	$(info Building binary for target $(TARGET) using $(BUILDARCH)/$(BUILDOS))
	docker run --rm -e GOARCH=$(BUILDARCH) -e GOOS=$(BUILDOS) -e BUILDDIR=build -v "$(CURR_DIR)/src":/usr/src/app -w /usr/src/app golang:1.20 make build

# tidies go modules file
depends:
	$(info Tidying go module dependencies)
	docker run --rm -v "$(CURR_DIR)/src":/usr/src/app -w /usr/src/app golang:1.20 make depends

# runs go test cases
test:
	$(info Running tests)
	docker run --rm -v "$(CURR_DIR)/src":/usr/src/app -w /usr/src/app golang:1.20 make test

# TODO: runs binary in a docker env
run: build
	$(info Running app on target $(TARGET) using $(BUILDOS)/$(BUILDARCH))
	$(error Running env not yet supported!)