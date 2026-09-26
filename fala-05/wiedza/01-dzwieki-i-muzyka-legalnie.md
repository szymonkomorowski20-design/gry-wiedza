# Dźwięki i muzyka do gier — skąd brać legalnie i na co uważać

Opracowanie fali 05 (26 września 2026). Wnioski z przejrzenia ok. 2800 repozytoriów z tematów GitHuba o audio, dwóch poziomów linków z ich README i czterech repozytoriów wskazanych przez właściciela biblioteki.

## Najważniejsza zasada: licencja kodu ≠ licencja dźwięków

Repozytorium z plikiem `LICENSE` na MIT nie oznacza, że dźwięki w środku są na MIT. Trzy przykłady z tej fali, w których deklaracja w repozytorium nie wystarcza do legalnego użycia dźwięków:

| Repozytorium | Co deklaruje | Co jest naprawdę w środku | Co zrobiliśmy |
|---|---|---|---|
| `Citedy/game-sounds` | MIT | 594 dźwięki wycięte z gier Nintendo, Blizzard, EA/Westwood, Konami, Capcom i in. oraz z Myinstants (tak podaje sam README w „Credits”) | Dźwięki i nagrania demo usunięte z lokalnej kopii razem z historią git; zostawiony kod hooków Claude Code |
| `kapishdima/soundcn` | MIT; „większość dźwięków CC0” | 703 dźwięki Kenney (CC0) + 110 dźwięków World of Warcraft („© Blizzard Entertainment — All Rights Reserved”) | 110 dźwięków Blizzard usunięte lokalnie; z CC0 opublikowane tylko 3 paczki Kenney, których nie było w bibliotece |
| `JimLynchCodes/Game-Sound-Effects` | brak licencji | 45 dźwięków, autor: „o ile wiem, royalty free” — bez źródeł | Już w fali 04 (lokalna kopia `BAZA-AI/fala-04`, opis w katalogu fali 04) — w fali 05 nie powtarzamy; nie do wydanej gry |

**Jak sprawdzać:** czytaj sekcje *Credits*, *License*, *Sources* w README; szukaj osobnych plików (`LICENSE-ASSETS.md`, `FACTORY-BANK-LICENSE.md`, `License.txt` w folderze paczki); w rejestrach z metadanymi (jak `registry.json` w soundcn) licencja bywa zapisana przy każdym dźwięku osobno.

## Mirror może źle podawać licencję

`goblinhack/deceased-superior-technician-music` (692 utwory, 3,1 GB) ma w repozytorium plik CC0, ale README cytuje autora: muzyka jest na **Creative Commons Attribution** („wystarczy link do nosoapradio.us”). Obowiązuje licencja autora, nie mirrora — w bibliotece traktujemy DST jako **CC-BY: wolno komercyjnie, trzeba podać autora**. Potwierdzenie w niezależnych źródłach: forum FreeGameDev, Last.fm.

## Przejęte domeny

Domena `nosoapradio.us` (dawna strona DST) należy dziś do kogoś innego — strona pokazuje „wpłaty i wypłaty”, nie muzykę. **Nie linkuj jej jako źródła.** W atrybucji podawaj nazwę artysty i historyczny adres jako zwykły tekst. Taka sytuacja powtarza się w starych listach „free music” — zanim dodasz link do napisów końcowych gry, otwórz go.

Przykładowa atrybucja do napisów końcowych:

```
Music: "Nazwa utworu" by Deceased Superior Technician (No Soap Radio),
licensed under Creative Commons Attribution. Originally published at nosoapradio.us.
```

## Przynęty z malware w tematach o audio

Tematy `sound-design`, `chiptune`, `fmod` zawierają repozytoria podszywające się pod programy komercyjne: „FL Studio 25 All Plugins Edition”, „Kontakt 8 Full Library”, „Serum VST Installer Free”, „Sylenth1 Crack”, „Adobe Audition Pro”, „Antares Auto-Tune Pro”, „Ableton Live 2026”. Wspólne cechy: repozytorium ma kilka kB, zero gwiazdek, nazwę produktu i słowa „Pro/Ultimate/Full/Edition/Installer/2025–2026”. **Wykluczyliśmy 56 takich repozytoriów** (lista: `zrodla/pominiete-podejrzane.json`). Nigdy nie pobieraj z nich „instalatorów”.

