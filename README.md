## Что тут у нас?
1. [Работа с :octocat:](#работа-с-git-octocat)
2. [Работа с :penguin:](#работа-с-terminal-penguin)
3. [Работа с Sublime](#работа-с-sublime-text)

___
#### Работа с git: :octocat:
[как оформлять readme](https://github.com/GnuriaN/format-README#%D0%9E%D0%B3%D0%BB%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5)

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

___
#### Работа с Terminal: :penguin:
```python
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

cp -r ~/yujin_ocs/yocs_cmd_vel_mux/ ~/catkin_ws/src/turtlebot2/ # переместить папку yocs_cmd_vel_mux 
                                                                  в папку turtlebot2 со всем содержимым

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
