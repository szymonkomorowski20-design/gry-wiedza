# Rejestr modeli ToxSam

Repozytorium ToxSam przechowuje katalog w plikach JSON. `projects.json` opisuje kolekcje, twórców i deklarowane licencje. Pliki `data/assets/*.json` opisują konkretne modele i podają adresy plików. To baza metadanych, nie zbiór wszystkich modeli umieszczonych lokalnie.

W tej fali zindeksowano 991 pozycji z 18 kolekcji. [Uproszczony rejestr](../zrodla/modele-3d.json) zachowuje nazwę, kolekcję, twórcę, format, adres, deklarację licencji i wersję źródła. Osobne wpisy w [dziale modeli](../katalog/06-modele-3d.md) ułatwiają wyszukiwanie. Same 991 modeli nie zostały pobrane.

## Jak wybierać plik

Najpierw znajdź kolekcję o odpowiednim stylu, potem sprawdź nazwę i format obiektu. Potwierdź licencję u autora pliku. CC0 dla metadanych rejestru i licencja konkretnego modelu są osobnymi informacjami, nawet gdy obie mają tę samą nazwę.

Adresy modeli w źródłowym rejestrze wskazują gałąź `main` innego repozytorium. Mogą więc zmieniać zawartość mimo przypiętej wersji samego katalogu. Przy faktycznym pobraniu trzeba zapisać datę, wersję repozytorium plików i sumę kontrolną modelu.

## Ćwiczenie

Znajdź model ławki lub rośliny. Zapisz, jak pasuje do skali i stylu twojej sceny, oraz czy wymaga uproszczenia, kolizji lub dodatkowych tekstur. Jeżeli importujesz glTF z plikami zewnętrznymi, zachowaj również wskazane bufory i obrazy. GLB może zawierać dane w jednym pliku, ale również wymaga sprawdzenia poprawności importu.

Nie traktuj liczby rekordów jako liczby gotowych, sprawdzonych zasobów produkcyjnych. To mapa do dalszego wyboru i weryfikacji.
