# Игнорирование файлов

Зачастую, у вас имеется группа файлов, которые вы не только не хотите автоматически добавлять в репозиторий, но и видеть в списках неотслеживаемых. К таким файлам обычно относятся автоматически генерируемые файлы (различные логи, результаты сборки программ и т.п.). В таком случае, вы можете создать файл `.gitignore`. с перечислением шаблонов соответствующих таким файлам. Вот пример файла .gitignore:

>`$ cat .gitignore`
>
>`*.[oa]`
>
>`*~`

Первая строка предписывает Git игнорировать любые файлы заканчивающиеся на “.o” или “.a” — объектные и архивные файлы, которые могут появиться во время сборки кода. Вторая строка предписывает игнорировать все файлы заканчивающиеся на тильду (~), которая используется во многих текстовых редакторах, например Emacs, для обозначения временных файлов. Вы можете также включить каталоги log, tmp или pid; автоматически создаваемую документацию; и т.д. и т.п. Хорошая практика заключается в настройке файла .gitignore до того, как начать серьёзно работать, это защитит вас от случайного добавления в репозиторий файлов, которых вы там видеть не хотите.

К шаблонам в файле `.gitignore` применяются следующие правила:

Пустые строки, а также строки, начинающиеся с **#**, игнорируются.

Стандартные шаблоны являются глобальными и применяются рекурсивно для всего дерева каталогов.

Чтобы избежать рекурсии используйте символ слэш (**/**) в начале шаблона.

Чтобы исключить каталог добавьте слэш (**/**) в конец шаблона.

Можно инвертировать шаблон, использовав восклицательный знак (**!**) в качестве первого символа.

Glob-шаблоны представляют собой упрощённые регулярные выражения, используемые командными интерпретаторами. Символ (*) соответствует 0 или более символам; последовательность `[abc]` — любому символу из указанных в скобках (в данном примере a, b или c); знак вопроса (?) соответствует одному символу; и квадратные скобки, в которые заключены символы, разделённые дефисом (`[0-9]`), соответствуют любому символу из интервала (в данном случае от 0 до 9). Вы также можете использовать две звёздочки, чтобы указать на вложенные директории: `a/**/z` соответствует `a/z`, `a/b/z`, `a/b/c/z`, и так далее.

---

Вот ещё один пример файла .gitignore:

* Исключить все файлы с расширение `.a`^

>`*.a`

* Но отслеживать файл `lib.a` даже если он подпадает под исключение выше:

>`!lib.a`

* Исключить файл TODO в корневой директории, но не файл в `subdir/TODO`

>`/TODO`

* Игнорировать все файлы в директории `build/`

>`build/`

* Игнорировать файл doc/notes.txt, но не файл `doc/server/arch.txt`

>`doc/*.txt`

* Игнорировать все `.txt` файлы в директории `doc/`
> `doc/**/*.txt`