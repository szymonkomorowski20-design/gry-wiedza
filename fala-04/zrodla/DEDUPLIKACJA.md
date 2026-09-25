# Jak pominięto powtórki (fala 04)

## Adresy

Falę porównano z katalogiem fali 01, katalogami i indeksem wiki fali 02, katalogiem fali 03, rejestrem `linki-osobno.jsonl` z BAZA-AI oraz ze **wszystkimi adresami wymienionymi w plikach Markdown i JSON fal 01–03**, w sumie z 20 218 znormalizowanymi adresami. Normalizacja jest taka sama jak w fali 03: HTTPS, bez `www`, bez końcowego ukośnika, małe litery hosta i nazw repozytoriów GitHuba, bez parametrów `utm_*`, `fbclid`, `gclid`, końcówki `.git` i kotwicy `#readme`.

Pominięto 1808 wystąpień adresów obecnych wcześniej ([rejestr](pominiete-powtorki.json)). Wśród nich są m.in. adresy repozytoriów czyzby/gdx-skins, devanshutak25/3d-resources, Kavex/GameSounds i JackLuguibin/GameAssets, które były już w katalogach jako linki. W tej fali dodano ich zawartość, ale nie powtórzono wpisu. Kolejne 264 wystąpień w obrębie fali dopisano jako dodatkowe źródła pierwszego wpisu.

## Repozytoria bez zmian

Pięć repozytoriów ze zlecenia miało ten sam commit co w fali 03: praveencrypty, HotpotDesign/Game-Assets-And-Resources, ahnerd, GDQuest/game-sprites i ToxSam/open-source-3D-assets. TMHSDigital miał nowszą wersję i przetworzono go ponownie. Niezmienionych nie przetwarzano drugi raz: mają lokalną kopię i status `bez_zmian_od_fali_03` w manifeście.

## Dokumenty

Dokumenty porównano z inwentarzami fal 02 i 03 po SHA-256 oraz po hashu git-blob. Pominięto 11 identycznych dokumentów ([raport](identyczne-dokumenty.json)); głównie powtarzające się README w folderach Ready Player Me.

## Paczki

Każdy plik w nowych ZIP-ach porównano (SHA-256) z plikami wszystkich 48 wcześniejszych paczek z `BAZA-AI/manifest-assetow.json` i z hashami fali 03. Nie wykryto żadnego powtórzonego pliku zasobu — wynik jest w [raporcie kontroli](../kontrola.json).

Reguły nie wykrywają tego samego materiału pod różnymi domenami ani kopii tej samej grafiki w innym formacie.
