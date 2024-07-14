# Конспект курса по GIT от яндекса

**VCS**- Version Control System (система контроля версий)
или синоним(**SCM** - Source Control Management ) система управления исходным кодом.  
команды:

## Ключи
**-a** - ключ (используется ls -a) показывает и скрытые папки тоже  
**-p** - ключ, позволяющий создать целую ветку директорий, например:  
**mkdir** -p dir1/dir2/dir3 создаст папки по такому пути  
**-r** - ключ рекурсии. можно использовать для удаления папки вместе с файлами( в том числе и другими папками) внутри.
rm -r Имя_папки  
**--all** -флаг для выбора всех файлов  

## Комманды
**pwd** - print working directory. Показывает текущую директорию.  
**cd** - (Change Directory) для изменения папки в которой находишься. Например, cd folder перенесет из рабочей директории в папку folder  
**~** - обозначает родительскую директорию  
**..** - да, две точки. Это операция перехода на иерархию выше текущей директории  
**.** - да, одна точка) обращение к текущей директории. нужно для запуска скриптов и программ, которые принимают папку в качестве параметра  
**ls** - list directory content - показывает папки и файлы в текущей директории  
**touch** - создает файл, синтаксис:
touch Имя_файла  
можно через пробел несколько файлов создать
**mkdir** - создает директорию. синтаксис:
mkdir Название_директории.  
**cp** и **mv** - копировать и переместить. синтаксис одинаковый  
Что_копируем/перемещаем Куда копируем/перемещаем  
**cat** - concatinate and print )объединить и распечатать. РАБОТАЕТ ТОЛЬКО С ТЕКСТОВЫМИ ФАЙЛАМИ. открывает и печатает содержимое файла. синтаксис:
cat Имя_файла  
**rm** - remove(удалить) удаляет файл.
Синтаксис: remove Имя_файла  
**rmdir** - remove directory. удаляет папку.
**ВАЖНО** если папка не пуста, то её не удалит)  
**&&** - позволяет выполнять несколько комманд за раз  
**git add** - подготовить файл к сохранению  
**git add .** - для добавления всех файлов из текущей папки в репозиторий    
## пример оформления кода (строго для практики оформления)  
```C++
wstring encryptMessage( std::wstring& message, const std::vector<int>& key) {
    wstring encryptedMessage;
    vector<wstring> EncryptedText;
    wstring column;
    rowCount = (message.length() + key.size() - 1) / key.size();
    
    for (int i = 0; i < key.size(); i++)
    {
        for (int j=0; j < message.size(); j++)
        {
            if (j * key.size()+i < message.size())
                column += message[j * key.size()+i];
            else
                break;
        }
        EncryptedText.push_back(column);
        column.clear();
    }
 
    // Проверка столбцов на равенcтво, при разных размерах, забить пробелами
    for (int i = 0; i < EncryptedText.size() - 1; i++)
    {
        if (EncryptedText[i].size() != EncryptedText[i + 1].size())
        {
            wchar_t space = *L" ";
            EncryptedText[i + 1].push_back(space);
        }

    }

    //Запись итого шифрованного сообщения в строку
    for (int i= 0; i < key.size(); i++)
    {
        encryptedMessage += EncryptedText[key[i]];
    }
    message = encryptedMessage;
    return encryptedMessage;
}
```  

## ХЭШ и файл HEAD

Хэш - hash (рубить, крошить) преобразование данных для получения отпечатка
гит преобразует коммит с помощью алгоритма SHA-1. Для каждого коммита генерируется уникальный хэш - результат хэширования.

свойства хэша:
- Если хэш получить из одного набора данных, результат будет гарантированно одинаковым.
- Если изменить хоть один символ во входных данных, то хэш изменится, причем разительно

GIT хранит таблицу  хэш->информация о коммите.  
хэш- идентификатор коммита.  
HEAD- это служебный файл в папке %название проекта%/.git , в котором хранится ссылка на файл, в котором хранится хэш последнего коммита

## СТАТУСЫ ФАЙЛОВ В РЕПОЗИТОРИИ:

**Untracked** - (неотслеживаемый), гит видит этот файл, но не отслеживает его изменения и не хранит его прошлые версии.  
**Staged** - (подготовленный), файл получает его после комманды git add %имя файла%. после этой комманды файл попадает в список файлов, что войдут в коммит.  
**staging area** - это зона, в которой хранятся файлы до коммита(но после git add).  
Также есть синонимы staging area as index or cache. Тогда staged as indexed or cached. Может использоваться в документации и на форумах.  
**Tracked** - (отслеживаемый) противоположность untracked. Этот статус получают файлы уже зафиксированные коммандой git commit, так и включенные в staging area коммандой git add.  
**Modified** - (Измененный), состояние означает, что гит сравнил текущий файл с сохраненной версией файла и нашел отличия.

## Оформление сообщений к коммитам

Вопросы, на которые должно отвечать сообщение:
- Что добавлено?
- Куда добавлено?
- Что изменено?
- как изменено?

Сообщения должны быть информативными, например "Кнопка выход покрашена в красный цвет". Тут есть конкретика Что изменено и как именно изменено.  
Ключ --oneline имеет ограничение на вывод первых 72-ух символов сообщения, поэтому часто на проектах стоит ограничение на 72 символа в сообщении к коммиту.

## СТИЛИ ОФОРМЛЕНИЯ

Они бывают разные, могут зависеть от доп программ на проекте и т.п. Например при работе с Jira часто пишут в сообщении на коммит "LGS-239: Дополнить список пасхалок новыми числами"  
в Github стиле пишут "Исправить #334, добавить график температуры"  
#334- связывает коммит и issue(список задач) в github`е и закрывает соответствующую задачу.  
conventional commits(соглашение о коммитах)
Предлагает формат сообщения:  
"<tуpe> : <сообщение>"  
Например "fix: устранить утечку памяти"  
Чаще всего сообщение начинается с глагола в форме инфинитива.

```mermaid
graph LR;
untracked -- "git add" --> "staged (в списке на коммит) + tracked";
"staged (в списке на коммит) + tracked" -- "git commit" --> tracked/commited;
"staged (в списке на коммит) + tracked" -- "Изменения" --> "Modified (измененный)";
"Modified (измененный)" -- "git add" --> "staged (в списке на коммит) + tracked";
tracked/commited --"Изменения"--> "Modified (измененный)";
```
[Ссылка на проект](https://github.com/Masslocalnik/project-to-share)  