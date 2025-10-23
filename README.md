# Noxcoin – Private. Secure. Untraceable.

### Note from the Maintainer
Hello!  
This is a community revival of **Noxcoin** — all previous threats have been deleted and purged.  
Please verify everything independently and use only trusted sources.  

My goal is simple: to help this coin survive and grow into a secure, community-driven project.  
I'm not an official developer — this project is open to everyone who wishes to help.  

> “The birth of a baby is very difficult, but what's even more difficult is keeping it alive and ensuring it grows into a valuable person.”

---

##  Project Links
- **Website:** [https://noxcoin.org](https://noxcoin.org)  
- **Explorer:** [https://explorer.noxcoin.org](https://explorer.noxcoin.org)  
- **Mining Stats:** [https://miningpoolstats.stream/noxcoin](https://miningpoolstats.stream/noxcoin)  
- **Discord:** [https://discord.gg/fgu34rYtrV](https://discord.gg/fgu34rYtrV)  
- **Telegram:** [https://t.me/+O0mMgUg1qXM4OWI8](https://t.me/+O0mMgUg1qXM4OWI8)

---

##  Acknowledgments
Special thanks to **@aalnase** ([go-poolmining.com](https://go-poolmining.com)) for his technical help and support in rebuilding and maintaining the Noxcoin network.

---

##  About Noxcoin
**Noxcoin** is a fork of **Monero**, the most battle-tested privacy cryptocurrency — rebuilt with a community-first vision.  
It retains Monero’s strong cryptographic foundation while introducing new emission rules, scaling adjustments, and decentralization incentives.

---

##  Key Features
- **Based on Monero Core** – Proven, privacy-focused architecture  
- **Privacy stack:** Ring Signatures, Stealth Addresses, RingCT, Bulletproofs+  
- **Fixed supply:** 21,000,000 NOX (no tail emission)  
- **Fast blocks:** 120 seconds  
- **Low fees:** 0.0000005 NOX/kB (~6× cheaper than Monero)  
- **Fair mining:** CPU-friendly RandomX algorithm  
- **Community-first governance:** No premine, no dev tax

---

##  Build Instructions

###  Linux
```bash
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
