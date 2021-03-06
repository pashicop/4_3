### Как сдавать задания

Вы уже изучили блок «Системы управления версиями», и начиная с этого занятия все ваши работы будут приниматься ссылками на .md-файлы, размещённые в вашем публичном репозитории.

Скопируйте в свой .md-файл содержимое этого файла; исходники можно посмотреть [здесь](https://raw.githubusercontent.com/netology-code/sysadm-homeworks/devsys10/04-script-03-yaml/README.md). Заполните недостающие части документа решением задач (заменяйте `???`, ОСТАЛЬНОЕ В ШАБЛОНЕ НЕ ТРОГАЙТЕ чтобы не сломать форматирование текста, подсветку синтаксиса и прочее, иначе можно отправиться на доработку) и отправляйте на проверку. Вместо логов можно вставить скриншоты по желани.

# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            }
            { "name" : "second",
            "type" : "proxy",
            "ip : 71.78.22.43
            }
        ]
    }
```
  Нужно найти и исправить все ошибки, которые допускает наш сервис  
  Исправленный JSON:
```
{ "info": "Sample JSON output from our service\\t",
    "elements":[
        { "name": "first",
        "type": "server",
        "ip": 7175
        },
        { "name": "second",
        "type": "proxy",
        "ip": "71.78.22.43"
        }
    ]
}
```

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

### Ваш скрипт:
```python
import json
import socket
import time
import yaml


def get_one_ip():
    list_services = []
    for service in services:
        serv_ip = {}
        serv_ip[service] = socket.gethostbyname(service)
        list_services.append(serv_ip)
    # print(list_services)
    return list_services


def get_all_ip():
    serv_ip = {}
    for service in services:
        serv_ip[service] = socket.gethostbyname_ex(service)[2]
    return serv_ip


def save_ip(list_ip):
    with open("1.json", "w") as js:
        json.dump(list_ip, js)
    with open("1.yaml", "w") as ym:
        yaml.dump(list_ip, ym, indent=2, explicit_start=True, explicit_end=True)
    return


def print_log(l_ip):
    for dict_s in l_ip:
        for service, ip in dict_s.items():
            ip_new = socket.gethostbyname(service)
            if ip != ip_new:
                print(f'[ERROR] {service} IP mismatch: {ip} {ip_new}')
                dict_s[service] = ip_new
                save_ip(l_ip)
                # print(list_ip)
            print(f'{service} - {ip_new}')
        time.sleep(1)


if __name__ == '__main__':
    services = ['drive.google.com', 'mail.google.com', 'google.com']
    # list_ips = get_all_ip()
    # print(list_ips)
    list_ip = get_one_ip()
    save_ip(list_ip)
    while True:
        print_log(list_ip)

```

### Вывод скрипта при запуске при тестировании:
```
drive.google.com - 64.233.162.194
[ERROR] mail.google.com IP mismatch: 64.233.161.19 64.233.161.18
mail.google.com - 64.233.161.18
google.com - 173.194.73.100
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
[{"drive.google.com": "64.233.162.194"}, {"mail.google.com": "64.233.161.18"}, {"google.com": "173.194.73.100"}]
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
---
- drive.google.com: 64.233.162.194
- mail.google.com: 64.233.161.18
- google.com: 173.194.73.100
...
```

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

Так как команды в нашей компании никак не могут прийти к единому мнению о том, какой формат разметки данных использовать: JSON или YAML, нам нужно реализовать парсер из одного формата в другой. Он должен уметь:
   * Принимать на вход имя файла
   * Проверять формат исходного файла. Если файл не json или yml - скрипт должен остановить свою работу
   * Распознавать какой формат данных в файле. Считается, что файлы *.json и *.yml могут быть перепутаны
   * Перекодировать данные из исходного формата во второй доступный (из JSON в YAML, из YAML в JSON)
   * При обнаружении ошибки в исходном файле - указать в стандартном выводе строку с ошибкой синтаксиса и её номер
   * Полученный файл должен иметь имя исходного файла, разница в наименовании обеспечивается разницей расширения файлов

### Ваш скрипт:
```python
???
```

### Пример работы скрипта:
???
