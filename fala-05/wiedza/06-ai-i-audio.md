# AI i audio — generowanie, MCP, skille dla agentów

Dział katalogu: [08i — AI i audio](../katalog/08i-ai-audio.md). Stan na 26 września 2026.

## Narzędzia, które agent (Claude Code) może używać sam

| Projekt | Licencja | Co daje |
|---|---|---|
| [`ehm-93/chipsmith`](https://github.com/ehm-93/chipsmith) | MIT-0 | **Serwer MCP**: model pisze piosenkę jako JSON z nutami w stylu MML, silnik renderuje ją deterministycznie do WAV (szybciej niż w czasie rzeczywistym, bez zależności audio). Idea: „model komponuje bez uszu”, bo mała paleta i ścisła specyfikacja pozwalają przewidzieć efekt zmian |
| `gvastethecreator/game-music-composer` | CC0 | **Skill** (Python CLI): komponuje, recenzuje, pisze MIDI, renderuje audio; 32 style; studio w przeglądarce do odsłuchu |
| [`dannyjpwilliams/ui-sound-design-skill`](https://github.com/dannyjpwilliams/ui-sound-design-skill) | MIT | **Skill**: opis słowny dźwięku → kod Web Audio / Tone.js |
| `cportka/8bit-sfx` | MIT | biblioteka 8888 efektów z opisami tekstowymi — agent wybiera dźwięk, **czytając katalog** zamiast słuchać |
| `tbimbato/MCP_RiR` | MIT | MCP generujący odpowiedzi impulsowe (pogłos) z opisu słownego |
| `MiasolChen/wwise-sdk-skill` | MIT | skill do badania SDK Wwise w konkretnej wersji z lokalnej dokumentacji |
| `celian-mrc/serum-mcp`, `dreamrec/livepilot` | MIT / brak | sterowanie syntezatorem Serum 2 i Ableton Live 12 z klienta AI (wymagają licencji tych programów) |

**Wzorzec wart przejęcia do game-buildera:** agent nie słyszy, więc wybiera i tworzy dźwięki przez **tekst** — katalog z opisami (8bit-sfx), deterministyczny renderer (chipsmith, 8bit-sfx) i odsłuch przez człowieka na bramce playtestu.

## Modele generujące (lokalnie lub przez API)

| Model | Licencja repozytorium | Uwagi |
|---|---|---|
| [Stable Audio 3](https://github.com/stability-ai/stable-audio-3) (★771) | MIT (kod) | wersje Small-Music i Small-SFX działają na CPU (433M parametrów, do 120 s); Medium wymaga GPU; Large tylko przez API. **Wagi modeli mają własną licencję na Hugging Face** — przeczytaj przed użyciem komercyjnym |
| [Qwen3-TTS](https://github.com/qwenlm/qwen3-tts) (★13,5 tys.) | Apache-2.0 | synteza mowy — głosy NPC, prototypy dialogów |
| [RAVE](https://github.com/acids-ircam/rave) (★1,8 tys.) | brak SPDX | autoenkoder audio w czasie rzeczywistym — przekształcanie barwy |
| [ACE-Step Studio](https://github.com/timoncool/ace-step-studio) (★344) | MIT | przenośny generator całych piosenek z wokalem |
| `prabal-rje/latentscore` | Apache-2.0 | muzyka ambient z opisu tekstowego |

**Prawa do wygenerowanych dźwięków:** zależą od licencji wag modelu i regulaminu usługi, nie od licencji kodu. Nie generuj głosów podobnych do prawdziwych osób bez ich zgody; zapisz w rejestrze licencji projektu, którym modelem i z jaką licencją powstał plik.

## Dźwięki w samym Claude Code (hooki)

Wtyczki grające dźwięk na zdarzenia sesji (start, przyjęcie zadania, koniec, błąd, prośba o zgodę) używają hooków `SessionStart`, `UserPromptSubmit`, `Stop`, `PostToolUseFailure`, `Notification`:

- `Citedy/game-sounds` — mechanizm w porządku (MIT, `hooks/hooks.json` + `scripts/play-sound.sh` z losowaniem dźwięku z kategorii i głośnością z `config.json`), ale **paczki dźwięków pochodzą z komercyjnych gier** — w bibliotece zostawiliśmy tylko kod.
- `peonping/peon-ping` (★5 tys.) — głosy „Peona” z Warcraft III: kod MIT, **dźwięki Blizzarda**.

Legalna wersja tego pomysłu: ten sam mechanizm hooków + dźwięki CC0 (np. z paczek `kenney-voiceover-pack`, `8bit-sfx-komplet`). Kandydat do game-buildera jako opcjonalny dodatek („gra dźwięk, gdy `gb verify` przejdzie/padnie”).

## Powiązane

- [Opracowanie 04](04-chiptune-trackery-generatory.md) — generatory bez AI.
- [Opracowanie 01](01-dzwieki-i-muzyka-legalnie.md) — licencje.
