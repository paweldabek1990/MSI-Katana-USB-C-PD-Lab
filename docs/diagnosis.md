# Diagnoza niestabilnego zasilania

## Oś zdarzeń

| Warunki | Zachowanie |
|---|---|
| Bateria 84–89,6%, ULTRA ECO 40% | Zasilanie i ładowanie stabilne w 11:17 obserwacji (61 próbek) |
| Bateria 86–89%, SMART 60% | Zasilanie i ładowanie stabilne w 04:57 obserwacji (27 próbek) |
| Bateria ok. 70–72%, SMART 60% | Około 16 widocznych cykli przełączania AC/bateria |
| Bateria 62%, ULTRA ECO 40% | Wielokrotne zaniki; zasilanie nie utrzymywało się |

Przy nieudanych próbach jednocześnie wykonywano intensywne zadania w Chrome / ChatGPT, ACC, Codexie i PowerShell. Diagnostyka wykazała zgodne z oczekiwaniami limity stanu procesora 60% AC/DC, ale nie zmierzono mocy wejściowej w chwili awarii.

## Hipotezy — żadna niepotwierdzona

| Hipoteza | Dlaczego rozważana | Czego brakuje |
|---|---|---|
| Zbyt duże chwilowe zapotrzebowanie na moc | Niższy SoC może podnieść moc ładowania, a aplikacje obciążają system | Analizator PD rejestrujący piki |
| Ograniczenie kabla 60 W / 3 A | USB-C przewód 3 A ogranicza standardową negocjację 20 V do 60 W | Potwierdzenie negocjowanego profilu i zachowania YX-10 |
| Nieprawidłowy reset / limit triggera YX-10 | Możliwe cykle renegocjacji lub ograniczenie termiczne | Dokumentacja i pomiar konkretnej przejściówki |
| Niezgodność pinu identyfikacyjnego Dell/MSI | Adapter z centralnym pinem nie ma potwierdzonej zgodności z MSI | Dokumentacja elektryczna, nie samo dopasowanie mechaniczne |
| Gorszy styk / napięcie pod obciążeniem | Intermitentny kontakt może udawać przeciążenie | Profesjonalny test elektryczny złącza |

## Dlaczego kabel 100 W nie daje gwarancji?

UGREEN 5 A z e-markerem może usunąć **limit przewodu** 3 A, ale nie zwiększa możliwości samego powerbanku, laptopa ani adaptera. Jeśli źródłem problemu jest YX-10 albo identyfikacja zasilacza, sama wymiana kabla może niczego nie poprawić. Na dzień publikacji nowy kabel pozostaje **nieprzetestowany**.

> [!WARNING]
> Testów przy cyklicznym rozłączaniu nie należy powtarzać w ciemno. Oryginalny zasilacz MSI 150 W pozostaje bezpieczniejszą referencją dla normalnej pracy. Dalsza diagnostyka wymaga potwierdzenia specyfikacji elektrycznej adaptera i odpowiednich pomiarów po stronie PD.

## Co potwierdziłby następny prawidłowy eksperyment?

- Znana dokumentacja adaptera YX-10, maksymalny prąd i zachowanie środkowego pinu.
- Analizator PD pokazujący kontrakt 20 V i rzeczywiste ograniczenie prądowe.
- Rejestrowany przebieg napięcia i prądu bez wielokrotnego resetowania podłączonego laptopa.
- Porównywalny stan baterii i obciążenie dla przewodu 3 A oraz 5 A — tylko jeśli zgodność elektryczna została potwierdzona.
