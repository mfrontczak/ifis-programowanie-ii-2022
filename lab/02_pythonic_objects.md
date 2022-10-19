# Lab 2

**Legenda**

📖 - proszę przeczytać

📝 - warte zapamiętania / zanotowania

⚠️ - zwróć uwagę

✏️ - zadanie do wykonania

🔍 - poszukaj w internecie

### Zadanie
Stwórz skrypt do obsługi Banku.

Skrypt powinien implementować następujące klasy:

* `Bank` - do przechowywania informacji o kontach bankowych (klasa Account), oraz nazwy banku.
* `Account` - do przechowywania informacji o użytkowniku konta np. imię i nazwisko, numer konta bankowego (powinien być unikalny), oraz saldo.
* `WireTransfer` - do przechowywania informacji o przelewach np. identyfikator porządkowy dla całego banku, z jakiego numeru konta, na jaki numer konta i kwota na jaką został dokonany przelew.

**Przykład do użycia:**

Zaimplementuj:

* Klasa `Bank` powinna implementować metodę `deposit` która będzie wyliczać sumę wszystkich depozytów jakie znajdują się na kontach klientów.
* Klasa `Account` powinna posiadać historię przelewów z/na konto.
* Klasa `Account` powinna implementować metodę `verify_balance` która sprawdzi czy kwota na koncie zgadza się z sumą przelewów z/na konta.

⚠️ Klasy mogą potrzebować jeszcze dodatkowych atrybutów i funkcji - zastanów się jakie.

## Obiekt
Obiekt jest abstrakcyjną strukturą danych, która posiada swój unikalny ID, typ oraz wartość. Typ obiektu jest określany dynamicznie na podstawie tego jakie metody udostępnia, technika ta jest nazywana 📖 [duck typing](https://pl.wikipedia.org/wiki/Duck_typing). Dzięki tej technice można ograniczyć wykorzystanie techniki dziedziczenia, gdyż obiekty wykorzystują odpowiednie specjalne metody do budowania zależności między nimi. 

Przykład:
```python
class Dog:
    def make_noice(self):
        print("Making dog noices.")
    
class Cat:
    def make_noice(self):
        print("Making cat noices.")
        

def make_noice(obj):
    obj.make_noice()
    
d = Dog()
c = Cat()

make_noice(d)
make_noice(c)
```

### Zadanie

✏️ Napisz skrypt w którym różne dwie klasy będą definiowały wspólny interfejs, stwórz listę różnych obiektów a następnie przeinteruj po niej i wywołaj odpowiednią metodę. 

📖 Proszę przeczytać https://docs.python.org/3.9/reference/datamodel.html aby dowiedzieć się więcej.

## Magiczne Metody
Metody specjalne potocznie nazywane "magicznymi metodami", są te metody klasy dzięki którym określamy jej (typ) oraz relacje z innymi obiektami.

Wybrane magiczne metody:
* `__init__` - metoda wykorzystywana jako konstruktor obiektu, w niej podajemy parametry dla nowej instancji klasy.
* `__new__` - metoda tworząca nową instancję klasy, wykorzysytwana wraz z wzorcem projektowym [Singleton](https://pl.wikipedia.org/wiki/Singleton_(wzorzec_projektowy)). 
* `__str__` - metoda wywoływana przez wbudowaną funkcję `str`, `print` lub `format`.
* `__repr__` - metoda wywoływana przez wbudowaną funkcję `repr`, zwraca oficjalny string reprezentujący obiekt.
* `__eq__` - metoda wywoływana w trakcie porównania obiektów przez operator `==`.
* `__ne__` - metoda wywoływana w trakcie porównania obiektów przez operator `!=`.
* `__lt__` - metoda wywoływana w trakcie porównania obiektów przez operator `<`.
* `__gt__` - metoda wywoływana w trakcie porównania obiektów przez operator `>`.
* `__len__` - metoda wywołowana przez wbudowaną funkcję `len`.
* `__iter__` - metoda wywoływana przez wbudowaną funkcję `iter` lub pętlę `for`.
* `__next__` - metoda wywoływana przez wbudowaną funkcję `next`.
* `__add__` - metoda wywoływana w trakcie wywołania operatora `+` na obiektach. 
* `__getitem__` - metoda wywoływana w trakcie wywołania `obiekt[klucz]`.
* `__slots__` - specjalna zmienna wykorzystywana do określenia atrybutów i metod. jakie klasa udostępnia. 

### Zadanie

✏️ Napisz skrypt w którym zaimplementujesz klasę odpowiadającą pionką na szachownicy. Pionki powinno dać się posortować względem ich wagi.

✏️ Stwórz klasę Animal z atrybutem name i size. 
   1. Wywołanie metody `sorted` na liście obiektów klasy Animal powinna zwrócić posortowaną listę względem rozmiaru.
   2. Reprezentacja tekstowa obiektu powinna zwracać <Animal: imię>.

✏️ Stwórz klasę CardDeck i Card. 
   1. Dodawanie nowych kart do tali kart powinien odbywać się przy pomocy operatora '+'.
   2. Wywołanie pętli na obiekcie CardDeck, powinien zwrócić karty znajdujące się w nim.
   3. Wywołanie CardDeck\[symbol karty\] powinien zwrócić obiekt klasy Card znajdujądej się w CardDeck.
   4. Klasa Card powinna implementować przyjazną dla użytkownika reprezentację tekstową karty.

