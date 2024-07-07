# ФАЙЛ С КОНСПЕКТАМИ ПО КУРСУ GIT ОТ ЯНДЕКСА

VCS- Version Control System (система контроля версий)
или синоним
SCM - Source Control Management ) система управления исходным кодом.

команды:
pwd - print working directory. Показывает текущую директорию.
cd - (Change Directory) для изменения папки в которой находишься. Например, cd folder перенесет из рабочей директории в папку folder
~ - обозначает родительскую директорию
.. - да, две точки. Это операция перехода на иерархию выше текущей директории
. - да, одна точка) обращение к текущей директории. нужно для запуска скриптов и программ, которые принимают папку в качестве параметра
ls - list directory content - показывает папки и файлы в текущей директории
-a - ключ (используется ls -a) показывает и скрытые папки тоже
touch - создает файл, синтаксис:
touch Имя_файла
можно через пробел несколько файлов создать
mkdir - создает директорию. синтаксис:
mkdir Название_директории.
-p - ключ, позволяющий создать целую ветку директорий, например:
mkdir -p dir1/dir2/dir3 создаст папки по такому пути
cp и mv - копировать и переместить. синтаксис одинаковый
Что_копируем/перемещаем Куда копируем/перемещаем
cat - concatinate and print )объединить и распечатать. РАБОТАЕТ ТОЛЬКО С ТЕКСТОВЫМИ ФАЙЛАМИ. открывает и печатает содержимое файла. синтаксис:
cat Имя_файла
rm - remove(удалить) удаляет файл.
Синтаксис: remove Имя_файла
rmdir - remove directory. удаляет папку.
ВАЖНО если папка не пуста, то её не удалит)
-r - ключ рекурсии. можно использовать для удаления папки вместе с файлами( в том числе и другими папками) внутри.
rm -r Имя_папки
&& - позволяет выполнять несколько комманд за раз
git add - подготовить файл к сохранению
--all -флаг для выбора всех файлов
git add . - для добавления всех файлов из текущей папки в репозиторий
