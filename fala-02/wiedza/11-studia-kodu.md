# Jak uczyć się z pobranego kodu

[Trzy archiwa](../kod/README.md) zawierają oryginalne fragmenty projektów na MIT wraz z informacją o konkretnej wersji. Są materiałem do czytania i własnych eksperymentów; celowo nie zawierają wszystkich bibliotek i zasobów potrzebnych do uruchomienia.

## 2048 — stan i reguły gry

Zacznij od `js/game_manager.js`, potem przeczytaj `grid.js` i `tile.js`. Oddziel reprezentację planszy od przyjmowania klawiszy oraz wyświetlania wyniku. Narysuj przebieg jednego ruchu: od wejścia, przez przesuwanie i łączenie, po nowy kafelek oraz zapis stanu.

Ćwiczenie: ręcznie prześledź ruch w wierszu `[2, 2, 2, 0]`. Określ, dlaczego kafelek powstały z połączenia nie powinien łączyć się ponownie w tym samym ruchu. Potem zaprojektuj test dla ruchu, który nie zmienia planszy. Pominięto fonty, style i HTML; kompletna gra jest w repozytorium autora.

## ECS — dane osobno, zachowanie osobno

W `src/index.ts` biblioteki ecs-lib wyszukaj pojęcia świata, encji, komponentu i systemu. Encja reprezentuje obiekt, komponent opisuje jego dane, a system przetwarza wybrane obiekty. Czytaj przykłady README razem z kodem, zamiast wprowadzać ECS do każdej małej gry z góry.

Ćwiczenie: opisz pocisk przez pozycję, prędkość i czas życia. Zapisz, który system przesuwa pocisk, a który go usuwa. Sprawdź, czy kolejność aktualizacji wpływa na wynik. Zachowane testy są przykładami autora, nie potwierdzeniem, że zostały tutaj uruchomione.

## Dialogger — graf rozmowy i format danych

Czytaj `dialogger.js` oraz `app.js`, szukając tworzenia węzłów, połączeń i zapisu. README rozróżnia `.dl` — dane edytora — oraz `.dlz` — dane zoptymalizowane do użycia poza edytorem. To przykład oddzielenia narzędzia autora od danych odczytywanych przez grę.

Ćwiczenie: zaprojektuj rozmowę z wyborem, warunkiem posiadania przedmiotu i dwoma zakończeniami. Określ, co zapiszesz w pliku i jak gra rozpozna kolejny węzeł. Zewnętrzne biblioteki, w tym komponenty interfejsu, nie są w tym wyciągu. Pełny projekt wymaga własnych zależności i środowiska wskazanego przez autora.

## Zastosowanie do własnego projektu

Zapisz najpierw rozwiązany problem, następnie minimalny fragment wzorca, który jest ci potrzebny. Zachowaj licencję MIT i informacje autorów przy wykorzystaniu kodu. Nie kopiuj całej architektury bez zrozumienia jej założeń. [Źródła, wersje i lista plików](../kod/manifest.json).
