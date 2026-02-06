# nfqws2-strategy-generator
### English readme: [here](README.en.md)

Генератор стратегий обхода DPI для nfqws2 / zapret2.

## Зависимости

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

## Сборка

```
git clone https://github.com/Sesdear/nfqws2-strategy-generator.git
cd nfqws2-strategy-generator
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

Исполняемый файл: `./nfqws2-strategy-gen`

## Использование

```
./nfqws2-strategy-gen --domains <список> --blob <пресет_или_файл> [опции]
```

Обязательные параметры (нужен хотя бы один из них, но обычно оба):
```
--domains  | -d    Список сервисов через запятую
                    youtube,discord,instagram,twitter,reddit,pinterest
                    (по умолчанию для каждого элемента → youtube)

--blob     | -b    Источник поддельного TLS ClientHello
                    Встроенные пресеты:
                      gosuslugi | vk | vk_kyber | rutracker | max
                      sberbank | google | iana | iana_big | random
                    Или путь к файлу с сырыми байтами:
                      ./myhello.bin   /path/to/custom.dat   fakehello.raw
                    (по умолчанию → gosuslugi)
```

Опциональные параметры:
```
--mode     | -m    Режим генерации стратегий
                    simple    — лёгкий / быстрый
                    advanced  — агрессивный обход DPI
                    mixed     — simple + advanced (по умолчанию)

--count    | -c N  Количество стратегий на каждую комбинацию (по умолчанию: 50)

--format   | -f    Формат вывода
                    txt   (по умолчанию)
                    json
```

### Примеры

```bash
# Базовый запуск для YouTube с пресетом gosuslugi
./nfqws2-strategy-gen --domains youtube --blob gosuslugi

# Несколько сервисов, случайный пресет, расширенный режим
./nfqws2-strategy-gen -d youtube,discord -b random -m advanced -c 120

# Сохранение в JSON, кастомный файл ClientHello
./nfqws2-strategy-gen --domains instagram,twitter --blob ./custom_hello.bin --format json

# Один сервис, свой файл, смешанный режим, 80 стратегий
./nfqws2-strategy-gen -d reddit -b /tmp/fake_tls_clienthello.dat -m mixed -c 80
```

## Справка

```
./nfqws2-strategy-gen --help
./nfqws2-strategy-gen -h
```

Вывод справки также отображается, если не указаны обязательные параметры `--domains` и `--blob`.
