# Noxcoin – Private. Secure. Untraceable
 
**Noxcoin** is a fork of **Monero** — the most battle-tested privacy cryptocurrency — but with several distinct improvements and a new community-first direction. It retains Monero’s cryptographic strength while adjusting emission, scaling behavior, and decentralization incentives. 

## Links
- **Website:** https://noxcoin.org  
- **Explorer:** https://explorer.noxcoin.org/  
- **Mining Pool:** https://noxcoin.minorpool.com/  
- **Discord:** https://discord.gg/z9ASXhjw

---

## Key Features
- **Based on Monero Core** with proven privacy guarantees
- **Privacy stack**: Ring Signatures, Stealth Addresses, RingCT, Bulletproofs+
- **Fixed supply**: 21M NOX (no tail emission)
- **Fast blocks**: 120 seconds
- **Low fees**: 0.0000005 NOX/kB (~6× cheaper than Monero)
- **Fair mining & decentralization**: CPU-friendly RandomX

---

## Build (Linux)
~~~bash
sudo apt update && sudo apt install build-essential cmake pkg-config libssl-dev libzmq3-dev \
libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline-dev libexpat1-dev \
qttools5-dev-tools libhidapi-dev libusb-1.0-0-dev libprotobuf-dev protobuf-compiler \
libudev-dev libboost-all-dev

git clone --recursive https://github.com/domajor/noxcoin
cd noxcoin

mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
~~~
Binaries will be in `build/release/bin`.

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
make release"
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
