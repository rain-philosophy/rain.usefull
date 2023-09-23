## :point_down: Что тут у нас? 
1. [Работа с :octocat:](#работа-с-git-octocat)
2. [Работа с :penguin:](#работа-с-terminal-penguin)
3. [Работа с Sublime](#работа-с-sublime-text)
4. [Работа с asyncio](#работа-с-asyncio)
5. [(C)читай hacker](#считай-hacker)

Вопросы:
Если await переключает программу на выполнение других тасков, то это разве не значит go to? я понимаю если await smthdef, но когда это  await asyncio.sleep...

___
#### Работа с git: :octocat:
[как оформлять readme - GitHub](https://github.com/GnuriaN/format-README#%D0%9E%D0%B3%D0%BB%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5)     
[настройка ssh - YouTube](https://youtu.be/fYFiQ7lpfiE?t=162)     
[Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

##### Команды:
```python
git clone https://... # скачать с Git

git add file # не сообщает git о необходимости добавления файла в репозиторий, а указывает текущее состояние файла,
             # чтобы его можно было зафиксировать позже.
git add . # альтернатива, если находишься в текущей папке с файлами. Добавляет все из этой папки

git commit                     # позволяет интерактивно редактировать комментарии для коммита
           -m "smth commented" # позволяет коммитить с комментарием прямо сейчас
           
git log # история коммитов
  git log --pretty=oneline # лог в одну строку
  git log --pretty=oneline --max-count=2
  git log --pretty=oneline --since='5 minutes ago'
  git log --pretty=oneline --until='5 minutes ago'
  git log --pretty=oneline --author=<your name>
  git log --pretty=oneline --all
  git log --all --pretty=format:"%h %cd %s (%an)" --since='7 days ago'
  git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short # наиболее подходящий формат логов
          --pretty="..." # определяет формат вывода
                    %h # вывод хэша
                    %ad # вывод даты
                    %s # вывод коммента
                    %an # вывод имени автора
                                                --graph # вывод в виде какого-то макета графа ASCII
                                                --date=short # keeps the date format short and nice
                                                
git checkout -b branchname # создать новую ветку
               -b # новая ветка
git branch # чекнуть в какой ветке находимся
git checkout branchname # переключиться на необходимую ветку

git --version # чекнуть версию git

ls -al # показать все файлы в папке, в том числе и скрытые

git config --global core.editor nano # сменить editor на nano (был subl)
```

##### Инструкция стандартная:

```python
git clone sshlink # Клонируем репозиторий с github через ssh ключ
subl filename # Изменяем файл в редакторе
git add filename # Сохраняем текущее состояние файла, для последующего добавления в репозиторий
subl filename # Можем снова изменить файл
git status # Проверить текущий статус состояний (будет один готовый к комиту файл и один еще не добавленный)
git commit # Фиксируем изменения (первого добавления)
git add . # Добавляем второе изменение файла
git status # Смотрим готово ли к коммиту
git commit # Коммитим
git status # Смотрим статус
git push # Загружаем на удаленный репозиторий, все произойдет автоматически, т.к. юзаем ssh ключ
```

##### Создание новой ветки (создается обычно для разработки и тестирования новой фичи, чтобы на мастере оставить стабильную версию):

```python
git checkout -b branchname # Создать новую ветку
git branch # Посмотреть в какой мы ветке
# Переключиться в определенную ветку:
  git checkout branchname
  git branch 
# Работаем в этой ветке:
  subl filename
  git status
  git add .
  git status
# Коммитим в новой ветке:
  git commit
  git status
git push # Наша гениальная идея должна отправиться в наш репозиторий
git push --set-upstream origin branchname # Будет подсказка, из нее
```

##### Мёрдж:
```python
# В репо в вебе заходим и делаем pull request and merge
git pull # На своей машине
```

##### Удоление ветки:
```python
  git branch --delete branchname
```

[:point_up: Оп и ап](#point_down-что-тут-у-нас)
___
#### Работа с Terminal: :penguin:
```python
ssh user_name@ip -p port_number # подключение по ssh

sourcedefender encrypt file_name # кодирование

scp -P port_number file_name user_name@ip:/home/dir_name/ # перекидывание файла по ssh с домашнего компа на сервер

nohup python3 -m sourcedefender filename.pye > output.txt 2>&1 & # запуск процесса на сервере с записью вывода в файл 
# 2>&1 означает, что терминал будет писать стандартные ошибки тоже в лог

echo $! > save_pid.txt # сохраняет пид процесса, чтоб потом не искать

ps -ef | grep command_name(python3) # найдет пид процесса

cat pid.txt # посмотреть содержимое текстового файла

kill 2566 # убить процесс
kill -KILL 2566 # убить его полностью, если по хорошему не получилось

tail my.log # вывести последние 10 строк лога (наверно про файл также)

tail -f my.log # лог в прямом эфире

sudo apt update
sudo apt upgrade


ctrl + alt + T # открыть терминал
ctrl + shift + T # новую вкладку терминала

ctrl + D # закрыть терминал
exit # закрыть терминал

tmux # много терминалов

clear # очистить терминал

Tab x2 # вывести список всех команд

'#! /bin/bash' # скрипт (в текстовом файле) без ''

pwd # показать текущую директорию

touch file1.txt # создать файл
> file1.txt # создать новый, если файла нет
cat > file1.txt # написать необходимый текст и нажать ctrl + D чтобы сохранить файл

echo # печатает строки, которые передаются в вывод
echo $USER # имя вошедшего в систему пользователя
     -e # интерпретация escape-символов (\n, \t ...)
"..." > file1.txt # перезаписать существующий файл
  echo -e "..." > file1.txt
"..." >> file1.txt # добавить в существующий файл 
  echo -e "..." >> file1.txt

mkdir sema # создать каталог sema
mkdir sema igor # создать 2 директории одновременно
mkdir -p /tmp/sema/igor # создать дерево директорий

rm file # удалить file
rm -r dir # удалить каталог dir
rm -f file # удалить форсировано file
rm -rf dir # удалить форсировано каталог dir

cp -r ~/yujin_ocs/yocs_cmd_vel_mux/ ~/catkin_ws/src/turtlebot2/ # копировать папку yocs_cmd_vel_mux 
                                                                # в папку turtlebot2 со всем содержимым

ls # просмотр содержимого

cd # переместиться в корень
cd ~/catkin_ws # переместиться из home (~) директории в catkin_ws
cd lib/ # переместиться из текущей директории в папку lib
cd .. # переместиться на уровень выше

mv myfile1.dat myfile2.dat # переименовать файл/папку
mv -v folder1/* ~/rain.pro/rain.dynamic # переместить все файлы папки в другую папку

cat file # просмотр содержимого файла

nano ~/.bashrc # редактировать bashrc файл
nano -c file # редактировать файл с отображением номеров строк

chmod [action] [flag] file_name # сделать файл исполняемым
      [action] = + # установить флаг
                 - # снять флаг
               [flag] = r # чтение
                        w # запись
                        x # выполнение (подсвечивается зелёным)

# Если перекинул фотки из одной системы в виртуалку, то права файлов только root. Чтобы их изменить на общие, надо:
# (https://careerkarma.com/blog/python-permissionerror-errno-13-permission-denied/)
sudo chmod 755 filename

ctrl + C # остановить процесс
ctrl + Z # закрыть процесс, но не останавливать
fg # открыть закрытый процесс

evince pdf_file # открыть пдф файл
nautilus Downloads/ # открыть папку Downloads

source rain.env/bin/activate # подключить jupyter
deactivate # выход из env

gnome-open filename.txt # открыть файл

ctrl + super + D # скрыть все окна

sudo shutdown -h now # выключить Linux
sudo shutdown -r now # перезагрузить Linux
systemctl suspend # отправить Linux в спящий режим

watch progress # отследить загрузку в Linux

zip -re -0 mane.zip rain.dynamic/ # архивировать с паролем
    -r # архивировать рекурсивно
    -e # с паролем
        -0 # степень сжатия: 0 без сжатия, 9 максимальное сжатие

Super+L # залочить экран Linux

df -h # показывает сколько занято места на дисках
   -h            # заставляет ее показывать это в человеко-читаемом формате, а не в байтах (с) Маслов
   /dev/sda_smth # реальные диски
```
[:point_up: Оп и ап](#point_down-что-тут-у-нас)
___
#### Работа с Sublime text:
```python
subl # открыть Sublime Text
subl [options] [files] # открыть файл в Sublime Text
     [options] = -n # в новом окне
                 -a # добавить в открытое окно
                 -w # приостановить командную строку пока редактируется файл
                 -s # оставить окно при открытии ST в следующий раз
```

[:point_up: Оп и ап](#point_down-что-тут-у-нас)
___
#### Работа с asyncio:
##### Минутка истории
```python
# обычная функция перемножения двух чисел
def multyply(a,b):
    return a * b
    
multyply(2,2) # Output: 4
```
```python
# пишем генератор с помощью ключевого слова yield
def generator(a,b):
    while True:
        yield a * b
        a = a + 1

g = generator(2,2) # Output: 4 Output: 6 Output: 8
```
```python
# раньше ассинхронность писали на генераторах, теперь так (тут что-то не так...)
async def asyncfunction(a):
    while True:
        await a
        a = a + 1
    
asyncio.run(asyncfunction())
```

##### Это база
```python
# async — ключевое слово, через которое мы объявляем асинхронную функцию, короутину
async def some_function():
    #function's logic
    pass
```
```python
# await — ключевое слово, через которое мы запускаем асинхронную функцию и передаем управление другим короутинам
await some_function()
```
```python
# awaitable - это все объекты, с которыми мы можем использовать ключевое слово await. Среди них:
#   Coroutines
#   Tasks
#   Futures
#     asyncio.Future — это более низкоуровневое представление asyncio.Task
```

##### Старая школа
```python
# loop (чисто старая школа)
loop = asyncio.get_event_loop() # получаем loop, тк ранее он не существовал - создаем новый
loop.run_until_complete(request_users_data(uid))

# можно даже так делать:
with open("out.csv", "w") as fh: # открываем фаил для записи
    fieldnames = ["id", "name", "email"] # названия колонок в csv файле
    writer = csv.DictWriter(fh, fieldnames=fieldnames) # объект для записи данных в csv формате
    writer.writeheader() # записываем название колонок
    for uid in ids:
        # запускаем короутину в loop и дожидаемся ее результата
        writer.writerow(loop.run_until_complete(request_users_data(uid))) 
        
loop = asyncio.get_event_loop() # получаем loop
loop.create_task(worker()) # добавляем Task в event_loop
loop.run_forever() # навсегда передаем управлени программы на обработку task-ов добавленных в event loop
```
##### Новая школа
```python
# asyncio.run() - ньюфаг в мире асинхронности, поэтому можно обойтись без явного использования loop в нашей программе
asyncio.run(main())
```
##### create_task()
```python
# create_task(asyncfunction()) - инициализация тасков
# можем инициализировать не через loop, а из другой корутины:
import asyncio

async def worker(idx: int):
    while True:
        print(f"worker-{idx} msg")
        await asyncio.sleep(1)

async def main():
    for i in range(3): # добавляем в event loop 3 task-и
        asyncio.create_task(worker(i + 1))

    while True:
        print(f"main msg")
        await asyncio.sleep(1) # сон нужен для передачи управления другим короутинам, нашим worker-ам

asyncio.run(main())
```
##### asyncio.gather() и asyncio.wait()
```python
# Если необходимо одновременно запустить несколько короутин и продолжить выполнение программы после завершения их работы
async def main():
    await asyncio.gather(
        random_sleep(1),
        random_sleep(2),
        random_sleep(3),
        random_sleep(4),
        random_sleep(5),
    )

asyncio.run(main())

# Либо через asyncio.wait()
# return_when=ALL_COMPLETED ставится по умолчанию
async def main():
    await asyncio.wait([random_sleep(i) for i in range(1, 6)], return_when=ALL_COMPLETED)

asyncio.run(main())

# return_when=asyncio.FIRST_COMPLETED если необходимо прервать асинхронные запросы по первому ответившему
```
##### Timeout asyncio.wait() и asyncio.wait_for() 
```python
# если мы хотим выйти из корутины по таймауту
import asyncio

async def request_traffic_jams():
    await asyncio.sleep(10)

async def main():
    try:
        await asyncio.wait_for(request_traffic_jams(), timeout=1.0)
    except asyncio.TimeoutError:
        print("Problems with traffic_jams service")

asyncio.run(main())
```
##### Адекватное завершение программы
```python
# вызываем исключение CancelledError внутри db_operation, 
# оно будет обработано как только event loop передаст управление task-е, обрабатывающей эту короутину

import asyncio
from asyncio import CancelledError

async def db_operation():
    print("operation start")
    try:
        while True:
            print("operation new round")
            await asyncio.sleep(1)
    except CancelledError:
        print("operation was cancelled")
        await asyncio.sleep(1)

    print("operation done")

async def main():
    task = asyncio.create_task(db_operation())
    await asyncio.sleep(5)

    task.cancel() 

    await task # передаем управление db_operation для корректного завершения

asyncio.run(main())
```


[:point_up: Оп и ап](#point_down-что-тут-у-нас)
___
#### (С)читай hacker:
##### Faker - приблуда для генерации рандомных тестовых данных (реалистичных)
```python
pip install Faker # установка

from faker import Faker # импорт

fake = Faker() # создание объекта

# методы:

fake.name() 
# Output: Laura Wilkins

fake.simple_profile()
''' Output: {'username': 'michael87', 
             'name': 'Whitney Oconnor', 
             'sex': 'F', 
             'address': '063 Gonzalez Drives\nOchoahaven, VA 75565', 
             'mail': 'caseybrendan@gmail.com', 
             'birthdate': datetime.date(1943, 1, 8)} '''

fake.address()
fake.province()
fake.city()

fake.url()
# Output: http://hogan.com/

fake.company()
# Output: Miles-Smith
fake.company_suffix()
# Output: and Sons
fake.company_email()
# Output: jennifer71@stevens.net

fake.text()
# Output: Us art couple protect act idea. Already yard argue suffer old story friend. Interest candidate whole point special drive order.
fake.word()
# Output: at
fake.words()
# Output: ['save', 'per', 'public']
fake.sentences()
# Output: ['Marriage feeling official.', 'Skin father suggest live here development.', 'Task suddenly majority.']
```

##### apple keyboard
```python
# выключить клаву
sudo bluetoothctl
power on
agent KeyboardOnly
default-agent
pairable on
# включить клаву
scan on # если остановился поиск
# найти мак адрес клавы
trust 00:C6:3F:96:CE:12
pair 00:C6:3F:96:CE:12
connect 00:C6:3F:96:CE:12

# по дефолту печатает цифрами
sudo apt install numlockx
mumlockx off

xmodmap -pke # посмотреть кейкоды
xmodmap -e "keycode 169 = Delete" # назначить клавише эджект клавишу делит
# сменить местами fn и ctrl https://www.reddit.com/r/AsahiLinux/comments/zmuz5l/is_there_a_way_to_remap_fn_to_ctrl/?rdt=63574:
cd /sys/bus/hid/drivers/apple/module/parameters
sudo nano swap_fn_leftctrl # изменить 0 на 1

# здесь описываются еще файлы и за что отвечают в последней папке
```
[:point_up: Оп и ап](#point_down-что-тут-у-нас)
