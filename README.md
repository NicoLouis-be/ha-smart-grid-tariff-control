Home Assistant – Dynamic Tariff Energy Control
Smart energy flow control for households with solar panels, home batteries, EV charging, and heat pumps, optimized for dynamic electricity tariffs.
This repository provides Home Assistant automations that dynamically decide when to:

inject electricity into the grid,
consume electricity from the grid,
charge or hold batteries,
shift flexible loads such as EV charging and heat pump operation,

all based on real‑time import and export electricity prices.

🚀 Project Goals

Maximize financial return under dynamic pricing
Prevent costly grid injection during negative export prices
Increase self‑consumption of solar energy
Automatically adapt energy behavior without manual intervention
Provide a transparent and extendable reference setup for Home Assistant users


🏠 System Overview
This project is designed around the following hardware setup:

☀️ Solar PV system

Peak production: 5 kW


🔋 2 plug‑in batteries

Max charge / discharge: 2.5 kW each


🚗 Electric Vehicle (EV)
🌡 Heat pump

Domestic hot water
Floor heating


⚡ Dynamic electricity contract

Import and export prices vary independently
Prices can be positive or negative




🤖 Included Automations
The repository contains three Home Assistant automations, each corresponding to a tariff situation commonly found in dynamic electricity markets.
The automations run continuously and evaluate:

current import & export price
solar production
battery state of charge
available flexible loads


🧠 Energy Control Logic
Phase 1 – Pay to Consume, Get Paid to Inject
Situation

Import price > 0
Export price > 0

Strategy

Prioritize self‑consumption
Inject excess solar energy into the grid
Avoid unnecessary grid consumption

This is the “classic” operating mode where solar surplus is profitable to export.

Phase 2 – Pay to Consume and Pay to Inject
Situation

Import price > 0
Export price < 0

Exporting power costs money and should be avoided.
This phase is split into three sub‑phases depending on battery capacity.
Phase 2.1 – Both batteries not full

Excess solar power is used to charge both batteries
Grid injection is fully avoided

Phase 2.2 – One battery full

Remaining battery continues charging
Flexible loads (EV / heat pump) are enabled if possible
Grid injection is still minimized

Phase 2.3 – Both batteries full

Batteries can no longer absorb excess power
Flexible loads are prioritized
Limited grid injection may occur as a last resort


Phase 3 – Get Paid to Consume, Pay to Inject
Situation

Import price < 0
Export price < 0

Strategy

Actively consume electricity from the grid
Charge batteries from the grid
Run EV charging and heat pump loads
Avoid solar injection as much as possible

This phase takes advantage of negative electricity prices on the consumption side.

📊 Energy Flow Example
The figure below shows a real‑world day of power flow (kW):

Positive values → grid injection
Negative values → grid consumption
Colored areas represent interaction between solar production, batteries, and grid

Operating phases are clearly marked to show how the automations react to changing tariff conditions.
vermogen.png

🧩 Requirements
To use or adapt these automations, you will typically need:

Home Assistant
Sensors for:

solar production
battery state of charge
grid import/export power
dynamic import & export prices


Entities to control:

battery charging
EV charging
heat pump (or other shiftable loads)



Exact integrations depend on your hardware and energy provider.

🔧 Customization
This project is intentionally modular:

Battery thresholds can be adjusted
Power limits are configurable
Additional loads can be added easily
Logic can be extended with forecasts or day‑ahead pricing

It is meant to be adapted, not copied blindly.

⚠️ Disclaimer
This project controls energy flows that can have financial consequences.
Always validate behavior with simulations, logs, and limits before running unattended.
