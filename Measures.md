# Measures Documentation

---

### Net Revenue

**DAX**

```
SUM(fFreight[Net Revenue])
```

**Description:** Total net revenue from all freight shipments.

---

### Number of Freights

**DAX**

```
DISTINCTCOUNT(fFreight[Freight ID])
```

**Description:** Count of unique freight shipments.

---

### Distance (miles)

**DAX**

```
SUM(fKMTraveled[KM Traveled]) * 0.621
```

**Description:** Total distance traveled in miles (converted from km).

---

### Weight (tons)

**DAX**

```
SUM(fFreight[Weight (Kg)]) / 1000
```

**Description:** Total freight weight in metric tons (kg → tons).

---

### Total Fixed Cost

**DAX**

```
SUM(fKMTraveled[Fixed Costs])
```

**Description:** Sum of fixed transport costs (e.g., lease, depreciation).

---

### Total Variable Cost

**DAX**

```
SUM(fKMTraveled[Fuel]) + SUM(fKMTraveled[Maintenance])
```

**Description:** Sum of variable costs (fuel + maintenance).

---

### Total Cost

**DAX**

```
[Total Fixed Cost] + [Total Variable Cost]
```

**Description:** Overall transport cost (fixed + variable).

---

### Cost Per Mile

**DAX**

```
DIVIDE([Total Cost], [Distance(mile)], 0)
```

**Description:** Average cost to move one mile.

---

### Cost Per Ton

**DAX**

```
DIVIDE([Total Cost], [Weight(ton)], 0)
```

**Description:** Average cost to move one ton.

---

### Maintenance Cost

**DAX**

```
SUM(fKMTraveled[Maintenance])
```

**Description:** Total maintenance expenditures.

---

### Fuel Cost

**DAX**

```
SUM(fKMTraveled[Fuel])
```

**Description:** Total fuel expenditures.

---

### Number of Trucks Used

**DAX**

```
DISTINCTCOUNT(fFreight[Truck ID])
```

**Description:** Number of distinct trucks used in the period.

---

### Profit

**DAX**

```
[Net Revenue] - [Total Cost]
```

**Description:** Net profit (revenue minus total cost).

---

### Profit %

**DAX**

```
DIVIDE([Profit], [Net Revenue], 0)
```

**Description:** Profit as a percentage of net revenue.

---

### Revenue LY

**DAX**

```
diffFromLY([Net Revenue])
```

**Description:** Revenue change vs. same period last year.

---

### Cost LY

**DAX**

```
diffFromLY([Total Cost])
```

**Description:** Cost change vs. same period last year.

---

### Weight LY

**DAX**

```
diffFromLY([Weight(ton)])
```

**Description:** Weight change vs. same period last year.

---

### Freights LY

**DAX**

```
diffFromLY([#Freights])
```

**Description:** Freight count change vs. same period last year.

---

### Revenue LM

**DAX**

```
diffFromLM([Net Revenue])
```

**Description:** Revenue change vs. last month.

---

### Revenue Color LY

**DAX**

```
colorLY([Net Revenue])
```

**Description:** Visual color flag for revenue vs. last year (e.g., Red/Green/Grey).

---

### Cost Color LY

**DAX**

```
VAR cy = [Total Cost]
VAR ly = CALCULATE(
    [Total Cost],
    SAMEPERIODLASTYEAR('Calendar'[Date])
)

VAR diffperc = DIVIDE(
    cy - ly,
    ly
)

RETURN
IF(
    AND(
        ISFILTERED('Calendar'[Year]),
        SELECTEDVALUE('Calendar'[Year]) <> 2018
    ),
    SWITCH(
        TRUE(),
        diffperc > 0, "Red",
        diffperc < 0, "Green",
        "Grey"
    ),
    ""
)
```

**Description:** Color flag for cost vs. last year: Red if higher, Green if lower, Grey otherwise (with year filters).

---

### Cost Color LM

**DAX**

```
VAR CM = [Total Cost]
VAR LM = CALCULATE(
    [Total Cost],
    DATEADD('Calendar'[Date], -1, MONTH)
)

VAR diffperc = DIVIDE(
    CM - LM,
    LM
)

RETURN
IF(
    AND(
        ISFILTERED('Calendar'[Month]),
        NOT(
            SELECTEDVALUE('Calendar'[Year]) = 2018 &&
            SELECTEDVALUE('Calendar'[MonthNumber]) = 1
        )
    ),
    SWITCH(
        TRUE(),
        diffperc > 0, "Red",
        diffperc < 0, "Green",
        "Grey"
    ),
    ""
)
```

**Description:** Color flag for cost vs. last month with month/year exclusions.

---

### Cost LM

**DAX**

```
diffFromLM([Total Cost])
```

**Description:** Cost change vs. last month.

---

### Weight LM

**DAX**

```
diffFromLM([Weight(ton)])
```

**Description:** Weight change vs. last month.

---

### Weight LM Color

**DAX**

```
ColorLM([Weight(ton)])
```

**Description:** Visual color flag for weight vs. last month.

---

### Weight LY Color

**DAX**

```
colorLY([Weight(ton)])
```

**Description:** Visual color flag for weight vs. last year.

---

### Freights LM

**DAX**

```
diffFromLM([#Freights])
```

**Description:** Freight count change vs. last month.

---

### Freights LY Color

**DAX**

```
colorLY([#Freights])
```

**Description:** Visual color flag for freights vs. last year.

---

### Freights LM Color

**DAX**

```
ColorLM([#Freights])
```

**Description:** Visual color flag for freights vs. last month.

---

### Revenue Color LM

**DAX**

```
ColorLM([Net Revenue])
```

**Description:** Visual color flag for revenue vs. last month.

---

### Profit Color

**DAX**

```
colorLY([Profit])
```

**Description:** Visual color flag for profit vs. last year.

---

### All Trucks

**DAX**

```
COUNT(dVeiculo[Truck ID])
```

**Description:** Total trucks in the fleet (master table count).

---

### Trucks %

**DAX**

```
DIVIDE([#Trucks Used], [All Trucks])
```

**Description:** Share of fleet that was used.

---

### Avg Trip Distance

**DAX**

```
DIVIDE([Distance(mile)], [#Freights])
```

**Description:** Average distance per freight trip (miles).

---

### Avg Trip Weight

**DAX**

```
DIVIDE([Weight(ton)], [#Freights])
```

**Description:** Average weight per freight trip (tons).

---

