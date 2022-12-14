# Lab 2

**Legenda**

馃摉 - prosz臋 przeczyta膰

馃摑 - warte zapami臋tania / zanotowania

鈿狅笍 - zwr贸膰 uwag臋

鉁忥笍 - zadanie do wykonania

馃攳 - poszukaj w internecie

## Obiekt
Obiekt jest abstrakcyjn膮 struktur膮 danych, kt贸ra posiada sw贸j unikalny ID, typ oraz warto艣膰. Typ obiektu jest okre艣lany dynamicznie na podstawie tego jakie metody udost臋pnia, technika ta jest nazywana 馃摉 [duck typing](https://pl.wikipedia.org/wiki/Duck_typing). Dzi臋ki tej technice mo偶na ograniczy膰 wykorzystanie techniki dziedziczenia, gdy偶 obiekty wykorzystuj膮 odpowiednie specjalne metody do budowania zale偶no艣ci mi臋dzy nimi. 

Przyk艂ad:
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

鉁忥笍 Napisz skrypt w kt贸rym r贸偶ne dwie klasy b臋d膮 definiowa艂y wsp贸lny interfejs, stw贸rz list臋 r贸偶nych obiekt贸w a nast臋pnie przeinteruj po niej i wywo艂aj odpowiedni膮 metod臋. 

馃摉 Prosz臋 przeczyta膰 https://docs.python.org/3.9/reference/datamodel.html aby dowiedzie膰 si臋 wi臋cej.

## Magiczne Metody
Metody specjalne potocznie nazywane "magicznymi metodami", s膮 te metody klasy dzi臋ki kt贸rym okre艣lamy jej (typ) oraz relacje z innymi obiektami.

Wybrane magiczne metody:
* `__init__` - metoda wykorzystywana jako konstruktor obiektu, w niej podajemy parametry dla nowej instancji klasy.
* `__new__` - metoda tworz膮ca now膮 instancj臋 klasy, wykorzysytwana wraz z wzorcem projektowym [Singleton](https://pl.wikipedia.org/wiki/Singleton_(wzorzec_projektowy)). 
* `__str__` - metoda wywo艂ywana przez wbudowan膮 funkcj臋 `str`, `print` lub `format`.
* `__repr__` - metoda wywo艂ywana przez wbudowan膮 funkcj臋 `repr`, zwraca oficjalny string reprezentuj膮cy obiekt.
* `__eq__` - metoda wywo艂ywana w trakcie por贸wnania obiekt贸w przez operator `==`.
* `__ne__` - metoda wywo艂ywana w trakcie por贸wnania obiekt贸w przez operator `!=`.
* `__lt__` - metoda wywo艂ywana w trakcie por贸wnania obiekt贸w przez operator `<`.
* `__gt__` - metoda wywo艂ywana w trakcie por贸wnania obiekt贸w przez operator `>`.
* `__len__` - metoda wywo艂owana przez wbudowan膮 funkcj臋 `len`.
* `__iter__` - metoda wywo艂ywana przez wbudowan膮 funkcj臋 `iter` lub p臋tl臋 `for`.
* `__next__` - metoda wywo艂ywana przez wbudowan膮 funkcj臋 `next`.
* `__add__` - metoda wywo艂ywana w trakcie wywo艂ania operatora `+` na obiektach. 
* `__getitem__` - metoda wywo艂ywana w trakcie wywo艂ania `obiekt[klucz]`.
* `__slots__` - specjalna zmienna wykorzystywana do okre艣lenia atrybut贸w i metod. jakie klasa udost臋pnia. 

### Zadanie

鉁忥笍 Napisz skrypt w kt贸rym zaimplementujesz klas臋 odpowiadaj膮c膮 pionk膮 na szachownicy. Pionki powinno da膰 si臋 posortowa膰 wzgl臋dem ich wagi.

鉁忥笍 Stw贸rz klas臋 Animal z atrybutem name i size. 
   1. Wywo艂anie metody `sorted` na li艣cie obiekt贸w klasy Animal powinna zwr贸ci膰 posortowan膮 list臋 wzgl臋dem rozmiaru.
   2. Reprezentacja tekstowa obiektu powinna zwraca膰 <Animal: imi臋>.

鉁忥笍 Stw贸rz klas臋 CardDeck i Card. 
   1. Dodawanie nowych kart do tali kart powinien odbywa膰 si臋 przy pomocy operatora '+'.
   2. Wywo艂anie p臋tli na obiekcie CardDeck, powinien zwr贸ci膰 karty znajduj膮ce si臋 w nim.
   3. Wywo艂anie CardDeck\[symbol karty\] powinien zwr贸ci膰 obiekt klasy Card znajduj膮dej si臋 w CardDeck.
   4. Klasa Card powinna implementowa膰 przyjazn膮 dla u偶ytkownika reprezentacj臋 tekstow膮 karty.

