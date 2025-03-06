# JSON PATH

## JSON PATH - Dictionaties
```bash
{
    "vehicles": {
        "car": {
            "color": "blue" ,
            "price": "$20,000"
        },
        "bus": {
            "color": "yellow",
            "price:" "$30,000"
        }
    }
}
```

### Query
Get car details
```bash
$.vehicles.car
```
Output:
```bash
[
    {
        
        "color": "blue" ,
        "price": "$20,000"
    }
]
```

Get bus details
```bash
$.vehicles.bus
```
Output:
```bash
[
    {
       "color": "yellow",
        "price:" "$30,000" 
    }
]
```

Get car's color
```bash
$.vehicles.car.color
```

Output:
```bash
[
    "blue"
]
```

## JSON PATH - Lists
```bash
[
    "car",
    "bus",
    "truck",
    "bike"
]
```

### Query
Get the 1st element
```bash
$[0]
```


Output:
```bash
["car"]
```

Get the 3rd element
```bash
$[2]
```
Output
```bash
["truck"]
```

Get the 1st and 4th element
```bash
$[0,3]
```
Output:
```bash
["car", "bike"]
```


## JSON PATH - Dictionry and List
```bash
{
  "car": {
    "color": "blue",
    "price": "$20,000",
    "wheels": [
      {
        "model": "X345ERT",
        "location": "front-right"
      },
      {
        "model": "X346GRX",
        "location": "front-left"
      },
      {
        "model": "X236DEM",
        "location": "rear-right"
      },
      {
        "model": "X987XMV",
        "location": "rear-left"
      }
    ]
  }
}
```

Get the model of 2nd wheel
```bash
$.car.wheels[1].model
```

Output:
```bash
"X346GRX"
```

## JSON PATH - Criteria
```bash
[
  12,
  43,
  23,
  12,
  56,
  43,
  93,
  32,
  45,
  63,
  27,
  8,
  78
]

```

Get all the numbers greated than 40
```bash
$[? ( @ > 40 )]
```
? = condition

@ = each element/item

Output:
```bash
[
  43,
  56,
  43,
  93,
  45,
  63,
  78
]
```

## JSON PATH - Criteria in dictiornary 
```bash
{
  "car": {
    "color": "blue",
    "price": "$20,000",
    "wheels": [
      {
        "model": "X345ERT",
        "location": "front-right"
      },
      {
        "model": "X346GRX",
        "location": "front-left"
      },
      {
        "model": "X236DEM",
        "location": "rear-right"
      },
      {
        "model": "X987XMV",
        "location": "rear-left"
      }
    ]
  }
}
```

Get the model of the rear-right wheel
```bash
$.car.wheel[?(@.location == "rear-right")].model
```