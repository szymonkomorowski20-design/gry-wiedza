# Unity — integracja pakietów i przykładów

Listy StefanoCecere oraz insthync obejmują gotowe gry, narzędzia edytora, sterowanie postacią, UI, renderowanie i dodatkowe systemy. Kod z publicznego repozytorium nie musi być gotowym pakietem ani pasować do każdej wersji Unity.

## Mały projekt kontrolny

Przed importem zanotuj wersję edytora, używany system wejścia, renderer i platformę docelową. Sprawdź instrukcję autora oraz pliki zależności. W pustym projekcie zaimportuj jeden pakiet, otwórz przykład i wykonaj eksport. Dopiero po takim sprawdzeniu przenoś rozwiązanie do właściwej gry. To procedura do wykonania przez twórcę; w tej bibliotece nie uruchamiano edytora Unity.

## Ustal granice odpowiedzialności

Dwa kontrolery postaci nie powinny jednocześnie sterować tą samą pozycją. Dwa systemy wejścia mogą nadawać inne znaczenie tej samej akcji. Ustal, czy pobrany przykład dostarcza tylko algorytm, czy także własny interfejs, scenę i menedżer rozgrywki. Kopiuj minimalną potrzebną część z zachowaniem licencji.

W przypadku narzędzi edytora oddziel kod używany podczas tworzenia gry od kodu uruchamianego u gracza. Scena demonstracyjna może zawierać zasoby o innych warunkach niż sam kod pakietu.

## Ćwiczenie

Wybierz jeden pakiet, np. do lokalizacji lub sterowania kamerą. Przygotuj scenę, która używa jednej funkcji. Zapisz: wersję, konfigurację, trzy kroki odtworzenia i znane ograniczenia. Usuń pakiet i sprawdź, które części twojej gry były od niego zależne — to pomaga ocenić koszt późniejszej wymiany.

[Programowanie i pakiety](../katalog/02-programowanie.md) · [UI i języki](../katalog/11-ui-lokalizacja.md) · [Kod gier](../katalog/17-kod-gier.md).
