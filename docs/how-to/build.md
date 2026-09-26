# Building Anvil from Source

## Requirements

Anvil requires a recent version of [Go](https://go.dev/dl/) installed. The build will download any required Go modules automatically from the internet, but the GIO UI library has some external dependencies if you are building on Linux. See the [GIO install page](https://gioui.org/doc/install) for the list.

## Standard Build Instructions

The usual build method should be run on Linux. The source code archive contains two subdirectories to be built: anvil, which contains the editor source code, and anvil-extras, which contains optional helper programs. 

Change to each of these directories and then run:

	./build.sh
	
This will build anvil and helper programs for the current OS and architecture. To build for another architecture, use the -a and -o options. For example, the following command builds for windows 64-bit:

    ./build.sh -a amd64 -o windows
    
Using `./build -h` provides help about the available options. The final binaries/executables are found in the anvil or anvil-extras directories.

## Alternate Build Instructions

If you are building on Windows or don't want to use build-all.sh for some reason, you can instead cd to specific subdirectories and build the binary using `go build`. You can do that in the following directories:

  * anvil/src/anvil: To build Anvil
  * anvil-extras/cmd/mdtoc: To build mdtoc
  * anvil-extras/cmd/autodump: To build aad
  * anvil-extras/cmd/Rt: To build the Rt 
  * anvil-extras/cmd/awin: To build awin
  * anvil-extras/cmd/wrap: To build wrap

