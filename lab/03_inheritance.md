# Lab 3

## Klasy (przypomnienie)

Klasa to zdefiniowany zbiór atrybutów i metod . Nowy obiekt stworzony z danej klasy nazywamy **instancją**. Interakcja z pozostałymi obiektami odbywa się przez wcześniej zdefiniowane metody.

#### minimalna definicja klasy
Aby zdefiniować klasę należy użyć słowa kluczowego `class`, dowolną nazwę (najlepiej zaczynającą się z dużej litery) oraz dwukropek.
```python
class NazwaKlasy:
    pass
```

Słowo kluczowe `pass` odgrywa tutaj kluczową rolę, w Pythonie nie ma możliwości pozostawienia pustej definicji klasy/funkcji oraz bloku instrukcji sterowania.

#### Tworzenie instacji z klasy

Przykład:
```python
# Definicja klasy
class Backpack:
    pass
    
arnolds_backpack = Backpack()  # nowa instancja przypisana do zmiennej arnolds_backpack
jimmys_backpack = Backpack()  # kolejna instancja tym razem przypisana do zmiennej jimmys_backpack
```

#### Atrybuty
Atrybutami nazywamy zmienne zdefiniowane w klasie.

Przykład 1:
```python
class Backpack:
    color = None

arnolds_backpack = Backpack()
arnolds_backpack.color = 'Blue'

jimmys_backpack = Backpack()
jimmys_backpack.color = 'Orange'

print(f"Kolor plecaka Jimmiego to {jimmys_backpack.color}")
print(f"Kolor plecaka Arnolda to {arnolds_backpack.color}")
```

Przykład 2:
```python
class Notebook:
    paper_size = 'b4'  # atrybut dostępny dla wszystkich instancji klasy Notebook z domyślną wartością. 
    
    def __init__(self, subject):
        self.subject = subject

arnolds_notebook = Notebook('Matematyka')
jimmys_notebook = Notebook('Fizyka')

print(f"Zeszyt Arnolda formatu {arnolds_notebook.paper_size} służy mu do przedmiotu {arnolds_notebook.subject}")
print(f"Zeszyt Jimmiego formatu {jimmys_notebook.paper_size} służy mu do przedmiotu {jimmys_notebook.subject}")
```

Przykład 3:

Modyfikacja atrybutu `paper_size` ma wpływ tylko na konkretną instancję.
```python
class Notebook:
    paper_size = 'B4'  # atrybut dostępny dla wszystkich instancji klasy Notebook z domyślną wartością. 
    
    def __init__(self, subject):
        self.subject = subject

arnolds_notebook = Notebook('Matematyka')
arnolds_notebook.paper_size = 'A5'

jimmys_notebook = Notebook('Fizyka')

print(f"Zeszyt Arnolda formatu {arnolds_notebook.paper_size} służy mu do przedmiotu {arnolds_notebook.subject}")
print(f"Zeszyt Jimmiego formatu {jimmys_notebook.paper_size} służy mu do przedmiotu {jimmys_notebook.subject}")
```


**Zadanie**

✏️ Napisz klasę `Student` z atrybutami `imie`, `nazwisko`, `nr_albumu`, `rok`.
✏️ Utwórz listę studentów i wyświetl na ekranie informacje o nich.

### Badanie typu obiektu
Do sprawdzenia czy dany obiekt jest powiązany z klasą używamy wbudowanej funkcji `isinstance(object, classinfo)`.
https://docs.python.org/3/library/functions.html#isinstance

## Dziedziczenie
Dziedziczenie jest ważnym elementem programowania obiektowego, pozwalające nam na definiowanie klasy która dziedziczy po klasie bazowej jej atrybuty i metody.

Przykład:
```python
class Zwierze:
    def __init__(self, gatunek):
        self.gatunek = gatunek
 

class Ptak(Zwierze):
    def latam(self):
        print("Latam.")


class Ryba(Zwierze):
    def plywam(self):
        print("Plywam.")


sowa = Ptak('Sowa')
rekin = Ryba('Rekin Młot')

print(sowa.gatunek) 
print(rekin.gatunek) 
```

Ważnym elementem programowania zorientowanego obiektowo w Pythonie jest funkcja `super()`. 
Użycie tej funkcji wewnątrz metody daje nam dostęp do właściwości klasy nadrzędnej (rodzica).

Przykład:
```python
class FreeUser:
    def __init__(self, username, is_paid=False):
        self.username = username
        self.is_paid = is_paid
        
    def isPaid(self):
        if self.is_paid:
            print(f"Użytkownik {self.username} ma płatny dostęp.")
        else:
            print(f"Użytkownik {self.username} ma darmowy dostęp.")
            
    def doFreeStuff(self):
        print("Do free stuff for free.")


class PaidUser(FreeUser):
    def __init__(self, username, tier, is_paid):
        super().__init__(username, is_paid)   # wywołanie metody __init__ z klasy bazowej FreeUser
        self.tier = tier
        
    def doPaidStuff(self):
        if self.tier == 'hobbyist':
            print("Do paid stuff for hobbyist.")
        elif self.tier == 'professional':
            print("Do paid stuff for professionals.")
        elif self.tier == 'corporate':
            print("Do paid stuff for corporate.")
            

arnold = PaidUser('arnold', 'hobbyist', True)

arnold.doPaidStuff()
```

Przykład z sprawdzeniem typu obiektu:
```python
arnold = PaidUser('arnold', 'hobbyist', True)

if isinstance(arnold, PaidUser):
    print("Zmienna arnold jest typu PaidUser")

if isinstance(arnold, FreeUser):
    print("Zmienna arnold jest typu FreeUser")

john = FreeUser('john', False)
    
if isinstance(john, PaidUser):
    print("Zmienna john jest typu PaidUser")

if isinstance(john, FreeUser):
    print("Zmienna john jest typu FreeUser")   
```

**Zadanie**

✏️ Napisz klasę `Student` oraz klasę dziedziczącą po niej `GraduatedStudent`. Nadaj im odpowiednie atrybuty.

