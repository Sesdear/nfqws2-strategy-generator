# zapret2-strategy-generator
### English readme: [here](README.en.md)
# RU

Генератор стратегий DPI bypass для nfqws2 / zapret2.

## Зависимости

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

## Сборка

```
git clone [<repo-url>](https://github.com/Sesdear/nfqws2-strategy-generator.git)
cd nfqws2-strategy-generator
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

Бинарник: `./nfqws2-strategy-gen`

## Использование

```
./nfqws2-strategy-gen --profiles <list> [--count N] [--format txt|json]
```

Формат `--profiles`:

```
service:blob:mode[,service:blob:mode...]
```

* `service`: youtube, discord, instagram, twitter, reddit, pinterest (default: youtube)
* `blob`: gosuslugi, vk, vk_kyber, rutracker, max, sberbank, google, iana, iana_big, random (default: gosuslugi)
* `mode`: simple, advanced, mixed (default)
* `--count N`: число стратегий (default: 50)
* `--format txt|json`: формат вывода (default: txt)

Примеры:

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
