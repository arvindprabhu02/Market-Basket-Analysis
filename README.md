# Market-Basket-Analysis
# Bakery Store Layout Optimization using Association Rule Mining

## Project Overview
This project aims to optimize a bakery's store layout and cross-selling strategies by analyzing customer purchasing behavior using Association Rule Mining (ARM). By identifying frequently co-purchased items and their underlying relationships, we propose a data-driven approach to product placement, bundling, and promotional activities to enhance sales and customer experience.

## Dataset
The analysis is based on a transactional dataset from a bakery, containing `TransactionNo` and `Items` purchased over a period. The dataset was preprocessed to create a binary transactional format suitable for ARM.

*   **Original Data Range**: Filtered for rows `2655` to `14993`.
*   **Missing Values**: Rows with missing `Items` were dropped.

## Methodology

1.  **Data Preparation**: Transformed raw transaction data into a one-hot encoded 'basket' DataFrame where rows represent transactions and columns represent items, with values indicating presence (1) or absence (0).
2.  **Frequent Itemset Generation**: Used the `Apriori` algorithm to find frequent itemsets (combinations of items that frequently appear together) with a `min_support` of `0.02`.
3.  **Association Rule Generation**: Generated association rules from the frequent itemsets using a `min_threshold` of `0.1` for `confidence`.
4.  **Rule Analysis**: Interpreted rules based on:
    *   **Support**: How frequently an itemset appears in the dataset.
    *   **Confidence**: The likelihood that item Y is bought when item X is bought (P(Y|X)).
    *   **Lift**: How much more likely item Y is bought when item X is bought, compared to Y's general popularity (P(Y|X) / P(Y)).
5.  **Strategic Recommendations**: Developed store layout, bundling, and cross-selling strategies based on the insights from the analyzed rules.

## Key Findings & Insights

### Top Frequent Itemsets (Min Support: 0.02)
-   `Coffee` is the most frequent individual item.
-   `Bread` and `Tea` are also highly frequent.
-   `{Bread, Coffee}` is the most frequent two-item combination.

### Association Rules by Confidence
High-confidence rules are crucial for predicting add-on purchases:
-   `{Toast} -> {Coffee}` (Confidence: ~0.66, Lift: ~1.39)
-   `{Pastry} -> {Coffee}` (Confidence: ~0.56, Lift: ~1.19)
-   `{Medialuna} -> {Coffee}` (Confidence: ~0.56, Lift: ~1.18)
-   `{Alfajores} -> {Coffee}` (Confidence: ~0.54, Lift: ~1.15)

These rules indicate strong tendencies for customers to pair baked goods with Coffee, making them reliable for direct cross-selling.

### Association Rules by Lift
High-lift rules reveal strong, non-random associations:
-   `{Cake} -> {Tea}` (Lift: ~1.53, Confidence: ~0.22)
This rule, despite lower confidence, indicates that customers buying Cake are significantly more likely to also buy Tea than expected by chance, suggesting a strong complementary pairing for specific occasions (e.g., afternoon tea).

### Items with Low or Negative Association (Lift < 1)
-   **`Bread`**: Shows low lift when paired with popular items like `Coffee`, `Cake`, and `Tea`. This suggests 'Bread' is often a standalone purchase or for different consumption occasions.
-   **`Coffee` (as antecedent)**: `Coffee -> Bread` and `Coffee -> Tea` have lift < 1, indicating that buying Coffee does not positively predict buying Bread or Tea.

### Standalone Items
-   **`Soup`**: Despite having individual support (>0.02), `Soup` does not form any multi-item frequent itemsets above the `min_support` threshold. This implies it's largely a standalone purchase with no strong predictable co-purchases.

## Store Layout Optimization & Strategies

### Primary Item Pairings & Counter/Display Placement
Leveraging strong `antecedent -> consequent` rules, especially those leading to `Coffee`:

*   **
