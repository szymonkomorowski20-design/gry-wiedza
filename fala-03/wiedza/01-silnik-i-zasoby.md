# Architektura silnika i obieg zasobów

Listy stevinz i bobeff rozdzielają silniki, biblioteki i rozwiązania poszczególnych problemów. Silnik z edytorem scen ma szerszy zakres niż biblioteka renderująca: musi zarządzać obiektami, zasobami, zapisem scen, narzędziami autora i wersją uruchamianą przez gracza.

## Minimalny podział

Oddziel warstwę platformy — okno, wejście, pliki i zegar — od reguł gry. Renderer otrzymuje dane do narysowania, a nie decyduje o punktach życia. System zasobów odpowiada za odnalezienie pliku, odczyt, przetworzenie i zwolnienie danych. Edytor może używać tych samych danych sceny co gra, lecz powinien dodawać własne narzędzia wyboru, cofania i diagnostyki.

## Import nie jest ładowaniem

Plik autora, np. duży model lub ilustracja, nie zawsze jest najlepszym formatem dystrybucyjnym. Import może wytwarzać atlas, skompresowaną teksturę albo uproszczoną siatkę. Zachowaj źródło oraz ustawienia importu, aby wynik dało się odtworzyć. Zapisz zależności: model może odsyłać do materiału, a materiał do tekstury. Zmiana jednego pliku powinna wskazywać, które wyniki należy ponownie przygotować.

## Pierwszy eksperyment

Zbuduj scenę z jednym modelem, materiałem i światłem. Zmień teksturę oraz ponownie załaduj scenę. Następnie usuń teksturę i sprawdź, czy błąd wskazuje konkretny brakujący zasób. Dopiero po działającym przepływie dodawaj edytor, skrypty lub wielowątkowość.

Do dalszego wyboru: [silniki](../katalog/01-silniki.md), [programowanie](../katalog/02-programowanie.md) i [rendering](../katalog/07-tekstury-shadery.md). Materiały z `ARCHIVE.md` stevinz zachowują to oznaczenie w metadanych; mogą dotyczyć starszych lub nieutrzymywanych rozwiązań.
