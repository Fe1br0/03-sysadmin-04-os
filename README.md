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



