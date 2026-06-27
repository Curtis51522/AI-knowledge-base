# Roboflow Bakery Detection YOLO Datasets

> Searched on 2026-06-26
> Criteria: Object Detection, YOLO format, >= 10 classes

---

## Small Cakes / Pastry / Dessert Focused

| Dataset Name | Classes | Images | Author | Type | Link |
|---|---|---|---|---|---|
| yolov8-mongines | 17 | ~284 | cakepestry | Instance Seg | https://universe.roboflow.com/cakepestry/yolov8-mongines |
| NEW BAKES DATA | 14 | N/A | Annotations | Detection | https://universe.roboflow.com/annotations-lfspf/new-bakes-data |
| Bread_Classification | 12 | ~1,060 | project-zgsiw | Detection | https://universe.roboflow.com/project-zgsiw/bread_classification |
| Bread Detector | 15 | ~1,823 | breaddetector | Detection | https://universe.roboflow.com/breaddetector/bread-detector |
| Count Cake | N/A (cake counting) | ~1,079 | count-cake | Detection | https://universe.roboflow.com/count-cake/count-cake-3edxw/dataset/4 |
| Cake and CupCake | 4 (muffin/cupcake) | 100 | Alab | Detection | https://universe.roboflow.com/alab/cake-and-cupcake |

### Notes

- **yolov8-mongines**: 17 cake/pastry classes (black forest cake, rainbow pastry, butterscotch cake, etc.). 284 images. Instance segmentation format.
- **NEW BAKES DATA**: 14 chocolate/pastry classes (CHOCOLATE-ROLL, CHOCOLATE-TEACAKE, etc.).
- **Bread Detector**: 15 bread classes (mostly Philippine varieties), 1,823 images — largest dedicated baking dataset.
- **Count Cake**: 1,079 cake images — good for cake counting.
- **Cake and CupCake**: Small dataset (100 images) with muffin and cupcake classes.

---

## Broad Food Datasets (Contain Cake/Pastry/Dessert Classes)

| Dataset Name | Classes | Images | Author | Dessert-relevant classes | Link |
|---|---|---|---|---|---|
| Classes (Fooddetect) | 47 | N/A | Fooddetect | Cupcakes, Brownie, Muffins, Waffles, Pancakes, French Toast | https://universe.roboflow.com/fooddetect-8cdpw/classes-litep |
| food 101 | 101 | ~493 | Food101 Capstone | chocolate_cake, waffles, ice_cream, etc. | https://universe.roboflow.com/food101-capstone/food-101-du1wm |
| food 101 (UOM) | 101 | ~1,473 | UOM | chocolate_cake, waffles, ice_cream, etc. | https://universe.roboflow.com/uom-y4jx0/food-101-du1wm-lj8w3 |
| Prd_detection | 96 | ~10,126 | AI | cake, brownie, bun, etc. | https://universe.roboflow.com/ai-bzf1h/prd_detection |
| backery item dataset | 53 | N/A | devAmeer | BlueberryBoxCake, CoconutCake, etc. | https://universe.roboflow.com/devameer/backery-item-dataset |
| food detection (nutriment) | 77 | N/A | nutriment | Butter, naan, etc. (Indian food focused) | https://universe.roboflow.com/nutriment-eazzk/-food-detection |

---

## Baked / Bread General Datasets

| Dataset Name | Classes | Images | Author | Link |
|---|---|---|---|---|
| Bakery (pastry) | Multiple pastry | 169 | yolov8 | https://universe.roboflow.com/yolov8-zbxu8/bakery-lfpgo |
| Bakery Products | ~8 | 376 | AUDIT | https://universe.roboflow.com/audit-nsgdv/bakery-products |
| bakery (s1) | 7 | 72 | s1 | https://universe.roboflow.com/s1-s0vr8/bakery-5mrtu |
| Bakery Product Detection v25.8.31 | N/A | 139 | Count object | https://universe.roboflow.com/count-object-pvkju/bakery-product-detection-v25.8.31-cmktc |

---

## Specific Dataset Check Results

### 1. Baked Goods v8
**Status: NOT FOUND** ❌
Could not locate this dataset on Roboflow Universe. It may have been removed, renamed, or made private.

### 2. Bread Detection v2
**Status: NOT FOUND** ❌
No exact match found. A similar dataset "Bread Detection 2" exists (by YOLO, 120 images, 8 classes) but it is not the same dataset.

### 3. Pastry & Bread
**Status: NOT FOUND** ❌
Could not locate this dataset on Roboflow Universe. It may have been removed or made private.

### 4. Bakery Products
**Status: AVAILABLE** ✅
- Author: AUDIT (audit-nsgdv)
- Images: 376
- Classes: ~8 (Butter-Cookies, Chessboard-Cookies-240gm, Chessboard-Cookies-72gm, etc.)
- Link: https://universe.roboflow.com/audit-nsgdv/bakery-products
- Note: Does not meet the >= 10 classes threshold.

---

## Recommendations for Small Cake / Pastry Detection

For a **small cake / pastry detection** project with YOLO format and >= 10 classes, the top options are:

1. **yolov8-mongines** (17 cake/pastry classes, 284 images) — best thematic match, but small size
2. **NEW BAKES DATA** (14 chocolate/pastry classes) — good thematic match
3. **Classes (Fooddetect)** (47 classes with cupcake/muffin/brownie/waffle) — broad dessert coverage
4. **food 101** (various versions, 493-1,473 images) — includes chocolate cake, waffles, ice cream
5. **backery item dataset** (53 classes with multiple cake types) — largest class count for bakery items

