# Cross-Compiling Anvil for MacOS

## Setup a Cross-Compilation Environment

Compiling Anvil for MacOS from Linux requires a C cross-compiler and the MacOS SDK. One way to get this is using [osxcross](https://github.com/tpoechtrager/osxcross). This has been tested with osxcross as of commit be6ffb3cbc6c0228614ebe6a4b5cd2726339ecc9, and Apple XCode 15.4 on Debian 11.2+ for Anvil.

The steps needed to setup the cross compiler are those described in the
osxcross README, and in this case:

  * Download Xcode 15.4 from the Apple developer site as noted in the osxcross readme
  * Clone osxcross to the same directory as the previous step, then cd into the osxcross directory
  * Install the dependencies listed in the osxcross readme
  * Run `./tools/gen_sdk_package_pbzx.sh ../Xcode_15.4.xip`. This should produce a file `MacOSX14.sdk.tar.xz` and a file `MacOSX14.5.sdk.tar.xz` in the current directory (the root of the osxcross git workspace)
  * Copy the SDK package `MacOSX14.5.sdk.tar.xz` to the subdirectory tarballs/
  * Run `./build.sh`

Once that is completed, GIO programs can be compiled by setting environment variables and then using `go build`. The correct environment variables to set depend on the target architecture:

  * PATH: update PATH to include the target/bin subdirectory of the osx-
    cross repo so that the compilers are in the PATH
  * GOOS: set to `darwin`
  * GOARCH: one of `amd64` or `arm64`
  * CC: For `amd64` use `x86_64-apple-darwin23.5-cc`, and for `arm64`
    use `arm64-apple-darwin23.5-cc`
  * CXX: For `amd64` use `x86_64-apple-darwin23.5-c++`, and for `arm64`
    use `arm64-apple-darwin23.5-c++`
  * CGO_ENABLED: Set to 1 so that CGO is allowed for cross-compiling
  * CGO_CFLAGS: Set to:
    -D_Nullable_result= -DNS_FORMAT_ARGUMENT(A)= -DTARGET_OS_OSX

The CGO_CFLAGS setting is required to avoid compilation errors. The defines '-D_Nullable_result=' and '-DNS_FORMAT_ARGUMENT(A)=' disable function attributes that cause compilation errors in the Mac SDK. The first attribute seems to only be applicable to Swift, and the second is meant to catch errors related to printf-style format strings at compile time, but is itself not handled properly in the compiler. Both are meant to catch internal SDK compile-time errors which I assume would have already been caught before the SDK was released, so are safe to disable.

The '-DTARGET_OS_OSX' defines the target OS to be OSX. Some important SDK headers are not included unless the target os is defined thus causing compile errors, so we define it.

## Compile Anvil

To specifically build Anvil, set the cross compiler environment variables and then compile Anvil by changing to the `editor/cmd/anvil` subdirectory in the Anvil repository and running `go build`. Optionally build the extra tools by changing to each subdirectory under `extras/cmd/` and running `go build`.

## Sign Binaries

MacOS refuses to run unsigned binaries by default. However, you can sign binaries without a proper code signing certificate and this usually satisfies MacOS. One way to do this is on Linux is to download and install the Rust version of [rcodesign](https://crates.io/crates/apple-codesign/0.29.0) created by [Gregory Szorc](https://gregoryszorc.com/blog/2022/08/08/achieving-a-completely-open-source-implementation-of-apple-code-signing-and-notarization/). 

Once installed it is as simple as running rcodesign on the binary, like so:

	rcodesign sign anvil


