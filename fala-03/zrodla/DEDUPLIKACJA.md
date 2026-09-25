# Jak pominięto powtórki

Porównanie obejmuje katalog pierwszej fali, katalog i indeks wiki drugiej fali oraz wcześniejsze manifesty pobrań. Nie usuwano starych plików z repozytorium.

## Adresy

Przed porównaniem ujednolicono HTTP/HTTPS, prefiks `www`, końcowy ukośnik, wielkość liter hosta oraz nazw właściciela i repozytorium na GitHubie. Usunięto parametry śledzące `utm_*`, `fbclid`, `gclid`, końcówkę `.git` i kotwicę `#readme`. Zachowano pozostałe parametry oraz kotwice, bo mogą wskazywać różne materiały. Zapisano także oryginalny URL.

Każdy nowy adres występuje w głównym katalogu trzeciej fali tylko raz. Dalsze wystąpienia są przypisane jako dodatkowe źródła. Wpisy obecne w starszych falach pominięto; ich ślady znajdują się wyłącznie w [rejestrze porównania](pominiete-powtorki.json).

Ujednolicenie HTTP/HTTPS i `www` jest regułą porządkowania, nie wynikiem sprawdzenia przekierowań każdego serwera. Nie łączono automatycznie różnych domen, forków ani podstron o podobnym tytule. Nie gwarantuje to wykrycia wszystkich semantycznych powtórek, np. tego samego filmu pod dwoma adresami.

## Dokumenty i podwójne źródła

Mu-L podano w zleceniu dwukrotnie — pobrano go raz. Identyczne dokumenty pomiędzy repozytoriami rozpoznano po SHA-256 i przetworzono raz. [Raport identycznych dokumentów](identyczne-dokumenty.json) zachowuje powiązanie z drugim źródłem. Pobrane wersje Mu-L i TMHSDigital miały wiele identycznych plików. Repozytoria źródłowe pozostają odnotowane w manifeście.

## Paczki

Porównano hashe zawartości zasobów w nowych ZIP-ach z wcześniejszymi ZIP-ami, a nie tylko nazwy archiwów. Nie dostarczono ponownie paczki o takim samym zestawie plików zasobów. Wynik jest w [raporcie kontroli](../kontrola.json).

W różnych paczkach mogą występować wspólne tekstury, ikony lub pliki licencji. Zachowano je tam, gdzie stanowią część paczki i mogą być potrzebne do poprawnego importu. To nie jest kolejna kopia całej paczki.
