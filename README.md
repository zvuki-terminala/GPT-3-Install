# GPT-3 Installation
## _Инструкция по установке_

Содержание :

- Подготовка
- Драйверы NVidia
- Установка GPT
- Настройка GPT

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
  
После завершения установок можно приступать к работе с GPT3.
Запустите nvtop, и генератор текста: 
    $bash ./scripts/generate_ruGPT2Large.sh

