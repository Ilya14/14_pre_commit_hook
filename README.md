# 14_pre_commit_hook

## Описание

Перехватчик pre-commit для автоматического запуска тестов при попытке
сделать коммит. В случае неуспешного тестирования коммит не выполняется.

## Использование

Для использования git-перехватчика необходимо поместить файл
"pre-commit" в директорию .git/hooks. Перехватчик pre-commit будет
запускается автоматически при выполнении комманды git commit.

## Пример

Пример попытки выполнить коммит при неуспешном прохождении тестов:

```sh
$ git commit -m "Тестирование pre-commit"
.E..
======================================================================
ERROR: test_returns_none_for_complex_solution (__main__.QuadraticEquationTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/media/Ilya/ntfs/SVNWorkCopies/DevMan/14_pre_commit_hook/tests.py", line 22, in test_returns_none_for_complex_solution
    root1, root2 = get_roots(1, 2, 3)
  File "/media/Ilya/ntfs/SVNWorkCopies/DevMan/14_pre_commit_hook/quadratic_equation.py", line 6, in get_roots
    root1 = (-b - sqrt(discriminant)) / (2 * a)
ValueError: math domain error

----------------------------------------------------------------------
Ran 4 tests in 0.001s

FAILED (errors=1)
pre-commit# ERROR    [12/30/2016 04:04:45 PM] 
            Git commit is impossible because of testing errors.
            Pre-commit testing is complete with code: 1.
```

Пример попытки выполнить коммит при успешном прохождении тестов:

```sh
$ git commit -m "Добавлен pre-commit для выполнения тестов перед коммитом"
....
----------------------------------------------------------------------
Ran 4 tests in 0.000s

OK
pre-commit# INFO     [12/30/2016 04:21:30 PM] Pre-commit testing is complete with code: 0
[master f9f81d5] Добавлен pre-commit для выполнения тестов перед коммитом
 2 files changed, 47 insertions(+), 6 deletions(-)
 create mode 100644 pre-commit
```