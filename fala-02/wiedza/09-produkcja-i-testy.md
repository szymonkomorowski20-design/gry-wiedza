# Produkcja, testy i wydajność

**Zastosowanie:** utrzymanie działającego projektu i ograniczenie przypadkowych regresji.

Dziel pracę na małe zadania z mierzalnym wynikiem. „Poprawić walkę” jest niejasne; „wróg przestaje atakować po śmierci” da się sprawdzić. Oddziel listę pomysłów od zakresu obecnego wydania.

Zapisuj zmiany w kontroli wersji wraz z krótkim opisem celu. Nie przechowuj haseł ani kluczy usług w repozytorium. Zależności i wersję silnika zapisuj tak, żeby projekt dało się odtworzyć. Duże pliki binarne wymagają osobnego planu przechowywania; katalog linków nie wymaga pobrania każdej wielogigabajtowej paczki.

## Co testować

- Start gry, wejście do poziomu, przegraną i restart.
- Zapis oraz odczyt, w tym brak pliku zapisu.
- Zmianę rozdzielczości, urządzenia sterowania i ustawień dźwięku.
- Szybkie powtórzenie akcji, które powinno wykonać się tylko raz.
- Działanie eksportu poza edytorem.

Automatyzuj stabilne reguły, takie jak wynik łączenia kafelków lub warunek ukończenia zadania. Ocenę czytelności i odczuć z gry uzupełnij obserwacją graczy.

## Wydajność

Zacznij od pomiaru na docelowym sprzęcie. Sprawdź, czy problem dotyczy CPU, GPU, pamięci czy ładowania. Zmień jedną rzecz i porównaj tę samą scenę. Sam wzrost FPS na bardzo mocnym komputerze nie dowodzi poprawy w warunkach docelowych.

**Efekt pracy:** powtarzalna lista prób, raport błędu z krokami i zapis pomiaru przed/po. Materiały: [produkcja i testy](../katalog/12-produkcja-testy.md), [szablon raportu](../szablony/RAPORT-BLEDU.md).
