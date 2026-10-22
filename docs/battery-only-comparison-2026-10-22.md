# Battery-only baseline: 80% vs 40% CPU

Date: 2026-10-22. Hardware: MSI Katana GF76 11UC. Powerbank and AC charger disconnected for both tests.

| Reading | BATERIA 80 | ULTRA ECO 40 |
| --- | ---: | ---: |
| Samples | 12 | 12 |
| First - last timestamp | 03:26:08 - 03:28:15 | 03:36:08 - 03:38:15 |
| Average battery discharge | 20.67 W | 19.07 W |
| Highest sampled discharge | 41.75 W | 21.87 W |
| Lowest sampled discharge | 11.39 W | 15.40 W |
| Average CPU load | 44.08% | 50.75% |
| Maximum CPU load | 79% | 66% |
| Laptop battery SoC | 89% to 87% | 80% to 78% |

Mean discharge difference: -1.60 W (-7.7%) in the 40% CPU profile. Due to different laptop battery charge levels and uncontrolled task activity this does not establish a causal improvement. Maximum reading is not the true instantaneous peak and measurements on battery do not measure powerbank input.

These are battery-only baseline data, not an endorsement to power a 150W MSI laptop through an unverified YX-10 PD adapter.
