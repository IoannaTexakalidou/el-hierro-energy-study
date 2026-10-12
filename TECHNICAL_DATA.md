# Technical data and bill of materials

This page lists the exact equipment I used in the model, its technical data, and what the least-cost system would cost to build. Every value comes from the source named next to it. Costs are in 2024 euros.

## 1. Wind turbine: Enercon E-70 E4, 2.3 MW

This is the turbine model already installed at the Gorona del Viento wind farm on El Hierro (5 units). I used the same model so that I could check my results against the real farm.

| Parameter | Value |
|---|---|
| Rated power | 2,300 kW |
| Rotor diameter | 71 m |
| Swept area | 3,959 m² |
| Hub height | 64 m (Taveira et al. 2018) |
| Starts producing at (cut-in) | 2 m/s |
| Reaches full power at | 15 m/s |
| Shuts down at (cut-out) | 25 m/s |
| Availability | 97% (Danish Energy Agency) |
| Lifetime | 27 years (Danish Energy Agency) |
| Capital cost | 1,422 EUR/kW, so 3.27 million EUR per turbine (Danish Energy Agency) |
| Operation and maintenance | 20.9 EUR/kW per year plus 2.47 EUR/MWh (Danish Energy Agency) |
| Power curve source | Open Energy Database, distributed with windpowerlib |

**Power curve** (electrical output in kW at each wind speed, standard air density 1.225 kg/m³):

| Wind (m/s) | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 to 25 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Power (kW) | 2 | 18 | 56 | 127 | 240 | 400 | 626 | 892 | 1,223 | 1,590 | 1,900 | 2,080 | 2,230 | 2,300 | 2,310 |

**What one turbine produced in my model at El Hierro (2025 weather):** 7,061 MWh in the year, capacity factor 35.0%. After scaling down to the wind the site really has (see the README), 6,210 MWh and 30.8%.

## 2. Solar panel: Jinko JKM580N-72HL4-BDV, 580 Wp

A current n-type TOPCon module, typical of what is installed in utility PV plants today.

| Parameter | Value |
|---|---|
| Rated power at standard test conditions | 580 Wp |
| Open circuit voltage (Voc) | 52.50 V |
| Short circuit current (Isc) | 13.95 A |
| Voltage at maximum power (Vmp) | 43.88 V |
| Current at maximum power (Imp) | 13.22 A |
| Module area | 2.58 m² |
| Efficiency | 22.48% |
| Fill factor | 79.2% |
| Temperature coefficient of power | −0.295 %/°C |
| Temperature coefficient of Voc / Isc | −0.257 / +0.045 %/°C |
| NOCT | 45.2 °C |
| Mounting | fixed, tilted 25°, facing south (PVGIS optimum for the site) |
| Inverter, wiring and other losses | 12% (PVGIS standard 14% minus its 2% for dust, which I model separately) |
| Lifetime | 40 years (Danish Energy Agency) |
| Capital cost | 550 EUR/kWp, so 319 EUR per installed module including everything around it (Danish Energy Agency) |
| Operation and maintenance | 9.3 EUR/kWp per year (Danish Energy Agency) |
| Land | 0.775 ha per MWp (Danish Energy Agency) |
| Data source | CEC module database, NREL System Advisor Model |

**What one panel produced in my model at El Hierro (2025 weather):** 1,061 kWh in the year, capacity factor 20.9%. Dust on the panels cost 6.0% and heat cost 5.0% of the output.

## 3. Battery: utility scale lithium ion

| Parameter | Value |
|---|---|
| Technology | lithium ion, utility scale, in containers (Danish Energy Agency, Technology Data for Energy Storage, 2025 values) |
| Round trip efficiency | 91% (AC to AC) |
| Lifetime | 20 years or 6,000 full cycles, whichever comes first |
| Capital cost | 234 EUR per kWh of storage plus 101 EUR per kW of power |
| Operation and maintenance | 9.7 EUR/kW per year |
| Sizes tested | 0 to 400 MWh, with 2, 4 or 8 hours of storage |

## 4. Bill of materials for the least-cost system

The cheapest system the model found covers 97.5% of the island's electricity from wind and sun. The existing diesel plant (12.7 MW) stays as backup and covers the remaining 2.5%, so it is not bought again and is not in this list.

