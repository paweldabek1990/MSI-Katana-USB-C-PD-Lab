# Metodyka testów i interpretacja danych

## Konfiguracja (22 października 2026)

- Komputer: MSI Katana GF76 11UC, fabryczne zasilanie 150 W (20 V / 7,5 A).
- Źródło: Silver Monkey 20 000 mAh, deklarowane USB-C PD 100 W.
- Kabel: Sollogic USB-C / USB-C 60 W, 3 A.
- Adapter PD-to-DC: YX-10, oznaczenie 20V PD, okrągła końcówka 4,5 × 3,0 mm z pinem.
- Akumulator: nominalnie 52 007 mWh; ostatnia pojemność przy pełnym naładowaniu 33 653 mWh.
- Windows: plan ULTRA ECO (maksymalny stan procesora 40% AC i DC), SMART 60 (60% AC i DC); Turbo Boost ustawiany jako wyłączony.
- Brak bezpośredniego wejścia ładowania USB-C w tym egzemplarzu laptopa; powerbank podłączano przez przejściówkę USB-C PD → DC.

## Źródła pomiaru

1. Skrypt Windows/PowerShell korzystał z **root/wmi:BatteryStatus** i **Win32_Battery**: PowerOnline, Charging, Discharging, ChargeRate, DischargeRate, RemainingCapacity i EstimatedChargeRemaining.
2. Stany AC / Charging i poziom naładowania były próbkowane podczas pracy komputera. Liczba przełączeń dotyczy tylko zarejestrowanych zmian pomiędzy próbkami — krótkie zaniki między próbkami mogły pozostać niewidoczne.
3. Przy stabilnej pracy z wyświetlacza Silver Monkey ręcznie odczytywano około 20 V, 1,5–2,0 A. **To obserwacje operatora, a nie zapis danych analizatora PD.**
4. Wartość BatteryRateW oznacza moc netto kierowaną do baterii laptopa, a nie pobór całego laptopa ani maksymalną moc USB-C.
5. Niestabilne próby przy 62–72% SoC dokumentowano wzrokowo. Nie posiadamy zsynchronizowanego przebiegu napięcia/prądu z momentu rozłączenia.

## Rezultaty

| Test | Czas | Próbki | AC/DC transitions | Energia baterii |
|---|---:|---:|---:|---|
| ULTRA ECO 40% | 11 min 17 s | 61 | 0 | 84→89,6%; średnio +9,36 W |
| SMART 60% | 4 min 57 s | 27 | 0 | 86→89%; +16,58→+8,77 W |
| SMART 60% + zgłoszona aktywność Codexa | ok. 3 min (limit skryptu) | **41** | **0** | 88→90%; raport TXT bez podanej mocy |

W pierwszych dwóch testach system Windows wskazywał podłączenie zasilania i ładowanie. Trzeci raport SMART 60 (znacznik 20261022-030105) potwierdza 41 próbek, brak wykrytych przełączeń oraz przyrost SoC z 88 do 90%; zawiera stan `Completed normally`, ale nie podaje wartości mocy ani pełnej historii obciążenia. Codex pracował według bieżącej relacji operatora. Przy 62–72% wystąpiły wcześniejsze powtarzalne rozłączenia.

## Ograniczenia i możliwe błędy

- Ograniczenie procesora do 40% lub 60% **nie jest** limitem mocy całego laptopa w watach.
- Niższy stan naładowania mógł oznaczać większy prąd ładowania, ale nie wykonano pomiaru porównawczego poboru przy tym samym obciążeniu.
- Odczyty przy wysokim SoC nie przewidują zachowania przy niższym SoC.
- Brak potwierdzenia elektrycznej zgodności sygnału identyfikacyjnego adaptera YX-10 z laptopem MSI.
- Z faktu, że powerbank jest oznaczony 100 W, **nie wynika** możliwość ciągłego dostarczenia 100 W przez kabel 60 W i konkretny trigger.
- Nie prowadzić ponownych prób z cyklicznym odcinaniem zasilania, dopóki tor PD nie zostanie zweryfikowany.