Consider merging multiple datasets (e.g., yolov8-mongines + NEW BAKES DATA + Bread_Classification) for better coverage and image count.

---

## 6. 四种特定面包 Roboflow 检索 (2026-06-26 补充)

用户指定品类：**baguette, soboro, sourdough, pandesal**

| 品类 | Roboflow 专属数据集 | 状态 |
|------|--------------------|------|
| **baguette** 🥖 | `bakery-tkv33/baguette-owbhn` | ✅ 有专属数据集 |
| **soboro** 🍞 | 无 | ❌ 未找到（韩国酥皮面包，Roboflow 无标注） |
| **sourdough** 🍞 | 无 | ❌ 未找到（酸面包，需从通用 bread 数据集中筛选） |
| **pandesal** 🍞 | 无专属，但 `breaddetector/bread-detector`（15类，1,823图，多为菲律宾面包）可能包含 | ⚠️ 可能在 Bread Detector 中 |

### 关键发现
- **baguette** 是唯一有专属数据集的（但图片数和标注质量需浏览器确认）
- **pandesal** 大概率在 `breaddetector/bread-detector` 的 15 个菲律宾面包品类中
- **soboro** 和 **sourdough** 在 Roboflow 上完全空白，需自行标注或从通用分类中筛选

---

## 7. 已知品类总清单（跨所有检索到的数据集）

### 已确认品类（Roboflow snippet 明确列出）

| # | 品类 | 来源数据集 |
|---|------|-----------|
| 1 | bread_coconut | bakeryresearch/bakery-hbr5t (5,222 图) |
| 2 | bread_roll | bakeryresearch/bakery-hbr5t |
| 3 | chiffon | bakeryresearch/bakery-hbr5t |
| 4 | croissant | bakeryresearch/bakery-hbr5t |
| 5 | croissant_chocolate | bakeryresearch/bakery-hbr5t |
| 6 | donut | bakeryresearch/bakery-hbr5t |
| 7 | Butter-Cookies | audit-nsgdv/bakery-products (376 图, ~8 类) |
| 8 | Chessboard-Cookies-240gm | audit-nsgdv/bakery-products |
| 9 | Chessboard-Cookies-72gm | audit-nsgdv/bakery-products |

### 高价值数据集（品类数多，具体列表需浏览器确认）

| 数据集 | 品类数 | 图片数 | 备注 |
|--------|--------|--------|------|
| backery item dataset | **53** | ? | 最大品类覆盖（BlueberryBoxCake, CoconutCake 等） |
| Classes (Fooddetect) | 47 | ? | Cupcakes, Brownie, Muffins, Waffles, Pancakes 等 |
| yolov8-mongines | 17 | 284 | black forest cake, rainbow pastry, butterscotch cake 等 |
| Bread Detector | 15 | 1,823 | 菲律宾面包为主，可能含 pandesal |
| NEW BAKES DATA | 14 | ? | CHOCOLATE-ROLL, CHOCOLATE-TEACAKE 等 |
| Bread_Classification | 12 | 1,060 | — |
| Prd_detection | 96 | 10,126 | cake, brownie, bun 等（最大图片量！） |
| food 101 (UOM) | 101 | 1,473 | chocolate_cake, waffles, ice_cream 等 |


## 8. 系统实际使用的 16 品类清单 ✅

> 来源：`config/settings.py` + `data/merged_yolo/data.yaml`  
> 更新：2026-06-27

| # | 品类 | YOLO 标注名 | merged_yolo 中有 |
|---|------|------------|:---:|
| 1 | 椰子面包 | `bread_coconut` | ✅ |
| 2 | 面包卷 | `bread_roll` | ✅ |
| 3 | 戚风蛋糕 | `chiffon` | ✅ |
| 4 | 可颂 | `croissant` | ✅ |
| 5 | 巧克力可颂 | `croissant_chocolate` | ✅ |
| 6 | 甜甜圈 | `donut` | ✅ |
| 7 | 蛋挞 | `eggtart` | ✅ |
| 8 | 奶油角 | `cream_horn` | ✅ |
| 9 | 哈密瓜面包 | `melon_bread` | ✅ |
| 10 | 披萨面包 | `pizza_bread` | ✅ |
| 11 | 酥皮面包 (Soboro) | `soboru_bread` | ✅ |
| 12 | 巧克力派 | `chocopie` | ✅ |
| 13 | 棒形面包 | `stickbread` | ✅ |
| 14 | 法棍 | `baguette` | ✅ |
| 15 | 菲律宾甜面包 | `pandesal` | ✅ |
| 16 | 酸面包 | `sourdough` | ✅ |

**merged_yolo 共 28 类**，系统取其中 16 类，多出的 12 类为菲律宾面包（binangkal, bonete, cornbread, ensaymada, flatbread, kalihim, monay, spanish-bread, wheat-bread, white-bread, whole-grain-bread, bagel）。

---

## 9. 中国烘焙店销售记录数据集（待 Codex 补充）

> 2026-06-27：所有外部 API（Kaggle, GitHub, HuggingFace, CORE, Tianchi, Google）均被拦截。
> 委托 Codex 搜索以下方向：

- Kaggle: `bakery sales transaction dataset`, `french bakery sales`
- GitHub: `bakery sales csv`, `transaction data`
- 阿里天池 (Tianchi): `烘焙 销售 数据`
- 和鲸社区 (HeyWhale): `面包店 销售记录`
- UCI ML Repository: retail transaction datasets
- 目标：CSV格式，含日期/产品/数量/金额字段，最好是中国烘焙店真实数据


