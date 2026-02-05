# EN

Strategy generator for nfqws2 / zapret2 DPI bypass.

## Dependencies

Fedora / RHEL / Alma:

```
sudo dnf install gcc-c++ cmake make
```

Debian / Ubuntu:

```
sudo apt install g++ cmake make
```

Arch Linux:

```
sudo pacman -S gcc cmake make
```

## Build

```
git clone <repo-url>
cd nfqws2-strategy-generator
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

Binary: `./nfqws2-strategy-gen`

## Usage

```
./nfqws2-strategy-gen --profiles <list> [--count N] [--format txt|json]
```

Profile format:

```
service:blob:mode[,service:blob:mode...]
```

* `service`: youtube, discord, instagram, twitter, reddit, pinterest (default: youtube)
* `blob`: gosuslugi, vk, vk_kyber, rutracker, max, sberbank, google, iana, iana_big, random (default: gosuslugi)
* `mode`: simple, advanced, mixed (default)
* `--count N`: strategies per profile (default: 50)
* `--format txt|json`: output format (default: txt)

Examples:

```
./nfqws2-strategy-gen --profiles youtube:gosuslugi:mixed
./nfqws2-strategy-gen --profiles youtube:gosuslugi:mixed,discord:vk:advanced --count 100
./nfqws2-strategy-gen --profiles youtube:random:mixed --format json
```

Help:

```
./nfqws2-strategy-gen --help
./nfqws2-strategy-gen -h
```
