# nfqws2-strategy-generator
### Russian readme: [здесь](README.md)

Strategy generator for DPI bypass in nfqws2 / zapret2.

## Dependencies

Fedora / RHEL / AlmaLinux:
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
git clone https://github.com/Sesdear/nfqws2-strategy-generator.git
cd nfqws2-strategy-generator
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

Binary: `./nfqws2-strategy-gen`

## Usage

```
./nfqws2-strategy-gen --domains <list> --blob <preset-or-file> [options]
```

Required parameters (at least `--domains` and `--blob` are usually needed):
```
--domains  | -d    Comma-separated list of target services
                    youtube,discord,instagram,twitter,reddit,pinterest
                    (default per item → youtube)

--blob     | -b    Fake TLS ClientHello source
                    Built-in presets:
                      gosuslugi | vk | vk_kyber | rutracker | max
                      sberbank | google | iana | iana_big | random
                    Or path to custom raw bytes file:
                      ./myhello.bin   /path/to/custom.dat   fakehello.raw
                    (default → gosuslugi)
```

Optional parameters:
```
--mode     | -m    Strategy generation mode
                    simple    — lightweight / fast
                    advanced  — aggressive DPI bypass
                    mixed     — simple + advanced (default)

--count    | -c N  Number of strategies per combination (default: 50)

--format   | -f    Output format
                    txt   (default)
                    json
```

### Examples

```bash
# Basic usage for YouTube with gosuslugi preset
./nfqws2-strategy-gen --domains youtube --blob gosuslugi

# Multiple services, random preset, advanced mode
./nfqws2-strategy-gen -d youtube,discord -b random -m advanced -c 120

# JSON output with custom ClientHello file
./nfqws2-strategy-gen --domains instagram,twitter --blob ./custom_hello.bin --format json

# Single service, custom file, mixed mode, 80 strategies
./nfqws2-strategy-gen -d reddit -b /tmp/fake_tls_clienthello.dat -m mixed -c 80
```

## Help

```
./nfqws2-strategy-gen --help
./nfqws2-strategy-gen -h
```

The help message is also shown if required parameters `--domains` and `--blob` are missing.
