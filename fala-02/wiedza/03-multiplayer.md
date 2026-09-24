# Multiplayer — zakres dodatkowej pracy

**Zastosowanie:** planowanie współdzielonego stanu gry.

Zanim wybierzesz bibliotekę sieciową, określ, kto zatwierdza wynik działania. Klient może wysyłać zamiar ruchu, a serwer obliczać rezultat. Samo przesłanie pozycji nie rozstrzyga, czy gracz miał prawo się tam znaleźć.

Rozdziel trzy pytania: jaki stan jest współdzielony, jak często go wysyłasz i jak przedstawiasz opóźnione dane. Interpolacja wygładza ruch między odebranymi stanami. Predykcja przewiduje efekt lokalnego wejścia, a korekta uzgadnia go z wynikiem serwera. Każde z tych rozwiązań zwiększa złożoność testów.

## Mały plan wdrożenia

1. Zacznij od dwóch klientów w jednej małej scenie.
2. Zsynchronizuj jedną interakcję, na przykład podniesienie przedmiotu.
3. Sprawdź równoczesne żądanie obu graczy: nagroda ma zostać przyznana tylko raz.
4. Dodaj obsługę rozłączenia i ponownego wejścia.
5. Testuj opóźnienia i utratę pakietów, zanim rozbudujesz świat.

W grze turowej często można przesyłać działania i aktualizacje stanu rzadziej niż w grze zręcznościowej. Determinizm wymaga świadomego kontrolowania kolejności aktualizacji, losowości i obliczeń; stały krok sam go nie gwarantuje.

**Efekt pracy:** spis komunikatów, właścicieli danych oraz test dwóch osób. Nie zaczynaj od budowy MMO jako sprawdzianu pierwszej mechaniki.

Punkty dalszej nauki z katalogów: [materiały sieciowe](../katalog/04-siec.md) i [Gaffer On Games](https://gafferongames.com/). To mapa zagadnień; nie przeprowadzono audytu każdej podlinkowanej implementacji sieciowej.
