# **ШПАРГАЛКА ПО GIT**  
---

## Список полезных команд  

### Навигация:  

- **pwd** - показать, в какой я папке;
- **ls** - показать файлы и папки в текущей папке;
- **ls -a** - показать также скрытые файлы и папки, названия которых начинаются с символа **.**;
- **cd** _имя папки_ - перейти в папку "имя папки";
- **cd** _папка1_/_папка2_ - перейти в папку2, которая внутри папки1;
- **cd ..** - перейти на уровень выше, в родительскую папку;
- **cd -** - перейти в домашнюю директорию (/Users/Username);
- **cd /** - перейти в корневую директорию.


**_Директория_** (directory, folder) — это узел, содержащий информацию о файлах, их имена и ссылки на файлы и на другие директории во внешней памяти.

### Работа с файлами и папками: 

#### Создание:  

- **touch _file.txt_** - создать файл _file.txt_ в текущей папке;
- **touch _file.txt project.exe script.js_** - создать несколько файлов в текущей папке;
- **mkdir _имя-директории_** - создать папку в текущей папке.

#### Копирование и перемещение: 

- **cp _file.txt_ ~/my-dir** - скопировать файл в другое место;
- **mv _file.txt_ ~/my-dir** - перемести файл в другое место.

#### Чтение  

- **cat _file.txt_** - вывести содержание текстового файла file.txt

#### Удаление  

- **rm _file.txt_** - удалить файл _file.txt_;
- **rmdir _my-dir_** - удалить папку _my-dir_;
- **rm -r _my-dir_** - удалить папку _my_dir_ и все содержимое в ней (**безвозвратно**).

## Полезные возможности    

- Команды можно выполнять списком, разделяя их с помощью **&&**;
- У консоли есть память - буфер с несколькими последними командами, между которыми можно перемещаться с помощью стрелок;
- **Tab** используется для того, чтобы git "дописал" имя файла или папки. Достаточно ввести несколько первых символов названия и нажать **Tab**;

## Как через Git подключиться к удаленному репозиторию на GitHub 
**Репозиторий** (от англ. repository — хранилище) — место, где хранятся и поддерживаются какие-либо данные.  
Чаще всего данные в репозитории хранятся в виде файлов, доступных для дальнейшего распространения по сети.  

Необходимо зарегестрироваться и создать учетную запись на [GitHub](https://github.com/).   

## Публичный и приватный ключ  
- **Публичный ключ** передаётся сторонним серверам, например, GitHub, для открытия доступа на эти сервера;
- **Приватный ключ**  хранится только на машине и никому не передаётся.  
С помощью **ssh-keygen -t ed25519** создается пара ssh-ключей (приватного и публичного). После этого в консоли выведется "изображение" вашего ключа, а в папке **~/ssh/** появятся два файла: **id_ed25519** и **id_ed25519.pub** с приватным и публичным ключами соответственно. Файл с расширением **pub** - приватный, его ни в коем случае нельзя никому отправлять!  

### Указываем публичный ключ на GitHub  

Для того чтобы GitHub (или иной сервис) мог авторизовать ваше подключение, необходимо указать в настройках аккаунта публичный ssh-ключ, который вы будете использовать для доступа к репозиториям (также можно указать несколько ключей).  

На github.com эта процедура делается следующим образом:   
- Переходим в "Settings" -> "SSH and GPG keys" (прямая ссылка).
- Нажимаем "New SSH key".
- В поле "Key" вставляем содержимое файла **id_ed25519.pub**.
- Нажимаем "Add SSH key".  

  
Затем в консоли необходимо ввести команду **$ ssh -T git@github.com**, появится следующее сообщение:  

The authenticity of host 'github.com (140.82.121.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])?   

Написать **yes**  
Затем создать директорию (например, **first-project** с помощью **touch**) и подключить ее к удаленному репозиторию через команду:  
**git remote add origin git@github.com: _your-nickname_/first-project.git**, где _your-nickname_ - ваш ник в GitHub  

## Создание коммитов  

**Коммит** - комментарий к каждому изменению в репозитории. Создается с помощью команды:  
**git commit -m 'Ваш коммит'**


## РАБОТА С РЕПОЗИТОРИЕМ

- **git init [имя проекта]** - создать новый локальный репозиторий;
- **git status** - посмотреть список новых или измененных файлов, которые еще не закомитены;
- **git diff** - показать изменения, которые еще не проставлены;
- **git diff HEAD** - показать все индексированные и неиндексированные изменения;
- **git branch** - показать все локальные ветки;
- **git branch -av** - показать все локальные и удаленные ветки;
- **git branch _new_branch_** - создать новую ветку _new_branch_;
- **git branch -d _new_branch_** - удалить ветку _new_branch_;
- **git add _file.txt_** - индексировать файл, готовый к коммиту;
- **git add -all** - индексировать ВСЕ файлы, готовые к коммиту;
- **git commit -m "commit message"** - закоммитить (зафиксировать индексированные файлы с комментарием в историю);
-----

_Важно помнить_, что ВСЕГДА вначале идет индексация **git add file.txt** и только затем коммит **get commit**!

-----

- **git push** - применить локальные изменения на удаленный сервер.

**Необходимо помнить последовательность**:  
1. git add --all (индексация изменений);
2. git commit -m 'Ваш коммит' (добавление комментария);
3. git push (применение локальных изменений на удаленный сервер).