| Item | Quantity | Unit cost | Total |
|---|---|---|---|
| Enercon E-70 wind turbine, 2.3 MW | 1 turbine (2.3 MW) | 3.27 million EUR each | 3.27 million EUR |
| Jinko 580 Wp solar panels, with inverters and mounting | 60,345 panels (35 MWp) | 550 EUR/kWp | 19.24 million EUR |
| Lithium ion battery, storage | 80 MWh | 234 EUR/kWh | 18.72 million EUR |
| Lithium ion battery, power conversion | 10 MW | 101 EUR/kW | 1.01 million EUR |
| **Total investment** | | | **42.2 million EUR** |

**Where the money goes inside each item.** The Danish Energy Agency splits each total into parts. Applied to this system:

| Wind (1 turbine) | Million EUR |
|---|---|
| Turbine (nacelle, rotor, tower) | 2.39 |
| Installation and development | 0.25 |
| Land purchase or rent | 0.31 |
| Settlements with neighbours | 0.19 |
| Removal of older turbines | 0.09 |
| Grid connection | 0.05 |

The parts of each item may not add up exactly to its total because of rounding.

| Solar plant (35 MWp) | Million EUR |
|---|---|
| Solar panels | 5.04 |
| Inverters | 0.84 |
| Mounting structures, cabling and rest of plant | 5.38 |
| Transformer and grid connection | 1.93 |
| Installation | 4.37 |
| Design, permits and financing | 1.68 |

| Battery (80 MWh, 10 MW) | Million EUR |
|---|---|
| Battery cells and racks | 6.24 |
| Construction, cabling and other project costs | 12.48 |
| Power conversion (inverters) | 1.01 |

The battery is charged and emptied about 283 times a year, so it reaches the end of its 20 year life before its 6,000 cycles. The wind breakdown is Danish practice. Neighbour settlements and removal of older turbines may not apply on El Hierro, so the wind cost is if anything on the high side.

**Running costs per year.**

| | EUR per year |
|---|---|
| Wind turbine maintenance | about 48,000, plus 2.47 EUR for every MWh produced |
| Solar plant maintenance | about 324,000 |
| Battery maintenance | about 97,000 |
| Diesel fuel and maintenance for the remaining 2.5% (1,278 MWh) | about 251,000 |

**Cost per year, with the investment spread over each item's lifetime** (4% real interest rate, the European Commission benchmark):

| Part | Million EUR per year |
|---|---|
| Wind turbine | 0.26 |
| Solar plant | 1.30 |
| Battery | 1.55 |
| Diesel backup (fuel and maintenance) | 0.25 |
| **Total** | **3.36** |

3.36 million EUR a year divided by the 51.6 GWh the island uses gives 65 EUR per MWh. Running on diesel alone costs 196 EUR per MWh for fuel and maintenance only.

**Land.** 35 MWp of solar panels need about 27 hectares, 5% of the 561 ha the island has classified as suitable for renewable projects.

## 5. Sources

Costs are the central estimates of the Danish Energy Agency technology catalogues, published in 2020 euros and converted to 2024 euros with the Eurostat euro area price index (×1.20). They are European average costs, not quotes for an island. The Canary Islands wind programme EOLCAN-2 cost about 1.20 million EUR per MW in 2021 to 2022, which is in line with the 1.42 million EUR per MW used here in 2024 euros.

1. Danish Energy Agency and Energinet, Technology Data for Generation of Electricity and District Heating (sheets 20 Onshore turbines, 22 Utility-scale PV)
2. Danish Energy Agency and Energinet, Technology Data for Energy Storage (sheet 180 Lithium Ion Battery)
3. Open Energy Database turbine library, windpowerlib (Enercon E-70/2300 power curve)
4. NREL System Advisor Model, CEC module database (Jinko JKM580N-72HL4-BDV)
5. European Commission JRC, PVGIS 5.3
6. Taveira N. et al. (2018), The hybrid power plant in El Hierro island, 3rd Hybrid Power Systems Workshop
7. European Commission (2014), Guide to Cost-Benefit Analysis of Investment Projects
