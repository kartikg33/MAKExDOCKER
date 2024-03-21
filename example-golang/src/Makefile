# set build directory if not already set
BUILDDIR?=build

.PHONY: build test run depends

default: build

# go build
# -- stores output binary in directory bin/
build:
	$(info Compiling for target $(TARGET) as $(GOARCH)/$(GOOS))
	mkdir -p $(BUILDDIR)
	go build -v -o $(BUILDDIR)/

# go test
test:
	go test

# go mod tidy
depends:
	go mod tidy

# don't allow 'go run .' as this will block up the terminal. instead build the binary and run it in a docker env for testing.