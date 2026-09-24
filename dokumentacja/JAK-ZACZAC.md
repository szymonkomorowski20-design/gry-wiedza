# Jak zacząć

## Prototyp gry 2D

1. Pobierz i rozpakuj Tiny Dungeon lub Tiny Town z folderu paczki.
2. Wybierz pojedyncze grafiki PNG albo arkusz kafelków i zaimportuj do swojego silnika.
3. Dla pixel art ustaw filtrowanie tekstur na najbliższego sąsiada (nearest/point). Wymiary siatki dopasuj do konkretnego arkusza.
4. Zbuduj małą mapę i dodaj postać z prostym ruchem oraz kolizjami.
5. Do menu wybierz UI Pack; do komunikatów i przycisków Interface Sounds.

## Prototyp gry 3D

1. Rozpakuj Mini Dungeon lub Nature Kit.
2. Wybierz format modelu obsługiwany przez Twój silnik spośród dostępnych w archiwum.
3. Zaimportuj jeden model wraz z jego teksturami i sprawdź skalę, materiały oraz orientację.
4. Dodaj kolizje i dopiero potem zbuduj większą scenę. Dostępność animacji sprawdzaj dla konkretnego modelu.

## Porządek w projekcie

Przechowuj importowane zasoby w folderach nazwanych według autora i paczki. Zachowaj pliki licencji. Nie importuj wszystkich formatów tego samego modelu, podglądów ani całej biblioteki, jeżeli gra ich nie używa.

Manifest `katalog/pobrane.json` pozwala sprawdzić integralność pobrań: obliczona suma SHA-256 archiwum powinna odpowiadać polu `sha256`. Liczba `archive_files` obejmuje wszystkie pliki w archiwum, w tym warianty formatów, dokumentację i podglądy; nie oznacza liczby unikalnych obiektów.
