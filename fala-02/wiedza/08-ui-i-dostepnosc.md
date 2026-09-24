# UI, dostępność i języki

**Zastosowanie:** umożliwienie graczowi zrozumienia i obsługi gry.

Każdy ekran powinien mieć jasny cel, czytelny wybór i możliwość powrotu. Sprawdź stan przycisku przy wskazaniu, wybraniu, naciśnięciu i zablokowaniu. Menu obsługiwane myszą może potrzebować osobnej kontroli nawigacji z klawiatury lub pada.

Nie przekazuj ważnej informacji wyłącznie kolorem. Dodaj symbol, kształt lub tekst. Zapewnij czytelny kontrast, regulację głośności i możliwość zmiany sterowania tam, gdzie to możliwe. Podstawowe punkty do sprawdzenia: [Game Accessibility Guidelines](https://gameaccessibilityguidelines.com/basic/).

## Lokalizacja od początku

Przechowuj tekst pod stabilnym identyfikatorem, np. `menu.start`, zamiast wpisywać go w wielu skryptach. Przetestuj długie tłumaczenia, polskie znaki i różne rozmiary okna. Font musi zawierać potrzebne glify. Prawo do używania fontu w grze i prawo do publikowania jego pliku sprawdź w licencji konkretnej rodziny.

Ikony sterowania z Input Prompts pomagają pokazać przyciski, ale sama grafika nie wprowadza obsługi urządzenia. Wyświetlany symbol powinien odpowiadać aktualnemu przypisaniu działania.

**Ćwiczenie:** przygotuj ekran pauzy obsługiwany bez myszy, suwak audio, powrót do gry oraz komunikat o zapisaniu ustawień. Przetestuj dłuższe etykiety.

Zobacz [katalog UI i lokalizacji](../katalog/11-ui-lokalizacja.md) oraz paczki UI w obu falach.
