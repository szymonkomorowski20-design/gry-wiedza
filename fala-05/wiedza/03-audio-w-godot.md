# Audio w Godocie 4.7 — praktyczny przewodnik

Oparte na dokumentacji Godota 4.7 (lokalna kopia: `BAZA-AI/fala-05/zrodla/godotengine--godot-docs-4.7`) i narzędziach znalezionych w fali 05. Nazwy klas i właściwości sprawdzone w dokumentacji klas 4.7.

## 1. Formaty i import

| Format | Kiedy | Dlaczego |
|---|---|---|
| **WAV** | krótkie, często powtarzane SFX (strzał, krok, klik) | brak kosztu dekodowania |
| **Ogg Vorbis** | muzyka, mowa, długie efekty | mały rozmiar |
| **MP3** | web i mobile, gdy gra wiele skompresowanych dźwięków naraz | niższy koszt CPU niż Vorbis |

W doku importu (zakładka *Import*) ustawia się: **Loop** i **Loop Offset** (pętle muzyki, ambientu), a dla muzyki interaktywnej **BPM**, **Beat Count**, **Bar Beats** — potrzebne do przejść „na takt”. Kompresji 8-bit dla WAV nie włączaj (wyraźnie gorsza jakość) — zamiast tego użyj Ogg/MP3.

## 2. Szyny (buses)

`Master` ← `Music`, `SFX`, `UI` (opcjonalnie `Voice`, `Ambient`). Głośność w ustawieniach gry = głośność szyny, nie pojedynczych odtwarzaczy. Efekty (pogłos w jaskini, dolnoprzepustowy pod wodą) nakłada się na szyny. Działający przepis z testami: game-builder `recipes/17-settings` (głośność 0–1 → `linear_to_db`, 0 = wyciszenie) i `recipes/21-audio` (pula głosów SFX).

## 3. Wbudowane typy strumieni — mniej kodu własnego

| Klasa | Do czego | Kluczowe API |
|---|---|---|
| `AudioStreamRandomizer` | warianty tego samego dźwięku (5 kroków, 3 trafienia) z losową wysokością i głośnością | `add_stream()`, `random_pitch` (np. `1.1` = od 1/1,1 do 1,1), `random_pitch_semitones`, `random_volume_offset_db`, `playback_mode` |
| `AudioStreamPolyphonic` | wiele dźwięków naraz z **jednego** odtwarzacza | `player.get_stream_playback().play_stream(stream)`; `stop_stream`, `set_stream_volume`, `set_stream_pitch_scale` |
| `AudioStreamPlayer.max_polyphony` | ten sam dźwięk nakładający się na siebie | właściwość (domyślnie 1) |
| `AudioStreamInteractive` | **muzyka adaptacyjna**: klipy + tabela przejść (eksploracja → walka → boss) | `set_clip_stream()`, `set_clip_name()`, `add_transition()`; w trakcie gry `get_stream_playback().switch_to_clip_by_name("walka")` |
| `AudioStreamSynchronized` | warstwy muzyki grane równo (perkusja, bas, melodia) — podkręcasz głośność warstw | `set_sync_stream()`, `set_sync_stream_volume()` |
| `AudioStreamPlaylist` | kolejka utworów, tasowanie | `set_list_stream()`, `shuffle` |
| `AudioStreamGenerator` | dźwięk liczony w kodzie (synteza, sonifikacja) | `get_stream_playback().push_frame()` |

Przykład — kroki z wariantami (zero własnej logiki losowania):

```gdscript
var steps := AudioStreamRandomizer.new()
for path in ["res://audio/step_1.wav", "res://audio/step_2.wav", "res://audio/step_3.wav"]:
	steps.add_stream(-1, load(path))
steps.random_pitch = 1.08
steps.random_volume_offset_db = 2.0
$StepPlayer.stream = steps
$StepPlayer.play()
```

Przykład — przełączenie muzyki na walkę (przejście według tabeli):

