# General Pre-requisites

## YAML

```yaml
# Key value pairs
Fruit: Apple
Vegetable: Carrot
Liquid: Water
Meat: Chicken

# Array/Lists
Fruit:
  - Orange
  - Apple
  - Banana
Vegetables:
  - Carrot
  - Cauliflower
  - Tomato

# Dictionary/Map
Banana:
  Calories: 105
  Fat: 0.4 g
  Carb: 27 g

# Dictionary/Map
# NOTE: must have equal spacing for fields of an item
Grapes:
  Calories: 62
  Fat: 0.3 g
  Carbs: 16 g
```

Spaces

```yaml
# Dictionary/Map
Banana:
  Calories: 105
    # Mismatched spacing would make these fields of calories
    Fat: 0.4 g
    Carb: 27 g
```

## JSON PATH

JSON PATH is a query language that helps easily extract data.

Root element signified by a `$`.
- Queries preceded by it: `$.vehicles`
- For a list `$[0]`

`?` specifies a criteria/filter
- `$[?( @ > 40)]` where `@` signifies 'each item in the lsit'
- Operator examples: `>`, `<`, `==`, `!=`, `in`, `nin`
