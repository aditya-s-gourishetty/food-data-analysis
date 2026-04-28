# Ingredient Similarity and Procedure in Recipes

This project studies how ingredient structure and cooking procedure relate to each other in recipe data. I used the Food.com recipe dataset to analyze the same recipe space through three connected views: recipe clustering, frequent ingredient itemsets with recurring action subsequences, and ingredient-similarity graph communities with text topics. The main result is that ingredient similarity is meaningful, but it does not determine procedure in a simple one-to-one way. Some ingredient sets, especially specific baking combinations, behave almost like a procedural blueprint, while broad savory ingredient bases allow several different cooking paths.

👉 Start here: `main_notebook.ipynb`

Video: https://www.youtube.com/watch?v=rm46rBcp3hg

## Research questions

1. How much agreement is there between recipe clusters built from ingredient features and recipe clusters built from step-text features?

2. Among recipes sharing a frequent ingredient itemset, what frequent step subsequences recur, and how concentrated are those procedural patterns?

3. Do recipe groups formed from ingredient similarity align with text topics from recipe descriptions and steps?

## Results summary

The three research questions all pointed to the same high-level conclusion: ingredients matter, but they do not determine cooking procedure uniformly across the dataset.

RQ1 showed that ingredient-based clusters and step-text-based clusters had only modest overall agreement, but the overlap was not random. Baking-oriented ingredient groups aligned more clearly with baking-style procedure groups, while broad savory ingredient groups spread across several cooking styles.

RQ2 showed that some ingredient sets behave almost like a recipe blueprint. Specific baking triples such as `egg + sugar + vanilla` were strongly tied to narrow recurring subsequences like `mix -> bake`. In contrast, savory aromatic sets such as `garlic + olive oil + onion` still had recurring structure, but supported a broader set of step patterns such as `mix -> simmer` and `simmer -> serve`.

RQ3 showed that ingredient-similarity communities aligned with text topics mainly at the level of broad recipe families such as soups, desserts, breads, salads, and savory mains. But even the largest ingredient communities still spread across several text topics, which means similar ingredients often support different dish forms and preparation styles.

## Data

This project uses the Food.com recipe dataset from Kaggle.

- Dataset: `shuyangli94/food-com-recipes-and-user-interactions`
- Main file used: `RAW_recipes.csv`
- Additional processed interaction files were downloaded with the dataset, but the main analysis in this project focuses on the recipe side

The notebook builds a shared cleaned recipe table and then applies RQ-specific representations on top of it. Shared preprocessing includes parsing ingredient and step columns into lists, cleaning description and step text, removing ingredient words from step text for procedure-focused text views, and building combined text fields used in RQ1 and RQ3. RQ2 adds stronger ingredient normalization because Apriori depends directly on exact item matching, and it converts recipe steps into normalized action sequences for sequence mining.

## How to reproduce


Environment used:
- Python `3.12.13`
- Full package list: `requirements.txt`

To reproduce:
1. Open `main_notebook.ipynb` in Google Colab.
2. Install dependencies from `requirements.txt` if needed.
3. Download the Kaggle dataset `shuyangli94/food-com-recipes-and-user-interactions`.
4. Update any dataset paths in the notebook if needed.
5. Run `main_notebook.ipynb` from top to bottom.

## Key dependencies

Important packages used in this project:
- Python `3.12.13`
- `numpy==2.0.2`
- `pandas==2.2.2`
- `scikit-learn==1.6.1`
- `networkx==3.6.1`
- `scipy==1.16.3`
- `matplotlib==3.10.0`
- `mlxtend==0.23.4`
- `prefixspan==0.5.2`
- `kaggle==2.0.1`

The full environment is in `requirements.txt`.

## Repo structure

```text
.
├── README.md
├── requirements.txt
├── main_notebook.ipynb
├── checkpoints/
│   ├── checkpoint_1.ipynb
│   └── checkpoint_2.ipynb