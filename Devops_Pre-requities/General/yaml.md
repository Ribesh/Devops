# YAML

XML
```bash
<Servers>
    <Server>
        <name>Server1</name>
        <owner>John</owner>
        <created>12232012 </created>
        <status>active</status>
    </Server>
</Servers>
```

JSON
```bash
{
    Servers: [
        {
            name: Server1,
            owner: John,
            created: 12232012,
            status: active,
        }
    ]
}
```

YAML
```bash
Servers:
    - name: Server1
      owner: John
      created: 12232012
      status: active
```

### YAML Key Value Pair

```bash
Fruit: Apple
Vegetable: Carrot
Liquid: Water
Meat: Chicken
```

### YAML Array/Lists

```bash
Fruits:
-   Orange
-   Apple
-   Banana

Vegetables:
-   Carrot
-   Cauliflower
-   Tomato
```

### YAML Dictionary/Map

```bash
Banana:
    Calories: 105
    Fat: 0.5 g
    Carbs: 27 g

Grapes:
    Calores: 62
    Fat: 0.3 g
    Carbs: 16 g
```

### YAML Advance (Key/Value, Disctionary, Lists)

```bash
Fruits:
    - Banana:
        Calories: 105
        Fat: 0.5 g
        Carbs: 27 g
    - Grapes:
        Calores: 62
        Fat: 0.3 g
        Carbs: 16 g
```

### YAML List
```bash
- Blue Car
- Red Car
- Orage Car
- Purple Car

```

### YAML Dictionary in Dictionary
```bash
Color: Blue
Model: 
    Name: Honda
    Year: 1995
Transmissison: Manual
Price: $20,000
```


### YAML List of Dictionary
```bash
-   Color: Blue
    Model: 
        Name: Honda
        Year: 1995
    Transmissison: Manual
    Price: $20,000

-   Color: Orange
    Model: 
        Name: Honda
        Year: 1995
    Transmissison: Manual
    Price: $22,000

-   Color: White
    Model: 
        Name: Honda
        Year: 1995
    Transmissison: Manual
    Price: $19,000
```