Wykluczone są też narzędzia do masowego pobierania cudzej muzyki (khinsider, Zophar's Domain, zgrywki dźwięków z gier) — technicznie działają, ale służą do kopiowania chronionych utworów.

## Legalne źródła — co jest nowego w fali 05

Klasyczne serwisy (Freesound, OpenGameArt, Kenney, Sonniss GDC Bundle, Incompetech, Free Music Archive, ccMixter, BBC Sound Effects, Pixabay, Zapsplat, Mixkit, Soundimage, Musopen, sfxr/bfxr/jfxr/ChipTone, 99Sounds, FreePD) są już w katalogach fal 01–04. W tej fali dochodzą:

| Źródło | Licencja | Uwagi |
|---|---|---|
| Muzyka DST (mirror na GitHubie) | CC-BY | 692 utwory elektroniczne/ambient do gier; atrybucja wymagana; wybór 8 utworów w paczce `dst-muzyka-wybor`, komplet lokalnie w BAZA-AI |
| `gvastethecreator/game-music-composer` | CC0 | 140 utworów (OGG i MP3), 140 plików MIDI, bank próbek, paczki Mega Drive/SNES z oryginalnymi instrumentami; zawiera skill dla agentów AI |
| `cportka/8bit-sfx` | MIT | 8888 efektów 8-bit w 44 kategoriach — syntezowane deterministycznie (ta sama nazwa = ten sam dźwięk) |
| `GareBear99/Free-Dark-Piano-Sound-Kit` | MIT + licencja assetów | 88 nut fortepianu A0–C8 + 26 pętli WAV z MIDI (15 mrocznych oryginałów, 11 motywów z muzyki klasycznej w domenie publicznej) |
| Kenney: Music Jingles, Voiceover Pack, Voiceover Pack Fighter | CC0 | brakowały w bibliotece (pozostałe 6 paczek audio Kenney są już w falach 01–02 — sprawdzone po SHA-256) |

Serwisy z muzyką, zweryfikowane na ich stronach warunków 26 września 2026:

| Serwis | Licencja | Atrybucja | Zakazy |
|---|---|---|---|
| [Maou-Damashii (魔王魂)](https://maou.audio) — muzyka i SFX fantasy/RPG | CC BY 4.0 | **wymagana** („Music: Maou-Damashii”) | podawanie się za autora, Spotify/NFT, trening AI |
| [OpenTracks](https://opentracks.com) — dawniej DOVA-SYNDROME (zmiana nazwy 15.09.2026), BGM od wielu twórców | własne warunki | niewymagana (twórca może wymagać) | rozpowszechnianie samego pliku, muzyka jako główna treść, trening AI, Content ID |
| [ENDE.APP](https://ende.app) — dawniej filmmusic.io, ~780 utworów Sascha Ende | CC BY 4.0 | autor zwalnia z podpisu, ale bezpieczniej podpisać | niezmienione utwory w serwisach muzycznych, Content ID |

Stare adresy `dova-s.jp` i `filmmusic.io` przekierowują pod nowe — w starych listach linki działają, ale podawaj nowe.

Uwaga do piano kitu: licencja assetów zabrania przedstawiania „mrocznych oryginałów” jako oficjalnej muzyki istniejących serii i odsprzedaży samej paczki. W grze można ich używać bez ograniczeń.

## Wątek z Reddita

Link `r/gamedev — where to find open-source music and sound effects` był niedostępny dla wszystkich narzędzi (blokada serwisu dla automatów). Typowe źródła z takich wątków są opisane wyżej lub w katalogach poprzednich fal. Jeśli treść wątku jest potrzebna dosłownie — trzeba ją wkleić ręcznie.

## Lista kontrolna przed wydaniem gry z cudzym audio

1. Każdy plik audio w projekcie ma wpis w rejestrze licencji (w game-builderze: `.ai/assets/REGISTER.md`, sprawdzany przez `gb lint`).
2. Licencja pochodzi od autora, nie od mirrora czy agregatora.
3. CC-BY / CC-BY-SA → tekst atrybucji w napisach lub w menu „Credits” (autor, tytuł, licencja, link).
4. CC-BY-NC → nie w grze płatnej ani z reklamami.
5. „Royalty free” bez nazwy licencji → znajdź warunki na stronie autora albo nie używaj.
6. Dźwięki z innych gier, filmów, seriali, Myinstants → nigdy.
7. Linki w atrybucji otwarte przed wydaniem (przejęte domeny).
8. Wygenerowane przez AI → sprawdź warunki narzędzia (część usług zastrzega prawa lub wymaga planu płatnego do użytku komercyjnego).

## Powiązane

- [Katalog: dział 08a–08j](../katalog/README.md) — wszystkie znalezione narzędzia i źródła audio.
- [Audio w Godocie 4.7](03-audio-w-godot.md) — jak to podłączyć w grze.
- Fala 04: [SFX](../../fala-04/wiedza/01-dzwieki-sfx.md).
