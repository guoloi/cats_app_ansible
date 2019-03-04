# cats_app_ansible

On Ubuntu only! Do not work on CentOS.

Using this ansible script you will be able to implement Cats_app on any number of slave Virtual Mashines.

I suppose that:

1. Every VM have Python 2.7 installed (apt install python)
2. There is user "user" on every Slave VM, which is able to escalate privileges using "sudo" command
3. Management VM has ssh access to every Slave VM by key (ssh-copy-id user@Slave_VM_IP)
4. On Management VM ansible is installed (apt install ansible)
5. In case of reboot you have to run script again, or start cats_app manualy

This script DO NOT install virtual mashines!

# Management VM:

ubuntu-18.04.2

# Slave VM(s)

ubuntu-18.04.2

# Command to run script:

ansible-playbook main.yaml -K

<br/>

# Развертывание приложения (написано Marley). Тестировалось в ubuntu linux 18.04.

1.  Установить vagrant
    https://www.vagrantup.com/

    \$ vagrant plugin install vagrant-hosts

2)

    $ cd ~
    $ git clone --depth=1 https://github.com/guoloi/cats_app_ansible
    $ cd cats_app_ansible/vm/
    $ ssh-add ~/.vagrant.d/insecure_private_key
    $ vagrant up

3)

Двумя сессиями подключиться к созданным виртуальным машинам:

    $ vagrant ssh client
    $ vagrant ssh server

<br/>

### Client и Server

    $ sudo su  -
    # adduser --disabled-password --gecos "" user
    # usermod -aG sudo user
    # passwd user

    vi /etc/ssh/sshd_config
    PasswordAuthentication yes

    # service sshd reload

<br/>

### Client

    # vi /etc/ansible/hosts

добавить ip или достаточно hostname

    server

<br/>

    # su - user

    $ ssh-keygen -t rsa
    $ ssh-copy-id user@server

    // Устанавливаем python 2.x на сервер
    $ ssh -tt server "sudo apt install -y python"

    $ cd ~
    $ git clone --depth=1 https://github.com/guoloi/cats_app_ansible
    $ cd cats_app_ansible/
    $ ansible-playbook main.yaml -K

http://192.168.56.102:8080/

<br/>

![Application](/img/cat.png?raw=true)

<br/>

# TODO: Что нужно сделать!

- Передавать адрес сервера на котором должно разворачиваться приложение в командной строке
- Nginx как прокси сервер приложения, работающий на 80 порту.
- Сообщение о результатах деплоя в slack и телеграм.
