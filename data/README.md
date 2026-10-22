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
