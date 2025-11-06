<p align="center">
  <img src="https://raw.githubusercontent.com/domajor/noxcoin-project/main/logo.png" alt="NoxCoin Logo" width="180"/>
</p>

# NoxCoin NXC Project  v0.5.1.3

## NoxCoin – Private. Secure. Untraceable.

### ?? Note from the Maintainer
Hello!  
This is a community revival of **NoxCoin** — all previous threats have been deleted and purged.  
Please verify everything independently and use only trusted sources.  

My goal is simple: to help this coin survive and grow into a secure, community-driven project.  
I'm not an official developer — this project is open to everyone who wishes to help.  

> “The birth of a baby is very difficult, but what's even more difficult is keeping it alive and ensuring it grows into a valuable person.”

---

##  Project Links 
- **Website:** [https://noxcoin.online](https://noxcoin.online)  
- **Explorer:** [https://explorer.noxcoin.online](https://explorer.noxcoin.online)  
- **Mining Stats:** [https://miningpoolstats.stream/noxcoin](https://miningpoolstats.stream/noxcoin)  
- **Discord:** [https://discord.gg/fgu34rYtrV](https://discord.gg/fgu34rYtrV)  
- **Telegram:** [https://t.me/+O0mMgUg1qXM4OWI8](https://t.me/+O0mMgUg1qXM4OWI8)

---

##  Acknowledgments
Special thanks to **@aalnase** ([go-poolmining.com](https://go-poolmining.com)) for his technical help and support in rebuilding and maintaining the NoxCoin network.

---

##  About NoxCoin
**NoxCoin** is a fork of **Monero**, the most battle-tested privacy cryptocurrency — rebuilt with a community-first vision.  
It retains Monero’s strong cryptographic foundation while introducing new emission rules, scaling adjustments, and decentralization incentives.

---

## License

See [LICENSE](LICENSE).

## Contributing

If you want to help out, see [CONTRIBUTING](docs/CONTRIBUTING.md) for a set of guidelines.

## Compiling NoxCoin from source

### Dependencies

The following table summarizes the tools and libraries required to build. A
few of the libraries are also included in this repository (marked as
"Vendored"). By default, the build uses the library installed on the system
and ignores the vendored sources. However, if no library is found installed on
the system, then the vendored source will be built and used. The vendored
sources are also used for statically-linked builds because distribution
packages often include only shared library binaries (`.so`) but not static
library archives (`.a`).

| Dep         | Min. version  | Vendored | Debian/Ubuntu pkg    | Arch pkg     | Void pkg              | Fedora pkg          | Optional | Purpose         |
| ----------- | ------------- | -------- | -------------------- | ------------ | --------------------- | ------------------- | -------- | --------------- |
| GCC         | 7             | NO       | `build-essential`    | `base-devel` | `base-devel`          | `gcc`               | NO       |                 |
| CMake       | 3.5           | NO       | `cmake`              | `cmake`      | `cmake`               | `cmake`             | NO       |                 |
| pkg-config  | any           | NO       | `pkg-config`         | `base-devel` | `base-devel`          | `pkgconf`           | NO       |                 |
| Boost       | 1.58          | NO       | `libboost-all-dev`   | `boost`      | `boost-devel`         | `boost-devel`       | NO       | C++ libraries   |
| OpenSSL     | basically any | NO       | `libssl-dev`         | `openssl`    | `openssl-devel`       | `openssl-devel`     | NO       | sha256 sum      |
| libzmq      | 4.2.0         | NO       | `libzmq3-dev`        | `zeromq`     | `zeromq-devel`        | `zeromq-devel`      | NO       | ZeroMQ library  |
| OpenPGM     | ?             | NO       | `libpgm-dev`         | `libpgm`     |                       | `openpgm-devel`     | NO       | For ZeroMQ      |
| libnorm[2]  | ?             | NO       | `libnorm-dev`        |              |                       |                     | YES      | For ZeroMQ      |
| libunbound  | 1.4.16        | NO       | `libunbound-dev`     | `unbound`    | `unbound-devel`       | `unbound-devel`     | NO       | DNS resolver    |
| libsodium   | ?             | NO       | `libsodium-dev`      | `libsodium`  | `libsodium-devel`     | `libsodium-devel`   | NO       | cryptography    |
| libunwind   | any           | NO       | `libunwind8-dev`     | `libunwind`  | `libunwind-devel`     | `libunwind-devel`   | YES      | Stack traces    |
| liblzma     | any           | NO       | `liblzma-dev`        | `xz`         | `liblzma-devel`       | `xz-devel`          | YES      | For libunwind   |
| libreadline | 6.3.0         | NO       | `libreadline6-dev`   | `readline`   | `readline-devel`      | `readline-devel`    | YES      | Input editing   |
| expat       | 1.1           | NO       | `libexpat1-dev`      | `expat`      | `expat-devel`         | `expat-devel`       | YES      | XML parsing     |
| GTest       | 1.5           | YES      | `libgtest-dev`[1]    | `gtest`      | `gtest-devel`         | `gtest-devel`       | YES      | Test suite      |
| ccache      | any           | NO       | `ccache`             | `ccache`     | `ccache`              | `ccache`            | YES      | Compil. cache   |
| Doxygen     | any           | NO       | `doxygen`            | `doxygen`    | `doxygen`             | `doxygen`           | YES      | Documentation   |
| Graphviz    | any           | NO       | `graphviz`           | `graphviz`   | `graphviz`            | `graphviz`          | YES      | Documentation   |
| lrelease    | ?             | NO       | `qttools5-dev-tools` | `qt5-tools`  | `qt5-tools`           | `qt5-linguist`      | YES      | Translations    |
| libhidapi   | ?             | NO       | `libhidapi-dev`      | `hidapi`     | `hidapi-devel`        | `hidapi-devel`      | YES      | Hardware wallet |
| libusb      | ?             | NO       | `libusb-1.0-0-dev`   | `libusb`     | `libusb-devel`        | `libusbx-devel`     | YES      | Hardware wallet |
| libprotobuf | ?             | NO       | `libprotobuf-dev`    | `protobuf`   | `protobuf-devel`      | `protobuf-devel`    | YES      | Hardware wallet |
| protoc      | ?             | NO       | `protobuf-compiler`  | `protobuf`   | `protobuf`            | `protobuf-compiler` | YES      | Hardware wallet |
| libudev     | ?             | NO       | `libudev-dev`        | `systemd`    | `eudev-libudev-devel` | `systemd-devel`     | YES      | Hardware wallet |

[1] On Debian/Ubuntu `libgtest-dev` only includes sources and headers. You must
build the library binary manually. This can be done with the following command `sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make`
then:

- on Debian:
  `sudo mv libg* /usr/lib/`
- on Ubuntu:
  `sudo mv lib/libg* /usr/lib/`

[2] libnorm-dev is needed if your zmq library was built with libnorm, and not needed otherwise

Install all dependencies at once on Debian/Ubuntu:

```
sudo apt update && sudo apt install build-essential cmake pkg-config libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libexpat1-dev libpgm-dev qttools5-dev-tools libhidapi-dev libusb-1.0-0-dev libprotobuf-dev protobuf-compiler libudev-dev libboost-chrono-dev libboost-date-time-dev libboost-filesystem-dev libboost-locale-dev libboost-program-options-dev libboost-regex-dev libboost-serialization-dev libboost-system-dev libboost-thread-dev python3 ccache doxygen graphviz
```

Install all dependencies at once on Arch:

```
sudo pacman -Syu --needed base-devel cmake boost openssl zeromq libpgm unbound libsodium libunwind xz readline expat gtest python3 ccache doxygen graphviz qt5-tools hidapi libusb protobuf systemd
```

Install all dependencies at once on Fedora:

```
sudo dnf install gcc gcc-c++ cmake pkgconf boost-devel openssl-devel zeromq-devel openpgm-devel unbound-devel libsodium-devel libunwind-devel xz-devel readline-devel expat-devel gtest-devel ccache doxygen graphviz qt5-linguist hidapi-devel libusbx-devel protobuf-devel protobuf-compiler systemd-devel
```

Install all dependencies at once on openSUSE:

```
sudo zypper ref && sudo zypper in cppzmq-devel libboost_chrono-devel libboost_date_time-devel libboost_filesystem-devel libboost_locale-devel libboost_program_options-devel libboost_regex-devel libboost_serialization-devel libboost_system-devel libboost_thread-devel libexpat-devel libminiupnpc-devel libsodium-devel libunwind-devel unbound-devel cmake doxygen ccache fdupes gcc-c++ libevent-devel libopenssl-devel pkgconf-pkg-config readline-devel xz-devel libqt5-qttools-devel patterns-devel-C-C++-devel_C_C++
```

Install all dependencies at once on macOS with the provided Brewfile:

```
brew update && brew bundle --file=contrib/brew/Brewfile
```

FreeBSD 12.1 one-liner required to build dependencies:

```
pkg install git gmake cmake pkgconf boost-libs libzmq4 libsodium unbound
```

### Cloning the repository

Clone recursively to pull-in needed submodule(s):

---

##  Build Instructions

## Build (Linux)
~~~bash
sudo apt update && sudo apt install -y build-essential cmake pkg-config libssl-dev libzmq3-dev \
libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline-dev libexpat1-dev \
qttools5-dev-tools libhidapi-dev libusb-1.0-0-dev libprotobuf-dev protobuf-compiler \
libudev-dev libboost-all-dev git

git clone --recursive https://github.com/domajor/noxcoin-project.git noxcoin
cd noxcoin

mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DMANUAL_SUBMODULES=1
make -j$(nproc)

~~~
Binaries will be in `build/bin`.

### System Requirements
- CPU with **AES-NI** (RandomX)
- **4 GB RAM** (8 GB recommended)
- **~2 GB** disk

---

## Build Instructions for Other Systems

### macOS (Homebrew)
Install packages via the repo Brewfile, then build:
~~~bash
brew update && brew bundle --file=contrib/brew/Brewfile
make release
~~~

### Windows (MSYS2 / MINGW64)
Follow the MSYS2 setup, then:
~~~bash
pacman -Syu
pacman -S mingw-w64-x86_64-toolchain make mingw-w64-x86_64-cmake \
  mingw-w64-x86_64-boost mingw-w64-x86_64-openssl mingw-w64-x86_64-zeromq \
  mingw-w64-x86_64-libsodium mingw-w64-x86_64-hidapi mingw-w64-x86_64-unbound
make release-static -j"$(nproc)"
~~~
Executables will be in `build/release/bin`.

### FreeBSD
~~~bash
pkg install git gmake cmake pkgconf boost-libs libzmq4 libsodium unbound
gmake release
~~~

### OpenBSD
~~~bash
pkg_add cmake gmake zeromq libiconv boost libunbound
gmake
~~~

### NetBSD
~~~bash
pkg_add cmake gmake boost-libs protobuf readline libusb1 zeromq git-base pkgconf
gmake release
~~~

### Solaris
~~~bash
mkdir -p build/release && cd build/release
cmake -DCMAKE_LINKER=/path/to/ld -DCMAKE_BUILD_TYPE=Release ../..
gmake
~~~

### Cross-compilation
See **docs/depends.md**.

---

## Run the Daemon
Foreground:
~~~bash
./build/release/bin/noxcoind
~~~
Background:
~~~bash
./build/release/bin/noxcoind --log-file noxcoind.log --detach
~~~

---

## Documentation
- Full build & dependencies: **docs/README.md**  
- Tor / anonymity networks: **docs/ANONYMITY_NETWORKS.md**  
- macOS packages: **contrib/brew/Brewfile**  
- Cross-compile (depends): **docs/depends.md**  
- License: **LICENSE**
