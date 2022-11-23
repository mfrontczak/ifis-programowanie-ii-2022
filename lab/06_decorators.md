# Lab 6

## Dekoratory klasy - Metody statyczne i klasowe (przypomnienie)

### Metoda statyczna
`@staticmethod` jest wbudowanym dekoratem który podmienia daną metodę. 
Metoda statyczna jest powiązana z klasą w której się znajduje i **nie posiada** dostępu do atrybutów klasy. 
Nie jest wymagane podawanie żadnych parametrów. 

```python
from datetime import datetime

class Data:
    def __init__(self, rok, miesiac, dzien):
        self.rok = rok
        self.miesiac = miesiac
        self.dzien = dzien
    
    @staticmethod
    def czy_dzisiejsza(rok, miesiac, dzien):
        dzis = datetime.now()
        return rok == dzis.year and miesiac == dzis.month and dzien == dzis.day


print(Data.czy_dzisiejsza(1997, 7, 18))  # sprawdzi czy podana data jest dzisiejsza.
```

### Metoda klasowa
`@classmethod` jest wbudowanym dekoratem który podmienia daną metodę. 
Metoda klasowa jest powiązana z klasą w której się znajduje i **posiada** dostęp do jej atrybutów.
Pierwszym parametrem w metodzie klasowej jest (musi być) `cls`, który odnosi się do klasy a nie instancji konkretnego obiektu. 

```python
from datetime import datetime

class Data:
    def __init__(self, rok, miesiac, dzien):
        self.rok = rok
        self.miesiac = miesiac
        self.dzien = dzien
    
    @classmethod
    def dzisiaj(cls):
        dzis = datetime.now()
        return cls(dzis.year, dzis.month, dzis.day)

d = Data.dzisiaj()  # Utworzy nową instancję obiektu z klasy Data z dzisiejszą datą.
```

✏️ Zapoznaj się z https://docs.python.org/3.9/library/dataclasses.html, utwórz przy pomocy dekorator `@dataclass` klasę Student z metodą `avg_grade`. klasa Student powinna posiadać atrybut `grades` typu `list` do przechowywania ocen.

# Dekoratory funkcji
```python
# funkcja power_of_2 przyjmie jako parametr inną funkcję
# a następnie wykorzysta ją wewnątrz funkcji _wrapper
# która wywoła przekazaną funkcję i zmodyfikuje jej wartość
def power_of_2(func):
    def _wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result**2
    return _wrapper


def just_a_number_plus_one(a):
    return a + 1

print(just_a_number_plus_one.__name__)

# tutaj dokonujemy "podmiany"
just_a_number_plus_one = power_of_2(just_a_number_plus_one)

print(just_a_number_plus_one.__name__)

print(just_a_number_plus_one(2))
```

Aby użyć funkcji jako dekorator należy użyć konstrukcji `@` + nazwa funkcji.

Przykład:
```python
def power_of_2(func):
    def _wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result**2
    return _wrapper

@power_of_2
def just_a_number_plus_one(a):
    return a + 1

print(just_a_number_plus_one.__name__)

print(just_a_number_plus_one(2))
```

Dektorator może również działać jak funkcja i przyjmować parametry.

Przykład:
```python
def multiply(by):
    def _wrapper(func):
        def _inner(*args, **kwargs):
            return func(*args, **kwargs) * by
        return _inner
    return _wrapper


@multiply(2)
def add_two_numbers(a, b):
    return a + b
    
    
@multiply(3)
def add_three_numbers(a, b, c):
    return a + b

print(add_two_numbers(3, 2)) 
print(add_three_numbers(1, 2, 3))
```

✏️ Zapoznaj się z https://docs.python.org/3/library/functools.html#functools.wraps, jakie są plusy wykorzystania tego dekoratora?

✏️ Napisz funkcję która przyjmuje jako parametr funkcję. Następnie niech funkcja wywoła przekazaną funkcję w argumencie i zwróci wynik jej działania. 

✏️ Stwórz dekorator który dla dowolnej funkcji będzie wyświetlał przed jej wywołaniem wartości argumentów jakie zostały do niej przekazane.

✏️ Napisz dekorator `register` który zapisze udekorowaną funkcję do listy, oraz zwróci tą funkcję spowrotem.
