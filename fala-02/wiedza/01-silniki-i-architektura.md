# Silniki i architektura — co wybierasz

**Zastosowanie:** wybór fundamentu projektu i podział odpowiedzialności w kodzie.

Silnik organizuje sceny, zasoby, wejście gracza i wykonywanie gry. Biblioteka zwykle rozwiązuje węższy problem, na przykład rysowanie, fizykę albo obsługę okna. Edytor grafiki przygotowuje pliki, ale nie zastępuje logiki rozgrywki. W katalogach te rodzaje narzędzi bywają wymieszane.

Przed wyborem wykonaj małą próbę: załaduj grafikę, porusz obiektem, odtwórz dźwięk i wyeksportuj projekt. Zapisz wymagany język, docelową platformę i wersję narzędzia. To daje więcej informacji niż porównywanie liczby funkcji.

## Praktyczny podział projektu

- **Wejście:** przekształca klawisz lub przycisk w zamiar, np. „skocz”.
- **Reguły:** rozstrzygają, czy postać może skoczyć i jaki stan się zmieni.
- **Prezentacja:** odtwarza animację, dźwięk i informację na ekranie.
- **Zapis:** przechowuje dane potrzebne po ponownym uruchomieniu.

Stan, taki jak liczba punktów, powinien mieć jedno jasno wskazane miejsce przechowywania. Wyświetlacz punktów odczytuje zmianę; nie musi sam rozstrzygać, za co gracz je otrzymuje.

ECS opisuje obiekty przez komponenty danych, a zachowanie przez systemy. W pobranym `ecs-lib` znajdziesz świat, encje, komponenty i systemy. Warto po niego sięgnąć, kiedy chcesz prześledzić kompozycję obiektów. Nie jest obowiązkową architekturą każdej małej gry.

**Ćwiczenie:** zrób przedmiot, który dodaje punkt i znika. Następnie zmień jego grafikę bez zmiany reguły punktacji.

Materiały: [silniki](../katalog/01-silniki.md), [programowanie](../katalog/02-programowanie.md), [README ecs-lib](https://github.com/nidorx/ecs-lib). Starsze poradniki sprawdzaj względem wersji silnika; historyczne nazwy i cenniki w katalogu nie są aktualną rekomendacją zakupu.
