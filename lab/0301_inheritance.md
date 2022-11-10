# Lab 3 - cd.
## Dziedziczenie
### Polimorfizm
Polimorfizm jest niczym innym jak dziedziczeniem po więcej niż jednej klasie. 

```python
class Zwierze:
    def __init__(self, gatunek):
        self.gatunek = gatunek
 

class Latajace(Zwierze):
    def latam(self):
        print("Latam.")

class Plywajace(Zwierze):
    def plywam(self):
        print("Plywam.")

class Chodzace(Zwierze):
    def chodze(self):
        print("Chodze.")

class Dziobak(Plywajace, Chodzace):
    pass
    
class Kaczka(Plywajace, Chodzace, Latajace):
    pass
    
kaczka = Kaczka('Pospolita')
dziobak = Dziobak('Australijski') 

kaczka.plywam()
kaczka.chodze()
kaczka.latam()

dziobak.chodze()
dziobak.plywam()
```

⚠️ Bardzo ważna jest kolejność w jakiej klasa dziedziczy po innych klasach.

Przykład:
```python
class A:
    def method(self):
        print("Klasa A")

class B:
    def method(self):
        print("Klasa B")    
        
class C(A, B):
    pass
    
class D(B, A):
    pass
       
c = C()
c.method()

d = D()
d.method()
```

Wywoływana metoda jest wyszukiwana od lewej do prawej. Informacje o kolejności wyszukania metod są zawarte w specjalnej zmiennej klasowej `__mro__` (Method Resolution Order).

```python
print(C.__mro__) #
print(D.__mro__) # można też użyć D.mro() -> [__main__.D, __main__.B, __main__.A, object]
```
Wynik:

```
(<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)
(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
```

**Zadanie**

✏️ Stwórz klasę `Car`, a następnie utwórz trzy klasy `SUV`, `Sport`, `MiniVan` które będą dziedziczyć po klasie `Car`. Zdefiniuj odpowiednie atrybuty dla każdej z klas.

### Domieszki (MixIn)
Domieszka to bardzo uproszczona definicja klasy która skupia się na zdefiniowaniu metod pomocniczych. Sama w sobie nie posiada żadnych atrybutów a jedynie wykorzystuje do swojego działania atrybuty z klasy nadrzędnej.

Przykład:
```python
import json

class ToJsonMixin:
    def to_json(self):
        return json.dumps({'value': self.value})  # bardzo duże uproszczenie jak to powinno działać

class NumberValue(ToJsonMixin):
    def __init__(self, value):
        self.value = value

class StringValue(ToJsonMixin):
    def __init__(self, value):
        self.value = value
        
n = NumberValue(5)
s = StringValue('Hello World')

print(n.to_json())
print(s.to_json())

```

**Zadanie**

✏️ Napisz domieszkę `AddableMixin`, powinna ona udostępniać metodą pozwalającą na dodawanie dwóch obiektów do siebie.

✏️ Napisz domieszkę `FromJSONMixin`, powinna ona udostępniać metodą pozwalającą na wczytywanie wartości atrybutów z pliku JSON.

## Metody statyczne i klasowe

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

✏️ Napisz metodę klasy dla klasy `Data` zwracającą nowy obiekt z datą wczorajszą.

✏️ Napisz metodę statyczną dla klasy `Data` zmieniającą datę zapisaną w stringu w formacie USA "MM/DD/YYYY" na format europejski "DD/MM/YYYY". 
