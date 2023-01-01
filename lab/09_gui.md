# Lab 9
## Tworzenie interfejsów graficznych

### TKinter
TK Interface jest domyślnie zainstalowanym modułem pozwalającym nam na tworzenie interfejsów graficznych.

📖 Proszę przeczytać https://docs.python.org/3/library/tkinter.html.

#### Klasa Tk
Klasa ``Tk` pozwala nam zdefiniować nasze okno w sposób obiektowy.

```python
import tkinter as tk

class App(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title('Sample Python GUI Window')
        self.geometry('300x300')

if __name__ == "__main__":
    app = App()
    app.mainloop()  # wywołanie pętli obsługującej zdarzenia.
    
```        

✏️ Pomocny tutorial: https://realpython.com/python-gui-tkinter/

### Thread
Wątkiem w programowaniu nazywamy kod który wykonuje się równolegle względem innego kodu wykonywanego w naszym programie. Niestety (albo stety 🙂), Python symuluje wątki, co pozwala na wykonywanie ich w systemach jednoprocesorowych, jak i wieloprocesorowych bez zmiany kodu, co ma to też wpływ na obniżoną wydajność. 

📖 Proszę przeczytać https://pl.wikipedia.org/wiki/Global_Interpreter_Lock.

📖 Proszę przeczytać https://wazniak.mimuw.edu.pl/images/5/54/Sop_02_wyk_bw_1.1.pdf


w Pythonie moduł zajmujący się wysokopoziomową obsługą wątków nazywa się `threading`.

📖 Proszę przeczytać https://docs.python.org/3.9/library/threading.html

#### Tworzenie wątku
Nowy wątek można stworzyć na dwa sposoby: zdefiniowanie funkcji lub klasy która ma zostać uruchomiana. 

Na tych zajęciach omówimy drugi sposób, czyli z wykorzystaniem klasy `Thread`.

Przykład:
```python
from threading import Thread

class MinThread(Thread):
    def run(self):
      # Tutaj pojawia się nasz kod który chcemy wywołać.
      pass
      
if __name__ == "__main__":
    thread = minThread()
    thread.run()
    # coś tu brakuje ale to zaraz :)
```


Należy pamiętąć, że wątek który został uruchomiony działa niezależnie i zakończenie działania naszego głównego wątku (czyli naszego skryptu) nie powoduje automatycznego zakończenie wątku.

W tym celu musimy wywołać metodę `join()` klasy `Thread`. która poinformuje główny wątek aby "zaczekał" na zakończenie wykonywania wątku.  

Uzupełniony przykład:
```python
from threading import Thread

class MinThread(Thread):
    def run(self):
      # Tutaj pojawia się nasz kod który chcemy wywołać.
      pass
      
if __name__ == "__main__":
    thread = minThread()
    thread.run()
    print("Hello World")
    thread.join() # <--
```

✏️ Stwórz wątek który będzie odliczał do 30.

✏️ Zmodyfikuj uprzednio utworzony kod aby uruchomić dwa wątki jednocześnie.


### Zadania

✏️ Stwórz Skrypt które będzie uruchamiać dowolną (zdefiniowaną przez Ciebie) komendę/program.

✏️ Na podstawie uprzednio utworzonego skryptu, stwórz GUI które będzie posiadać przycisk wywołujący funkcję uruchamiającą dowolną komendę/program.

✏️ Stwórz GUI które będzie posiadać przycisk wykonujący zadanie w wątku (np. odliczający do 60 sekund z interwałem 1 sekunda). Wynik odliczania powinien wyświetlać się w okienku.
