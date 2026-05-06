# zmk-config-zyraft

Konfiguracja ZMK dla **Zyra FT** - klawiatura 34-klawiszowa oparta na układzie Sweep/Cradio.

## Hardware

- Shield: `cradio` (oficjalny Sweep/Cradio z upstream ZMK)
- Kontrolery: 2× nice!nano v2
- 34 klawisze (5 kolumn × 3 rzędy + 2 thumb na każdą stronę)
- Bez nice!view (pin D1/P0.06 jest zajęty przez switch matrix)

## Warstwy

| # | Nazwa | Aktywacja | Funkcja |
|---|-------|-----------|---------|
| 0 | Base | bazowa | QWERTY z home-row mods |
| 1 | Right | trzymaj prawy thumb (BSPC) | Cyfry, strzałki, HOME/END/PGUP/PGDN |
| 2 | Left | trzymaj lewy thumb (TAB) | Symbole, brackets |
| 3 | Tri | oba thumby jednocześnie | studio_unlock, BT, bootloader, reset |

## Home-row mods (HRM)

Klawisze A/S/D/F i J/K/L/' mają podwójne działanie:
- **Stuknięcie** = litera
- **Przytrzymanie 220 ms** = modyfikator

| Klawisz | Tap | Hold |
|---------|-----|------|
| A | a | Shift |
| S | s | Alt |
| D | d | Ctrl |
| F | f | Gui (Win/Cmd) |
| J | j | Gui |
| K | k | Ctrl |
| L | l | Alt |
| ' | ' | Shift |

`require-prior-idle-ms = 100` - HRM nie aktywuje się jeśli niedawno był naciśnięty inny klawisz, co minimalizuje błędne triggery przy szybkim pisaniu.

## Thumb cluster

| Pozycja | Tap | Hold |
|---------|-----|------|
| Lewy zewn. | TAB | Layer 2 (Left) |
| Lewy wewn. | ENTER | - |
| Prawy wewn. | SPACE | - |
| Prawy zewn. | BSPC | Layer 1 (Right) |

## ZMK Studio

Aktywne. Lewa połówka ma snippet `studio-rpc-usb-uart`.

**Aby odblokować:**
1. Trzymaj **lewy thumb (TAB)** + **prawy thumb (BSPC)** jednocześnie → wchodzisz w Tri layer
2. Naciśnij **Q** (ten sam klawisz fizyczny - lewa górna ręka)
3. W przeglądarce na https://zmk.studio kliknij **Connect**, wybierz port → klawiatura odblokowana

## Build

GitHub Actions buduje 3 firmware automatycznie po każdym pushu:
- `cradio_left-nice_nano-zmk.uf2`
- `cradio_right-nice_nano-zmk.uf2`
- `settings_reset-nice_nano-zmk.uf2`

## Flashowanie

1. Lewa USB → 2× reset → przeciągnij `cradio_left-...uf2` na pendrive `NICENANO`
2. Prawa USB → 2× reset → `cradio_right-...uf2`
3. Połącz TRRS, podłącz lewą do USB → klawiatura "**Zyra FT**" pojawi się w BT
