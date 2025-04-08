# Podstawy GUI w Pythonie: Tkinter i Kivy

Tworzenie graficznych interfejsów użytkownika (GUI) w Pythonie pozwala na budowanie aplikacji przyjaznych dla użytkownika. Zamiast komunikacji tekstowej (np. przez konsolę), użytkownicy mogą wchodzić w interakcję z programem za pomocą okien, przycisków, pól tekstowych i innych elementów interfejsu.
W tej instrukcji skupimy się na dwóch popularnych bibliotekach GUI w Pythonie:
- [Tkinter](https://docs.python.org/3/library/tkinter.html) – prosta i wbudowana biblioteka GUI, idealna do nauki i budowy podstawowych aplikacji desktopowych.
- [Kivy](https://kivy.org/doc/stable/) – biblioteka służąca do budowy aplikacji wieloplatformowych (np. na Androida, iOS), wspierająca również urządzenia dotykowe.

## Tkinter
Tkinter to standardowa biblioteka GUI do Pythona. Jest łatwa w użyciu i doskonała do nauki podstawowych pojęć GUI.
### Główne komponenty (widgety)
- Tk(): Główne okno aplikacji
- Label: Etykieta z tekstem
- Button: Przycisk
- Entry: Pole tekstowe jednowierszowe
- Text: Wielowierszowe pole tekstowe
- Frame: Kontener do organizacji innych widgetów
- Checkbutton: Przycisk wyboru (checkbox)
- Radiobutton: Przycisk opcji
- Listbox: Lista opcji do wyboru
- Canvas: Obszar do rysowania
- Menu: Pasek menu
- Scale: Suwak
- Spinbox: Pole wyboru wartości liczbowej
- Messagebox: Okna dialogowe z komunikatami

Układ komponentów:
- pack() – proste układanie elementów w pionie lub poziomie
- grid() – układ tabelaryczny
- place() – pozycjonowanie absolutne

Pniżej przedstawiono prosty przykład wykonania notatnika z wożliwością odczytu i zapisu plików
```Python
import tkinter as tk
from tkinter import filedialog

# Funkcja do zapisywania tekstu do pliku
def save_file():
    file = filedialog.asksaveasfilename(defaultextension=".txt")
    if file:
        with open(file, 'w') as f:
            f.write(text.get("1.0", tk.END))

# Funkcja do wczytywania tekstu z pliku
def load_file():
    file = filedialog.askopenfilename()
    if file:
        with open(file, 'r') as f:
            text.delete("1.0", tk.END)
            text.insert(tk.END, f.read())

# Tworzenie głównego okna aplikacji
root = tk.Tk()
root.title("Mini Notatnik")

# Pole tekstowe
text = tk.Text(root)
text.pack(expand=True, fill='both')

# Menu aplikacji
menu = tk.Menu(root)
root.config(menu=menu)
file_menu = tk.Menu(menu)
menu.add_cascade(label="Plik", menu=file_menu)
file_menu.add_command(label="Otwórz", command=load_file)
file_menu.add_command(label="Zapisz", command=save_file)

# Uruchomienie aplikacji
root.mainloop()
```
Kolejny przykłąd wykorzystujący pozycjonowanie w postaci siatki (grid) dotyczy prostego kalkulatora obliczającego pole prostokąta.
```Python
import tkinter as tk

def oblicz_pole():
    try:
        a = float(entry_a.get())
        b = float(entry_b.get())
        wynik_label.config(text=f"Pole: {a * b} m²")
    except ValueError:
        wynik_label.config(text="Błąd danych")

root = tk.Tk()
root.title("Kalkulator pola prostokąta")

# Pola wejściowe
tk.Label(root, text="Długość a (m):").grid(row=0, column=0)
entry_a = tk.Entry(root)
entry_a.grid(row=0, column=1)

tk.Label(root, text="Szerokość b (m):").grid(row=1, column=0)
entry_b = tk.Entry(root)
entry_b.grid(row=1, column=1)

# Przycisk i wynik
tk.Button(root, text="Oblicz", command=oblicz_pole).grid(row=2, columnspan=2)
wynik_label = tk.Label(root, text="")
wynik_label.grid(row=3, columnspan=2)

root.mainloop()
```



