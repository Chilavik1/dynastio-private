# 🚀 Пошаговое руководство по настройке сервера

![Docker](https://shields.io🟢_Active-blue?style=for-the-badge&logo=docker)
![OS](https://shields.io)

Понятный гайд по подключению к хосту, развертыванию Docker-окружения и запуску приватного игрового сервера.

---

## 📌 Содержание
1. [💻 Шаг 1: Подключение к хосту](#-шаг-1-подключение-к-хосту)
2. [🐳 Шаг 2: Установка Docker](#-шаг-2-установка-docker)
3. [🎮 Шаг 3: Загрузка сервера](#-шаг-3-загрузка-сервера)

---

## 💻 Шаг 1: Подключение к хосту

Для управления сервером вам понадобится SSH-клиент. Вы можете использовать любой удобный инструмент:

* **MobaXterm** — отличное решение «всё в одном» (содержит встроенную консоль и файловый менеджер SFTP).
  
  <details>
  <summary>📸 Посмотреть интерфейс MobaXterm</summary>
  
  ![Интерфейс MobaXterm]<img width="1280" height="683" alt="Xterm" src="https://github.com/user-attachments/assets/d5b11f1d-4f5c-4278-9bdc-e08dd10ebd5e" />

  </details>

* **VS Code (Remote - SSH)** — официальный плагин для редактора кода. В данном руководстве мы будем использовать именно его.

  <details>
  <summary>📸 Посмотреть плагин VS Code</summary>
  
  ![Плагин VS Code Remote SSH]<img width="1280" height="683" alt="VScode" src="https://github.com/user-attachments/assets/932bf60c-863a-4a3d-816a-99f87932ddb6" />

  </details>

### 🔑 Данные для авторизации
При подключении программа запросит у вас следующие данные (их можно найти в панели вашего хостинг-провайдера):
* **IP-адрес:** `IPv4` вашего сервера.
* **Логин:** обычно `root` (для ОС Ubuntu).
* **Пароль:** создается вами при покупке/настройке виртуального сервера.

---

## 🐳 Шаг 2: Установка Docker

После успешного подключения к консоли последовательно выполните следующие команды для настройки Docker.

### 1. Обновление индексов пакетов
```bash
sudo apt update
```

### 2. Установка зависимостей
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

### 3. Добавление GPG-ключа Docker
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

### 4. Подключение официального репозитория
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

### 5. Установка Docker CE
```bash
sudo apt install docker-ce -y
```

### 6. Проверка статуса службы
```bash
sudo systemctl status docker
```

> ✅ **Проверка:** Если служба работает корректно, в консоли вы увидите статус `active (running)`.
> 
> <details>
> <summary>📸 Пример успешного вывода в консоли</summary>
> 
> ![Статус Docker](ссылка_на_скрин_вывода_в_консоль.png)
> </details>

---

## 🎮 Шаг 3: Загрузка сервера

Когда Docker полностью готов к работе, скачайте официальный образ приватного сервера командой:

```bash
docker pull n0uk/dynast.io-server-private:release
```

---
💡 **Заметили ошибку или хотите дополнить гайд?** Создайте [Pull Request](https://github.com) или откройте Issue!
