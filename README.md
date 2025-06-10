# Rooftop-Solar-PV-System-Design-Simulation



## 📌 Overview
This project simulates the design of a rooftop solar PV system for a 3BHK residential building using site-based assumptions. It includes PV sizing, energy yield simulation, financial analysis, and documentation.

---

## 🏠 Assumptions
```python
# Rooftop Area (sq.m)
rooftop_area = 80  # 80 sq.m of usable space

# Panel Parameters
panel_capacity_kw = 0.33   # 330W panel
panel_area = 2             # 2 sq.m per panel
efficiency = 0.18          # 18% typical

# Site Conditions
average_solar_irradiance = 5  # kWh/m2/day
system_loss = 0.2             # 20% total system losses

# Cost & Tariff
cost_per_kw = 50000           # INR per kW installed
electricity_tariff = 7        # INR/kWh
```

---

## 🧼 PV Sizing & Energy Yield Estimation
```python
import math
import pandas as pd

# PV Sizing Calculations
num_panels = math.floor(rooftop_area / panel_area)
total_capacity_kw = num_panels * panel_capacity_kw
daily_energy_kwh = total_capacity_kw * average_solar_irradiance * (1 - system_loss)
monthly_energy_kwh = daily_energy_kwh * 30
annual_energy_kwh = monthly_energy_kwh * 12

print("Number of Panels:", num_panels)
print("Total Installed Capacity (kW):", total_capacity_kw)
print("Estimated Daily Energy Output (kWh):", daily_energy_kwh)
print("Estimated Annual Energy Output (kWh):", annual_energy_kwh)

# Create a table of monthly outputs assuming minor degradation
monthly_output = [monthly_energy_kwh - i * 20 for i in range(12)]
months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]

output_df = pd.DataFrame({"Month": months, "Estimated Energy Output (kWh)": monthly_output})
print("\nMonthly Energy Output Table:\n")
print(output_df.to_string(index=False))
```

---

## 💰 Financial Estimation
```python
# CAPEX
system_cost = total_capacity_kw * cost_per_kw

# Yearly savings
annual_savings = annual_energy_kwh * electricity_tariff

# Payback period
payback_years = round(system_cost / annual_savings, 2)

print("System Cost (INR):", system_cost)
print("Annual Savings (INR):", annual_savings)
print("Payback Period (Years):", payback_years)
```

---

## 📊 Data Visualization (Optional)
```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10,6))
plt.bar(output_df["Month"], output_df["Estimated Energy Output (kWh)"], color='orange')
plt.title("Estimated Monthly Solar Energy Output")
plt.xlabel("Month")
plt.ylabel("Energy (kWh)")
plt.grid(True)
plt.tight_layout()
plt.show()
```

---

## 📄 Deliverables
- PV system sizing script (this file)
- Yield simulation chart
- Monthly output table
- Financial summary
- PDF report (optional)

---

## ✅ Tools Used
- Python (math, pandas, matplotlib)
- Excel (for manual validation)
- PVsyst (optional, for advanced simulation)
- Google Maps (for rooftop area estimation)
