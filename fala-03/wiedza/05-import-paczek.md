# Jak wykorzystać pobrane paczki

## KayKit — sceny 3D i postacie

Wybierz jedną paczkę pasującą do prototypu. Publiczne wersje zawierają modele, tekstury oraz pliki ułatwiające pracę w Godot; konkretne formaty różnią się między zestawami. Zachowaj układ katalogów, aby nie zerwać odwołań do materiałów. Dostępność plików OBJ, FBX czy glTF sprawdź w danym ZIP-ie, zamiast zakładać ten sam zestaw dla wszystkich paczek.

Rozpocznij od importu jednego obiektu. Oceń skalę względem postaci, kierunek osi, materiał, cienie i punkt obrotu. Modele z atlasem kolorów potrzebują właściwej tekstury; jednolity biały obiekt może oznaczać utracone przypisanie materiału. Dodaj kolizję odpowiednią do mechaniki, niekoniecznie identyczną z widoczną siatką. Dla animowanych postaci sprawdź szkielet oraz dostępne klipy.

## GDQuest — prosty prototyp 2D

Paczka zawiera SVG postaci, broni i elementów planszy. Ustal rozmiar rasteryzacji, punkt obrotu i sposób skalowania. Grafika ma pomagać sprawdzać zasady gry. Nie dołączono zewnętrznego fontu Montserrat ani całego starego motywu Godot, ponieważ wspólna deklaracja CC0 nie zastępuje odrębnej licencji fontu.

## bunnitech i CodinGame — sprite’y i plansze

Podwodne grafiki bunnitech są przezroczystymi PNG. Wybrane paczki CodinGame mają własne deklaracje CC0. Część plików może być atlasem zamiast pojedynczej postaci. Najpierw sprawdź wymiary oraz układ klatek; dopiero potem skonfiguruj wycinanie i animację w silniku.

## Próba integracji

Przygotuj małą scenę: podłoże, bohater, jeden obiekt interaktywny i ekran wyniku. Zapisz rozmiary, jednostki oraz ustawienia importu. Archiwa sprawdzono pod kątem integralności, lecz nie wykonano importu wszystkich paczek do silników.

[Lista paczek i zastosowania](../paczki/README.md) · [Manifest pobrań i licencje](../pobrane.json).
