# Tekstury, shadery i efekty

**Zastosowanie:** nadanie powierzchniom wyglądu oraz przygotowanie efektów rozgrywki.

W paczce PBR kilka map opisuje różne cechy jednej powierzchni. Kolor odpowiada za barwę, normal map za pozorny kierunek powierzchni, roughness za charakter odbić, a displacement za wysokość używaną tylko przez obsługującą go konfigurację. Nie podłączaj wszystkich map do kanału koloru.

## Import pobranych materiałów ambientCG

1. Rozpakuj wybraną paczkę 1K-JPG.
2. Przejrzyj nazwy map i dokumentację używanego silnika.
3. Mapę koloru traktuj jako kolor; mapy danych skonfiguruj zgodnie z wymaganiami importera.
4. Wybierz właściwy wariant normal map, jeśli paczka udostępnia więcej niż jedną konwencję.
5. Sprawdź materiał na prostym obiekcie, pod neutralnym światłem, zanim użyjesz go w całej scenie.

Shader wykonuje obliczenia potrzebne do wyświetlenia obiektu lub obrazu. Zacznij od jednego efektu: zmiany koloru, przesunięcia UV albo maskowania. Potem dodaj parametr sterowany zdarzeniem w grze. [The Book of Shaders](https://thebookofshaders.com/) jest punktem wejścia do ćwiczeń z shaderami; konkretne przykłady wymagają dopasowania do silnika.

Efekt VFX powinien przekazywać informację: zasięg ataku, trafienie albo gotowość umiejętności. Porównuj czytelność efektu w prawdziwej scenie i mierz koszt. Duża liczba przezroczystych warstw może być problemem nawet wtedy, gdy geometria jest prosta.

**Ćwiczenie:** porównaj tę samą powierzchnię z samym kolorem i pełnym materiałem. Następnie zrób efekt trafienia z jednej tekstury cząsteczki.

Źródła do dalszej pracy: [tekstury, rendering i VFX](../katalog/07-tekstury-shadery.md).
