# Źródła, zakres analizy i prawa autorów

Stan opracowania: 24 września 2026. Dokładne identyfikatory wersji oraz liczby plików znajdują się w [manifeście](manifest.json).

| Źródło | Co wnosi do biblioteki | Sposób wykorzystania |
|---|---|---|
| [Pndy/gamedev-list](https://github.com/Pndy/gamedev-list) | Szczegółowy podział warsztatu twórcy: edytory, sterowanie, grafika, audio, produkcja i publikacja | Nazwy, odnośniki, sekcje; własne opisy zastosowań. Brak jawnego LICENSE w pobranej wersji |
| [Kavex/GameDev-Resources](https://github.com/Kavex/GameDev-Resources) | Silniki, kod gier, biblioteki i narzędzia z historycznymi oznaczeniami kosztów | Nazwy, odnośniki, sekcje i oznaczenia; własne opisy. Brak jawnego LICENSE w pobranej wersji |
| [mbrukman/awesome-gamedev](https://github.com/mbrukman/awesome-gamedev) | Wolne oprogramowanie i kultura; rozróżnienie licencji kodu oraz assetów | README i opracowanie katalogu na CC BY-SA 4.0; zachowano [licencję](../licencje/mbrukman-LICENSE.txt) |
| [sangohan/The-Gamedev-Resource-Mega-List](https://github.com/sangohan/The-Gamedev-Resource-Mega-List) | Nauka programowania, tech artu, projektowania i budowa portfolio | MIT; kuratorka wymieniona w README: Hazel Kennedy, informacja copyright: notpresident35. Zachowano [licencję](../licencje/sangohan-LICENSE.txt) |
| [FronkonGames/Awesome-Gamedev](https://github.com/FronkonGames/Awesome-Gamedev) | Materiały o produkcji, silnikach, projektowaniu, marketingu i analizach ukończonych gier | MIT, Fronkon Games; zachowano [licencję](../licencje/fronkon-LICENSE.txt) |

Kavex wskazuje także pierwotnych współtwórców listy `ellisonleao/magictools` w swoim CONTRIBUTING.md. Pełne informacje o autorach pozostają dostępne w repozytoriach źródłowych i historii Git.

## Co zostało przeanalizowane

Zinwentaryzowano wszystkie pliki śledzone przez Git w pięciu bieżących wersjach. Przetworzono całe README, ich nagłówki, listy, tabele, przypisy i adresy. Przejrzano dodatkowe teksty, licencje i pliki konfiguracyjne. Grafiki promocyjne nie zawierają materiału szkoleniowego i nie są składnikiem katalogu.

To opracowanie zawartości repozytoriów, a nie pełnych treści wszystkich stron, książek, kursów i filmów, do których odsyłają. Nie pobrano historii wszystkich commitów, issues ani zewnętrznych zasobów każdego serwisu. Nie deklarujemy trwałego „nauczenia” modelu — wiedza utrwalona jest w tych plikach.

Każdy wpis wskazuje konkretny commit i linię źródła. `source_description` zachowuje opisy tylko z trzech jawnie licencjonowanych list. `purpose_pl` to opis zastosowania wynikający z tematu i nazwy, a nie recenzja otwartej strony docelowej. Klasyfikacja została wykonana regułami i może wymagać korekty dla wieloznacznych tytułów.

## Pliki towarzyszące i wyjątki

- Skrypty Pndy `generator.py` i `mixer.py` generują i scalają katalog z plików JSON, których repozytorium nie zawiera. Nie są silnikiem gry ani dodatkową bazą do pobrania.
- CONTRIBUTING i konfiguracje kontroli linków opisują utrzymanie list, a nie tworzenie gier. Nie przeniesiono ich jako instrukcji dla tej biblioteki.
- `wall-of-shame.md` u mbrukmana zawiera historyczne oceny wolności projektów. Wskazuje GFDL, podczas gdy LICENSE.md zawiera CC BY-SA 4.0. Z powodu tej niespójności nie kopiowano tego pliku ani nie przyjęto dawnych ocen jako aktualnych faktów; [oryginał](https://github.com/mbrukman/awesome-gamedev/blob/a94bf4e18b511a93ae5bd574764b411e721850ae/wall-of-shame.md).
- Oznaczenia cen Kavex są danymi historycznymi. Nie są potwierdzeniem dzisiejszej ceny ani możliwości redystrybucji.
- Niejasne kopie komercyjnych książek oznaczono `rights_unclear_do_not_download`. Zapisanie odnośnika ze źródła nie jest potwierdzeniem legalności publikacji pliku.

## Licencja opracowania

Opracowanie katalogu w `katalog/` oraz autorskie notatki w `wiedza/` i szablony w `szablony/` udostępniono na **CC BY-SA 4.0**, z zachowaniem oznaczeń i praw źródeł. Zmiany względem list: połączenie, podział tematyczny, polskie objaśnienia, metadane pochodzenia i statusu pobrania. Pełny tekst CC BY-SA 4.0 jest w [pliku licencji](../licencje/mbrukman-LICENSE.txt).

Prawa do samych narzędzi, książek, filmów i paczek wynikają wyłącznie z ich własnych licencji. MIT/CC BY-SA listy odnośników nie nadaje takiej licencji stronie, do której ona odsyła.

Zachowane README w podfolderach stanowią kopie referencyjne. Ich odnośniki względne i ilustracje mogą wskazywać strukturę oryginalnego repozytorium; do nawigacji używaj naszego katalogu lub źródła online.
