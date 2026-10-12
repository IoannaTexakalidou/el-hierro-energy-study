# Formulas used in the study

Every equation the model uses, grouped by topic, with a short note on what it does and where it comes from.

## 1. Wind turbine

**Wind speed at hub height.** The weather data gives wind at 10 m and 100 m. A power law between the two gives the wind at the 64 m hub, every hour.

```math
\alpha = \frac{\ln(v_{100}/v_{10})}{\ln(100/10)} \qquad v_{hub} = v_{100}\left(\frac{64}{100}\right)^{\alpha}
```

**Air density** from the measured pressure $p$ and temperature $T$ each hour, with $R_0 = 287.05$ J/(kg K).

```math
\rho = \frac{p}{R_0\,T}
```

**Turbine output.** Thinner air carries less energy, so the wind speed is corrected for density before it is read off the manufacturer's power curve (IEC 61400-12-1).

```math
v_{eq} = v_{hub}\left(\frac{\rho}{1.225}\right)^{1/3} \qquad P_{el} = \text{PowerCurve}(v_{eq})
```

**Power in the wind and power coefficient.** $A$ is the area swept by the blades, $D = 71$ m the rotor diameter. $C_p$ can never pass the Betz limit of 16/27 = 59.3%.

```math
P_{wind} = \frac{1}{2}\,\rho\,A\,v_{hub}^{3} \qquad A = \frac{\pi D^2}{4} \qquad C_p = \frac{P_{el}}{P_{wind}} \le \frac{16}{27}
```

**Yearly efficiency and capacity factor**, summed over the 8,760 hours of the year.

```math
\eta = \frac{\sum_t P_{el}(t)}{\sum_t P_{wind}(t)} \qquad CF = \frac{\sum_t P_{el}(t)}{P_{rated}\cdot 8760}
```

**Correction to the real site.** The weather data overstates the wind on the ridge, so the modelled output is scaled to the 2,700 full load hours reported for the site (Staffell and Pfenninger 2016).

```math
E_{site} = E_{model}\cdot\frac{2700}{FLH_{model}} = E_{model}\cdot 0.879
```

## 2. Solar panel

**Efficiency and fill factor** at standard test conditions ($G = 1000$ W/m², 25 °C), from the data sheet (IEC 60904).

```math
\eta_{STC} = \frac{P_{max}}{1000\cdot A_{module}} \qquad FF = \frac{V_{mp}\,I_{mp}}{V_{oc}\,I_{sc}}
```

**Cell temperature.** The sun heats the panel above the air temperature $T_{amb}$. NOCT is the data sheet value of 45.2 °C.

```math
T_{cell} = T_{amb} + \frac{NOCT - 20}{800}\,G
```

**Panel output each hour.** Output follows the sunlight $G$ on the panel, falls by $\gamma = -0.295$ %/°C as the cell heats up, and falls again with the dust loss $SL$ (PVWatts model).

```math
P = P_{max}\,\frac{G}{1000}\,\big[1 + \gamma\,(T_{cell} - 25)\big]\,(1 - SL)
```

**Dust on the panels.** Dust from the air ($PM_{10}$) settles each dry day at a speed $v_{dep} = 0.9$ cm/s and builds up a layer $w$. A day with 5 mm of rain or more washes it off ($w = 0$). The layer is turned into a loss of output (Coello and Boyle, European version by Fernández Solas et al. 2025).

```math
w_d = w_{d-1} + v_{dep}\cdot PM_{10}\cdot 86400\ \text{s}\cdot\cos\beta \qquad SL = 0.3437\ \text{erf}\!\left(0.17\,w^{0.8473}\right)
```

**Performance ratio** (IEC 61724).

```math
PR = \frac{\text{yearly yield (kWh/kWp)}}{\text{yearly sunlight on the panel (kWh/m}^2\text{)}}
```

## 3. The island's hourly balance

**Net load.** What the renewables leave uncovered in hour $t$. Positive means a gap, negative means extra power.

```math
P_{net}(t) = L(t) - P_{RES}(t)
```

**How closely renewables follow demand** (Pearson correlation, from −1 to 1).

```math
r = \frac{\text{cov}(L, P_{RES})}{\sigma_L\,\sigma_{RES}}
```

**Hourly dispatch rule** (the HOMER load following strategy). Each hour:

1. Wind and sun supply the load directly, up to a stability limit $SNSP$ (formula below the list).
2. Extra power charges the battery, within its power and free space. What is left is switched off (curtailed).
3. A gap is filled from the battery, within its power and stored energy. What is left comes from the diesel plant.

```math
P_{direct} = \min\big(P_{RES},\ SNSP\cdot L\big)
```

The battery's stored energy changes as follows, with the round trip efficiency $\eta_{rt}$ = 91% split evenly between charging and discharging:

```math
E(t) = E(t-1) + \sqrt{\eta_{rt}}\;P_{ch}(t) - \frac{P_{dis}(t)}{\sqrt{\eta_{rt}}}
```

**Renewable share of the year.**

```math
RES\ \text{share} = \frac{\sum_t \big(P_{direct}(t) + P_{dis}(t)\big)}{\sum_t L(t)}
```

## 4. Costs

**Turning an investment into a yearly payment** (capital recovery factor). $i$ = 4% is the real interest rate, $n$ the lifetime of each item in years.

```math
CRF(i, n) = \frac{i\,(1+i)^n}{(1+i)^n - 1}
```

**Yearly cost of a system.** Each item's investment times its CRF, plus its maintenance, plus the diesel still burned.

```math
C_{year} = \sum_k \big[\,CAPEX_k\cdot CRF(i, n_k) + O\&M_k\,\big] + E_{diesel}\cdot c_{diesel}
```

**Cost per MWh** (the figure used to compare systems).

```math
LCOE = \frac{C_{year}}{\text{electricity used by the island in a year}}
```

**Battery lifetime.** Whichever ends first: 20 years, or 6,000 full cycles.

```math
n_{battery} = \min\left(20,\ \frac{6000}{\text{cycles per year}}\right)
```

**Cost of a diesel MWh.** Fuel use per MWh comes from the real 2025 data: the 5,591 t of fuel that Gorona saved, divided by the renewable MWh it delivered. Price from the EU Weekly Oil Bulletin, density 0.832 t/m³.

```math
c_{diesel} = \frac{\text{fuel use (t/MWh)}}{0.832\ \text{t/m}^3}\times\text{price (EUR/m}^3\text{)} + O\&M = 196\ \text{EUR/MWh}
```

**From 2020 to 2024 euros.** The Danish catalogue prices are in 2020 euros and are raised with the euro area price index.

```math
\text{EUR}_{2024} = \text{EUR}_{2020}\times\frac{126.07}{105.06} = \text{EUR}_{2020}\times 1.20
```

## 5. The existing plant

**Energy stored in the upper reservoir.** $V$ = 150,000 m³ of water, $H$ = 682 m of height.

```math
E = \rho_{water}\,g\,V\,H
```

**Round trip efficiency of the water storage**, measured from the 2025 grid data.

```math
\eta_{rt} = \frac{\text{energy from the water turbines}}{\text{energy used by the pumps}} = \frac{6229}{12935} = 48\%
```

**Stability limit.** $SNSP$ in the dispatch rule above is the largest share of demand that wind and sun may cover at any moment. For the existing plant it was varied from 10% to 100%. About 44% reproduces the real 2025 result. For the new system with a grid-forming battery it is set to 100%.
