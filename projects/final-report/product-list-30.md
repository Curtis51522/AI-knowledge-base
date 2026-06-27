# Final 30-Product List

> Confirmed 2026-06-27

## Source Breakdown

| Source | Count |
|--------|:----:|
| Existing YOLO + Roboflow | 16 |
| French Bakery + Roboflow | 4 |
| food-101 + Roboflow | 10 |
| **Total** | **30** |

---

## Complete List

### Group A — Existing 16 (have Roboflow, merged_yolo confirmed)

| # | Product Key | Display Name | French Bakery Map |
|---|------------|-------------|-------------------|
| 1 | donut | Donut | — |
| 2 | eggtart | Egg Tart | — |
| 3 | croissant | Croissant | CROISSANT (11,508) |
| 4 | cream_horn | Cream Horn | — |
| 5 | bread_coconut | Coconut Bread | — |
| 6 | melon_bread | Melon Bread | — |
| 7 | bread_roll | Bread Roll | — |
| 8 | pizza_bread | Pizza Bread | — |
| 9 | chiffon | Chiffon Cake | — |
| 10 | croissant_chocolate | Chocolate Croissant | PAIN AU CHOCOLAT (10,578) |
| 11 | soboru_bread | Soboro Bread | — |
| 12 | chocopie | Choco Pie | — |
| 13 | stickbread | Stick Bread | — |
| 14 | baguette | Baguette | BAGUETTE (15,292) |
| 15 | pandesal | Pandesal | — |
| 16 | sourdough | Sourdough | — |

### Group B — French Bakery + Roboflow (4)

| # | Product Key | Display Name | French Bakery |
|---|------------|-------------|---------------|
| 17 | cookie | Cookie | COOKIE (2,002) |
| 18 | brioche | Brioche | BRIOCHE (1,657) |
| 19 | brownie | Brownie | BROWNIES (38) |
| 20 | macaron | Macaron | MACARON (132) |

### Group C — food-101 + Roboflow (10)

| # | Product Key | Display Name | French Bakery Map |
|---|------------|-------------|-------------------|
| 21 | apple_pie | Apple Pie | CHAUSSON AUX POMMES (1,442) |
| 22 | cheesecake | Cheesecake | synthetic |
| 23 | chocolate_cake | Chocolate Cake | FONDANT CHOCOLAT (218) |
| 24 | cupcake | Cupcake | synthetic |
| 25 | tiramisu | Tiramisu | synthetic |
| 26 | waffle | Waffle | synthetic |
| 27 | red_velvet_cake | Red Velvet Cake | synthetic |
| 28 | carrot_cake | Carrot Cake | synthetic |
| 29 | churros | Churros | synthetic |
| 30 | creme_brulee | Creme Brulee | synthetic |

---

## Data Source Summary

| Data Type | Products | Count |
|-----------|----------|:----:|
| French Bakery real sales | croissant, baguette, croissant_chocolate, cookie, brioche, brownie, macaron, apple_pie, chocolate_cake | 9 |
| Synthetic (from similar template) | All others | 21 |

## Roboflow YOLO Source

| Dataset | Classes Used |
|---------|-------------|
| `bakeryresearch/bakery-hbr5t` (5,222 img) | bread_coconut, bread_roll, chiffon, croissant, croissant_chocolate, donut |
| `Bread Detector` (15 cls, 1,823 img) | pandesal |
| `Bread_Classification` (12 cls, 1,060 img) | sourdough, baguette |
| `Prd_detection` (96 cls, 10,126 img) | brownie, cake types |
| `food-101` (101 cls, 101K img) | apple_pie, cheesecake, chocolate_cake, cupcake, tiramisu, waffle, red_velvet_cake, carrot_cake, churros, creme_brulee |
| `cookies-zugla` (548 img) | cookie |
| `donut-macaron-cookie` | macaron |
| Custom | eggtart, cream_horn, melon_bread, pizza_bread, soboru_bread, chocopie, stickbread |
