# lynxtiger_infra
lynxtiger Infra repository

ДЗ bastion_homework

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
