# Домашнее задание к занятию "3.4. Операционные системы, лекция 2"

1. На лекции мы познакомились с node_exporter. В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой unit-файл для node_exporter:

>>> поместите его в автозагрузку,
>>> 
>>> предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на systemctl cat cron),
>>> 
>>> удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

`Разархивировал node_exporter по пути /opt/node_exporter , далее создал юнит файл в /etc/systemd/system/node_exporter.service со следующими параметрами:`

[Unit]
Description=Node Exporter

[Service]
ExecStart=/opt/node_exporter

[Install]
WantedBy=default.target

`Выполнил команды sudo systemctl daemon-reload /  sudo systemctl enable node_exporter.service / sudo systemctl start node_exporter.service тем самым запустил перечитку конф файлов , затем автовключение сервиса при запуске ВМ и наконец сам запуск сервиса`

![image](https://user-images.githubusercontent.com/106814458/176315877-99c04968-efb6-471d-944e-4bc7ca379034.png)

`К сожалению на примере systemctl cat cron так и не понял как добавить опций нашему сервису.Смог только уловить суть , что в строчке EnvironmentFile= можно указать внешний файл с переменными и затем в строке ExecStart= указать эти переменные в виде ключей , гугл не смог помочь или я плохо искал , был бы благодарен за ссылку где об этом можно почитать более информативно`

`Удостоверился что после выполнения ребута ВМ node_exporter автоматически поднимается скриншоты с подтверждением ниже:`

![image](https://user-images.githubusercontent.com/106814458/176321014-59b4e8b6-6488-4c82-8644-948fa39d1eb1.png)

![image](https://user-images.githubusercontent.com/106814458/176321037-345481c0-6384-4f9a-a4fd-940723cb1804.png)

2. Ознакомьтесь с опциями node_exporter и выводом /metrics по-умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.


`Для CPU:`
> node_cpu_seconds_total{cpu="0",mode="user"}
> 
> node_cpu_seconds_total{cpu="0",mode="system"}
> 
>node_cpu_seconds_total{cpu="0",mode="idle"}

`Для NETWORK:`

> node_network_receive_bytes_total
>
> node_network_receive_errs_total
>
> node_network_transmit_bytes_total

`Для Disk:`

> node_disk_io_time_seconds_total
>
> node_disk_written_bytes_total
>
> node_disk_read_bytes_total

`Для Memory:`

> node_memory_MemAvailable_bytes
>
> node_memory_MemFree_bytes
>
> ode_memory_MemTotal_bytes


3. Установите в свою виртуальную машину Netdata. Воспользуйтесь готовыми пакетами для установки (sudo apt install -y netdata). После успешной установки:

`Ознакомился с метриками которые по умолчанию собирает Netdata`

![image](https://user-images.githubusercontent.com/106814458/176325865-06d1f4c6-9d1a-42c4-9d13-04d025e1fd66.png)


