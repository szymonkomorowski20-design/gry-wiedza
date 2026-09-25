# C++ — wybieraj rozwiązanie konkretnego problemu

Caerind gromadzi nie tylko silniki, ale również biblioteki językowe, matematykę, grafikę, fizykę, sieć i narzędzia. Większość z nich jest pojedynczym składnikiem programu. Lista „awesome” nie potwierdza zgodności ze swoim kompilatorem ani kompletności dokumentacji.

## Zanim dodasz zależność

Zapisz problem, docelowe platformy, używany standard C++ i ograniczenia projektu. Sprawdź licencję oraz to, czy biblioteka wymaga wyjątków, RTTI, konkretnego systemu budowania lub dodatkowych bibliotek. Uruchom najmniejszy przykład w osobnym projekcie i dopiero później integruj z grą. Nie wykonano tutaj kompilacji wszystkich pozycji katalogu.

## Kto posiada zasób

Dla każdego uchwytu określ właściciela i czas życia. Inna część programu może korzystać z obiektu, ale nie musi odpowiadać za jego usunięcie. Zasada RAII pozwala wiązać zwalnianie zasobu z końcem życia obiektu zarządzającego. Dotyczy to również plików, blokad czy uchwytów grafiki, nie tylko pamięci.

Szczególnie uważaj na dane przechowywane przez zewnętrzną bibliotekę po zakończeniu wywołania. Wskaźnik do lokalnego bufora może wtedy stracić ważność. Zapisz też, na którym wątku wolno tworzyć i usuwać zasób.

## Ćwiczenie

Porównaj dwie biblioteki do jednego zadania, np. parsowania konfiguracji. Dla obu przygotuj ten sam mały plik, błąd składni i brak wymaganej wartości. Oceń integrację, czytelność błędów oraz koszt utrzymania zamiast samej liczby funkcji. Wybór zapisz razem z konkretną wersją zależności.

[Biblioteki i architektura](../katalog/02-programowanie.md) · [Matematyka i fizyka](../katalog/03-matematyka-ai-fizyka.md).
