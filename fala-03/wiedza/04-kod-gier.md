# Czytanie kodu gotowej gry

Listy leereilly i bobeff obejmują gry, porty, remake’i oraz projekty odtwarzające zachowanie starszych programów. Otwarte repozytorium nie oznacza, że zawiera całą grę z legalnie dostępną grafiką, muzyką i danymi poziomów. Licencję kodu i wymagane dane sprawdza się oddzielnie.

## Czytaj od jednej akcji

Wybierz małą czynność: ruch postaci, zebranie przedmiotu lub zmianę sceny. Znajdź wejście użytkownika, zmianę stanu i miejsce, w którym wynik staje się widoczny. Narysuj połączenia między tymi trzema etapami. Nie musisz najpierw poznać wszystkich plików dużej gry.

Potem sprawdź zapis danych. Czy stan rozgrywki jest oddzielony od obiektów wyświetlanych na ekranie? Kto tworzy przeciwnika, kto go aktualizuje, a kto usuwa? Jak projekt reaguje na brak zasobu lub niezgodny zapis gry?

## Remake to szczególny przypadek

Projekt może wymagać plików oryginalnej komercyjnej gry. Nie kopiuj takich danych do własnej biblioteki na podstawie samej licencji otwartego silnika. W tej fali pozostawiono odnośniki do kodu; nie pobrano ROM-ów ani komercyjnych danych gier.

## Ćwiczenie

Przeczytaj implementację jednej mechaniki i opisz jej wejścia, stan oraz wynik własnymi słowami. Zbuduj minimalny eksperyment z własnymi danymi. Jeżeli wykorzystujesz oryginalny kod, zachowaj jego licencję i wymagane informacje autorów. Zapisz dokładną wersję źródła, bo domyślna gałąź może się zmienić.

[Katalog kodu gier](../katalog/17-kod-gier.md). Podział na gatunki z oryginalnych list jest zachowany w polu `sources.section` pliku JSON.
