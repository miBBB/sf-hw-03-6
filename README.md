# Установка Ansible на vm1,vm2,vm3

# Обновление системы Ubuntu
sudo apt update && sudo apt upgrade -y

# Обновление системы CentOS
yum update && yum upgrade -y

# Установка Ansible
sudo apt install -y ansible

# Создание пользователя для Ansible
sudo useradd -m -s /bin/bash ansible

# Установка пароля
sudo passwd ansible

# Добавление в группу sudo
sudo usermod -aG sudo ansible

# Настройка sudo без пароля
echo "ansible ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ansible

# Добавление в группу wheel в CentOS
sudo usermod -aG wheel ansible

# Настройка SSH-авторизации на vm-1
# Переключение на пользователя ansible
sudo su - ansible

# Генерация SSH-ключа
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""

# Копирование публичного ключа на vm2 и vm3
ssh-copy-id ansible@192.168.0.108
ssh-copy-id ansible@192.168.0.103

# Тестирование подключения
ssh ansible@192.168.0.108
ssh ansible@192.168.0.103

# Для установки необходимых сервисов запускам комманду
ansible-playbook -i inventory install_services.yml


