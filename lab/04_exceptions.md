# Lab 4
## Wyjątki
Wyjątkiem nazywamy często zdarzenie w wyniku którego nasz skrypt lub program nie działa prawidłowo. Kiedy skrypt zgłosi wyjątek interpreter przerwie jego wykonanie i poinformuje o błędzie użytkownika. Na szczęście w języku Python jak i wielu innych językach programowania istnieje mechanizm służący przechwytywaniu wyjątku przez programistę i obsługi tego zdarzenia.

W celu przechwycenia wyjątku w naszym skrypcie używamy konstrukcji `try` `except`.

Przykład 1: zwracający wyjątek:
```python
f = open('nie_istniejacy.txt')
```

Przykład 2: zwracający wyjątek:
```python
i = int('pietnaście')
```

Przykład 1: obsługujący wyjątek:
```python
try:
    f = open('nie_istniejacy.txt')
except:   # przechwytujemy wszystkie wyjątki.
    print("Podany plik nie istnieje lub nie masz uprawnień do odczytu.")
```

Przykład 2: obsługujący wyjątek:
```python
try:
    i = int('pietnaście')
except ValueError as err:
    print(err)
```

Oczywiście użycie konstrukcji `except` bez podania typu wyjątku który chcemy obsłużyć, będzie przechwytywać wszystkie możliwe wyjątki. W wypadku kiedy chcemy przechwycić konkretny wyjątek należy po `except` podać jego nazwę (jak w przykładzie 2). 

Konstrukcja `except ... as e` pozwala nam na uzyskanie dostępu do informacji o wyjątku zwróconym przez interpreter.

### Przechwytywanie wielu wyjątków
Python umożliwia nam zdefiniowanie w jednym wierszu `except` wielu wyjątków jakie chcemy obsłużyć.

Przykład:
```python
try:
    import foobar
    foobar.value
except (ModuleNotFoundError, ImportError) as e:
    # jakaś obsługa błędu ModuleNotFoundError lub ImportError
except (FileNotFoundError, IOError, OSError) as e:
    # jakaś obsługa błędu FileNotFoundError lub IOError lub OSError
```

📖 Proszę przeczytać https://docs.python.org/3.9/library/exceptions.html, aby dowiedzieć się więcej.

📖 Proszę przeczytać https://docs.python.org/3.9/library/exceptions.html#exception-hierarchy, aby dowiedzieć się więcej.

📖 Proszę przeczytać https://docs.python.org/3.9/tutorial/errors.html, aby dowiedzieć się więcej.

✏️ Z listy dostępnych wyjątków wybierz jeden a następnie użyj go wraz z składnią `raise` do wywołania wyjątku. Napisz skrypt który obsłuży wyjątek - w dowolny sposób.

✏️ Napisz skrypt który będzie odpytywał użytkownika o jego wiek, aż do momentu kiedy wprowadzi poprawne dane. (użyj pętli `while True`)