```gdscript
var playback := $Music.get_stream_playback() as AudioStreamPlaybackInteractive
playback.switch_to_clip_by_name(&"walka")
```

## 4. Eksport do przeglądarki — ograniczenia (ważne dla gier webowych)

Od Godota 4.3 web domyślnie używa trybu **Sample** (Web Audio API, niskie opóźnienie). W tym trybie:

- **nie działają** efekty audio (`AudioEffect*`), pogłos i efekt Dopplera,
- **nie działa** generowanie proceduralne (`AudioStreamGenerator`),
- dźwięk pozycyjny może działać niepoprawnie.

Pełne audio Godota: *Project Settings → Audio → General → Default Playback Type.web* = **Stream** albo właściwość **Playback Type** = Stream na konkretnym odtwarzaczu — kosztem większego opóźnienia. Przeglądarki blokują autoodtwarzanie: pierwszy dźwięk dopiero po kliknięciu/klawiszu (np. ekran „Kliknij, aby zacząć”).

**Wniosek dla game-buildera:** w specyfikacji gry z celem „web” trzeba zapisać, czy gra używa efektów szyn lub generowania dźwięku — jeśli tak, decyzja „Stream” i test na eksporcie webowym.

## 5. Rozszerzenia i integracje (z katalogu fali 05)

| Projekt | Licencja | Do czego | Uwagi |
|---|---|---|---|
| [`utopia-rise/fmod-gdextension`](https://github.com/utopia-rise/fmod-gdextension) | MIT (wiązania) | FMOD Studio w Godocie 4 | FMOD ma własną licencję — sprawdź warunki na fmod.com przed wydaniem |
| [`alessandrofama/wwise-godot-integration`](https://github.com/alessandrofama/wwise-godot-integration) | brak deklaracji SPDX | Wwise w Godocie | Wwise ma własną licencję Audiokinetic |
| [`detomon/godot-blipkit`](https://github.com/detomon/godot-blipkit) | MIT | GDExtension: brzmienie starych układów (chiptune na żywo) | dobre do gier retro bez plików audio |
| [`hyprtuna/divisi`](https://github.com/hyprtuna/divisi) | MIT | muzyka adaptacyjna: zegar muzyczny bez dryfu, sygnały na beat i takt | alternatywa/uzupełnienie `AudioStreamInteractive` |
| [`maxotaku11niku/bambootrackerplayer`](https://github.com/maxotaku11niku/bambootrackerplayer) | MIT | odtwarzanie modułów BambooTracker (FM) | |
| [`timoncool/godot-strudel`](https://github.com/timoncool/godot-strudel) | AGPL-3.0 | live-coding muzyki (Strudel) w GDScript | AGPL — uważnie przy grach zamkniętych |
| `MightyPrinny/godot-FLMusicLib` | CC0 | MP3, chiptune, trackery przez Game Music Emu | GDNative = **Godot 3**, w 4 nie działa bez portu |
| `kyzfrintin/godot-mixing-desk` | MIT | proceduralny miks i muzyka warstwowa | tylko **Godot 3.3** — w 4 zastąpione przez klasy z punktu 3 |

## 6. Generowanie dźwięków bez plików

- **8bit-sfx** (paczka `8bit-sfx-komplet` w tej fali: wszystkie 8888 efektów jako WAV mono 8-bit 22,05 kHz, 14,8 MB): deterministycznie z nazwy — importujesz gotowe pliki.
- **sfxr / jfxr / ChipTone** (fale 01–04): edytory parametrów; eksport WAV.
- `AudioStreamGenerator` + własny oscylator — tylko desktop albo web w trybie Stream.

## 7. Testowanie audio

W game-builderze testy działają bez głośników: sterownik „dummy” w trybie headless odtwarza strumienie (`playing` = true), więc da się sprawdzić logikę (wybór głosu, kradzież najstarszego, zakres wysokości — `recipes/tests/unit/test_r21_audio.gd`). Nie da się automatycznie ocenić **brzmienia i synchronizacji** — to punkt bramki playtestu człowieka.
