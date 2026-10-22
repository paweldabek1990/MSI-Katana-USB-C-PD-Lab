# Schemat danych / Data dictionary

Plik [test-results.csv](test-results.csv) zawiera **agregaty i obserwacje z 22 października 2026**, a nie surowy, synchroniczny zapis przebiegu prądu USB-C.

| Pole | Znaczenie |
|---|---|
| `date` | Data eksperymentu w lokalnej strefie operatora |
| `mode` | Profil zarządzania energią Windows |
| `cpu_state_max_ac_dc_percent` | Maksymalny stan procesora AC i DC, **nie** moc laptopa |
| `battery_start_percent` / `battery_end_percent` | Odczyt SoC akumulatora MSI |
| `duration_seconds` | Czas monitoringu |
| `samples` | Liczba próbek Windows |
| `observed_ac_dc_transitions` | Zmiany źródła zasilania w monitoringu lub obserwacja wizualna |
| `battery_net_power` | Wskaźnik ładowania baterii, **nie** prąd na wejściu z powerbanku |
| `status` | Stabilny wyłącznie w czasie obserwacji lub niestabilny |
| `measurement_type` | `logged`, `console log` albo `user observation` |

Wpisy `~` oraz puste pola oznaczają niepełne dane, nie zero. Przy wynikach wizualnych liczba przełączeń nie jest wyznaczona przez telemetrię Windows.

Dla powtarzalności przyszłych eksperymentów wymagane będą: dokładny model triggera, elektryczna zgodność wyjścia DC, pomiar profilu PD, zakres stanu baterii MSI, obciążenie oraz brak objawów cyklicznego rozłączania.

## Rejestr testu z obciążeniem CPU — 22.10.2026

[powerbank-stress-2026-10-22.csv](powerbank-stress-2026-10-22.csv) zawiera 34 próbki z testu z podłączonym Silver Monkey 100 W, kablem Sollogic 60 W i adapterem YX-10. Dane zostały znormalizowane z oryginalnego eksportu PowerShell (przecinki dziesiętne → kropki; od początku testu: 0–74 s).

| Kolumna | Znaczenie |
|---|---|
| `elapsed_seconds` | Czas od pierwszego pomiaru, zaokrąglony w skrypcie do sekund |
| `phase` | BASE, CPU_TEST lub COOLDOWN |
| `source` | Stan źródła według Windows, AC lub BAT |
| `charging` | Flaga ładowania baterii z Windows |
| `battery_percent` | Stan naładowania baterii MSI, nie powerbanku |
| `cpu_percent` | Odczyt średniego wykorzystania procesora |
| `battery_net_W` | Moc netto do baterii MSI, nie całkowita moc wejściowa z USB-C; pierwszy odczyt pusty |

Wszystkie 34 próbki wykazały AC i `charging=True`; przyrost SoC wyniósł 83→84%. Brak wykrytego rozłączenia nie oznacza, że bardzo krótki zanik pomiędzy próbkami jest wykluczony. Pomiar nie potwierdza stabilności przy 62–72% naładowania baterii MSI.

**Plan dalszy:** [porównanie UGREEN 100 W / 5 A z Sollogic 60 W / 3 A, 24.10.2026](https://github.com/paweldabek1990/MSI-Katana-USB-C-PD-Lab/issues/1), pod warunkiem otrzymania kabla i zweryfikowania adaptera.
