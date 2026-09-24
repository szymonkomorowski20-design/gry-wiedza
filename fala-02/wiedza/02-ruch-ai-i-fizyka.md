# Ruch, AI i fizyka

**Zastosowanie:** sterowanie postacią, przeciwnicy, kolizje i wyszukiwanie drogi.

Wektor opisuje kierunek i wielkość przesunięcia. Przy prostym ruchu bez przyspieszenia przemieszczenie wynika z prędkości i czasu. W silniku korzystającym z fizyki przestrzegaj jego sposobu aktualizacji ciał, zamiast jednocześnie wymuszać pozycję i oczekiwać stabilnych kolizji.

Stały krok symulacji pomaga oddzielić obliczenia fizyki od liczby rysowanych klatek. Trzeba też ograniczyć nadrabianie zaległych kroków przy spadku wydajności. Wyjaśnienie i kompromisy: [Fix Your Timestep — Glenn Fiedler](https://gafferongames.com/post/fix_your_timestep/).

## Przeciwnik jako stany

Zacznij od trzech stanów: patrol, pościg, powrót. Dla każdego zapisz warunek wejścia i wyjścia. Gdy wróg traci cel, zdecyduj, czy idzie do ostatniej znanej pozycji, czy od razu wraca. To decyzja projektowa, której sama biblioteka AI nie podejmie.

## Wyszukiwanie drogi

Mapa dla algorytmu to graf miejsc i połączeń. BFS nadaje się do jednakowych kosztów przejść; Dijkstra uwzględnia różne koszty, a A* dodatkowo wykorzystuje oszacowanie odległości do celu. Znaleziona droga nie rozwiązuje jeszcze animacji ruchu, otwierania drzwi ani unikania dynamicznych przeszkód. Źródło: [Red Blob Games](https://www.redblobgames.com/pathfinding/a-star/introduction.html).

**Ćwiczenie:** plansza z przeszkodami i jednym przeciwnikiem. Sprawdź brak drogi, cel za ścianą i sytuację, gdy cel zmienia miejsce. Oddziel decyzję AI od ruchu postaci.

Więcej: [matematyka, AI i fizyka](../katalog/03-matematyka-ai-fizyka.md).
