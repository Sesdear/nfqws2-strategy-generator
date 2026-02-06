# nfqws2-strategy-generator
### English readme: [here](README.en.md)

Генератор стратегий обхода DPI для **nfqws2 / zapret2**.


---

## Зависимости

### Fedora / RHEL / AlmaLinux
```bash
sudo dnf install gcc-c++ cmake make
```

### Debian / Ubuntu
```bash
sudo apt install g++ cmake make
```

### Arch Linux
```bash
sudo pacman -S gcc cmake make
```

---

## Сборка

```bash
git clone https://github.com/Sesdear/nfqws2-strategy-generator.git
cd nfqws2-strategy-generator
mkdir build && cd build
cmake ..
cmake --build . -j$(nproc)
```

Исполняемый файл будет доступен как:
```bash
./nfqws2-strategy-gen
```

---

## Использование

```bash
./nfqws2-strategy-gen --domains <список> --blob <пресет_или_файл> [опции]
```

---

## Обязательные параметры

### `--domains` / `-d`
Список сервисов через запятую:

```
youtube,discord,instagram,twitter,reddit,pinterest
```

Если указан неизвестный сервис — используется `youtube`.

Пример:
```bash
-d youtube,discord
```

---

### `--blob` / `-b`
Источник поддельного TLS ClientHello.

#### Встроенные пресеты:
```
gosuslugi
vk
vk_kyber
rutracker
max
sberbank
google
iana
iana_big
random
```

#### Кастомный файл (сырые байты):
```
./myhello.bin
/path/to/custom.dat
fakehello.raw
```

---

## Опциональные параметры

### `--mode` / `-m`
Режим генерации стратегий:

```
simple    — лёгкий / быстрый
advanced  — агрессивный обход DPI
mixed     — simple + advanced (по умолчанию)
```

---

### `--count` / `-c N`
Количество стратегий для каждой комбинации сервис + blob.

По умолчанию:
```
50
```

---

### `--format` / `-f`
Формат вывода:

```
txt   (по умолчанию)
json
```

---

## Примеры использования

```bash
# Базовый запуск для YouTube с пресетом gosuslugi
./nfqws2-strategy-gen --domains youtube --blob gosuslugi
```

```bash
# Несколько сервисов, случайный пресет, расширенный режим
./nfqws2-strategy-gen -d youtube,discord -b random -m advanced -c 120
```

```bash
# Сохранение в JSON, кастомный файл ClientHello
./nfqws2-strategy-gen --domains instagram,twitter --blob ./custom_hello.bin --format json
```

```bash
# Один сервис, свой файл, смешанный режим, 80 стратегий
./nfqws2-strategy-gen -d reddit -b /tmp/fake_tls_clienthello.dat -m mixed -c 80
```

---

## Выходные файлы

Имена файлов формируются автоматически:

```
strategies_<service>_<blob>_<mode>.<format>
```

Пример:
```
strategies_youtube_gosuslugi_mixed.txt
```

---

## Справка

```bash
./nfqws2-strategy-gen --help
./nfqws2-strategy-gen -h
```

Справка также отображается, если не указаны обязательные параметры
`--domains` и `--blob`.

---

## Примечания

* Генератор **не проверяет валидность стратегий** — он создаёт разнообразные
  комбинации параметров для тестирования.
* Рекомендуется запускать `nfqws2` с ограниченным набором стратегий и
  постепенно отбирать рабочие.
