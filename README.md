# lynxtiger_infra
lynxtiger Infra repository

### ДЗ bastion_homework

Add to local machine file '~/.ssh/config' with the following content:

Host bastion
HostName 84.201.165.36
User appuser
IdentityFile ~/.ssh/app_user.pub

##### для любого хоста подсети - самостоятельная работа

Host 10.129.0.*
ProxyCommand ssh bastion -W %h:%p
User appuser
IdentityFile ~/.ssh/app_user.pub

##### для конкретного хоста по имени - дополнительное задание
##### здесь ключ одинаковый используется. В идеале имеет смысл использовать для бастионной машины один ключ, а для внутренних другой
Host someinternalhost
HostName 10.129.0.25
ProxyCommand ssh bastion -W %h:%p
User appuser
IdentityFile ~/.ssh/app_user.pub

bastion_IP = 84.201.165.36
someinternalhost_IP = 10.129.0.25

### ДЗ 6 TestApp
testapp_IP = 51.250.74.127
testapp_port = 9292

#### Самостоятельная работа
Скрипт install_ruby.sh содержит команды по установке Ruby
Скрипт install_mongodb.sh содержит команды по установке MongoDB
Скрипт deploy.sh содержит команды скачивания кода, установки зависимостей через bundler и запуск приложения

#### Дополнительное задание
Скрипт startup.sh содержит вызов всех трех скриптов из списка выше

###### команда деплоя инстанса -
yc compute instance create \
  --name reddit-app \
  --metadata-from-file user-data=metadata.yaml \
  --hostname reddit-app \
  --memory=4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604-lts,size=10GB \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --metadata serial-port-enable=1 \
  --ssh-key ~/.ssh/appuser.pub
