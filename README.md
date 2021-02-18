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
    $mv only-gpt3 ..
    $mv nvidiadrivers ..
    $cd ..
    
## Драйверы NVidia

Установите драйверы NVidia CUDA и Tensorflow запустив скрипт nvidiadrivers:

    $./nvidiadrivers

После установки система перезагрузится. 

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
