# Backup
### Поместить `vagrantfile` в корень, а `inventory.ini` и `playbook.yml` в папку ansible в корне с vagrantfile, запустить `vagrant up`
В данной работе мы настроили резервное копирование с использованием borgbackup и автоматизировали его выполнение с помощью systemd timer. Настройка выполнялась с использованием Vagrant+ansible, что позволило минимизировать ручной труд и обеспечить воспроизводимость процесса.
