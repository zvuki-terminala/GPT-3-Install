# GPT-3 Installation
## _Инструкция по установке_

Содержание :

- Подготовка
- Драйверы NVidia
- Установка GPT
- Настройка GPT
- Запуск веб-сервера на Uvicorn
- Ошибки

## Подготовка 



Клонируйте репозиторий git:

    $git clone https://github.com/zvuki-terminala/GPT-3-Install.git
    
После клонирования репозитория переместите файлы скриптов в домашний каталог:

    $cd GPT-3-Install
    $mv full-gpt3 ..
    $mv nvidiadrivers ..
    $mv conda ..
    $cd ..
    
Установите Conda запустив скрипт:

    $./conda
    
По ходу установки нажисайте ENTER или вводите yes при запросе.
    
## Драйверы NVidia

Установите драйверы NVidia CUDA и Tensorflow запустив скрипт nvidiadrivers:

    $./nvidiadrivers
   
Для работы CUDA вам нужно будет обновить файл ~/.profile откройте его для редактирования

    $sudo vi ~/.profile
    
Добавьте в конец файла следующие строки:

    set PATH for cuda 10.1 installation
    if [ -d "/usr/local/cuda-10.1/bin/" ]; then
        export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
        export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    fi

После обновления файла ~/.profile перезагрузите систему 

    $sudo reboot

## Установка GPT-3

После перезагрузки системы запустите скрипт full-gpt3:
    
    $./full-gpt3

По окончании скрипта будет скачан репозиторий gpt-3, находится файлы gpt будут в папке ru-gpts.
Дополнительно будет установлен nvtop.

## Настройка GPT-3

Для полной установки GPT-3 перейдите в директорию ru-gpts:

    $cd ru-gpts
    $virtualenv gpt_env
    $source gpt_env/bin/activate
    $pip3 install -r requirements.txt    
    
## Запуск веб-сервера на Uvicorn

После проверки работоспособности нейросети можно приступать к запуску приложения с веб-сервером Uvicorn.
Перейдите в директорию ru-gpts и введите команду:

    $mkdir logs 
    $sudo chmod u+x conda
    $conda update --all
    $conda env create
    
Conda проверит и установит дополнительные пакеты если потребуется, а папка logs необходима для записи логов работы Uvicorn'а.
Следом идет установка Nvidia Apex:
    
    $sudo apt-get update
    $sudo apt-get upgrade
    $sudo reboot
    
    [Перезагрузка]
    
    $git clone https://github.com/NVIDIA/apex
    $cd apex
    $pip install -v --disable-pip-version-check --no-cache-dir ./
   
Переходим к установке Uvicorn:

    $pip3 install fastapi
    $pip3 install uvicorn
    $pip3 install tendo
    
После установки веб-сервера можно запускать приложение, но перед этим проверьте наличие папки pelevin в папке ru-gpts,
если она отсутствует поместите модель в папку ru-gpts, после этого можно запускать приложение:

    [предварительно надо открыть порт]
    
    $sudo iptables -A INPUT -i lo -j ACCEPT
    $sudo iptables -A OUTPUT -o lo -j ACCEPT
    $sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    $sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    $sudo iptables -A INPUT -p tcp --dport 8000 -j ACCEPT

    $cd ru-gpts
    
    [Перед каждым запуском веб-сервера]

    $git pull
    $export DEVICE="cuda:0"
    $export INSTANCE="0"
    $export MODEL="pelevin"
    $uvicorn rest:app --host 0.0.0.0 --port 8000
    
После запуска приложения можно проверить подключение в браузере:

    https://[ip-адрес сервера]:8000/health
    
Ответ должен быть true.
Дополнительно можно открыть интерфейс Fast-API

    https://[ip-адрес сервера]:8000/docs
    
Для завершения работы приложения зажмите дважды комбинацию Ctrl + C в bash.           
    

    

    
    

