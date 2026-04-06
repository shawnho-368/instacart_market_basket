# Instacart Shopping Pattern Analysis

## Overview

This project analyzes 3.4+ million Instacart orders to uncover shopping behavior patterns, with a focus on temporal trends and category performance. The analysis identifies actionable insights for operational planning, inventory management, and targeted marketing strategies. This analysis is framed from the perspective of an ops or growth team trying to allocate staffing, inventory, and marketing spend more efficiently.

**Key Question:** *When do customers shop, and how does their behavior differ between weekdays and weekends?*

## Key Findings

### Patterns
- **Peak days shift weekly:** Sunday and Monday drive the highest order volumes, suggesting customers prepare for the week ahead
- **Time-of-day varies by day type:** Weekday orders peak at 10-11 AM, while weekend orders peak 2-3 hours later at 1-3 PM
- **Consistent evening decline:** Order activity drops sharply after 5 PM across all days

### Shopping Behavior
- **Weekend stock-up effect:** Weekend baskets average 15% larger than weekdays (10.2 vs 8.9 items)
- **Late-night planning:** Orders placed 9 PM-midnight show 20% higher basket sizes despite lower volumes
- **Cross-category consistency:** Late-night basket increase spans all departments, not driven by specific categories

### Category Insights
- **Top 3 dominate:** Produce, dairy eggs, and beverages appear in 60%+ of all orders
- **Synchronized patterns:** Leading categories follow identical hourly and daily trends
- **No category-specific surges:** All departments decline uniformly after 5 PM

## Business Impact

### Operational Recommendations
| Area | Recommendation | Expected Impact |
|------|----------------|-----------------|
| **Staffing** | Peak coverage Sun/Mon 10 AM-3 PM | Match capacity to demand |
| **Inventory** | Prioritize top 3 categories during peak hours | Reduce stockouts, improve fulfillment |
| **Delivery** | Incentivize off-peak slots (Tue-Fri, after 5 PM) | Smooth demand, reduce costs |

### Marketing Opportunities
| Strategy | Timing | Rationale |
|----------|--------|-----------|
| **Promotional campaigns** | Weekdays 9-10 AM, Weekends 12-1 PM | Capture pre-peak planning window |
| **Late-night engagement** | 8-11 PM targeted messaging | Leverage high-intent, large-basket shoppers |
| **Weekly prep bundles** | Sunday morning featured placement | Align with beginning-of-week behavior |

It's worth noting that the dataset doesn't distinguish between orders placed in real time versus those scheduled in advance. This limits the confidence of demand-based recommendations, as observed order timing may not reflect actual shopping intent at that moment.

## Dataset

**Source:** [Instacart Market Basket Analysis (Kaggle)](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)

> **⚠️ Note:** Due to GitHub's file size limitations (100 MB per file), the dataset files are **not included** in this repository. You must download them separately from Kaggle to run the analysis.

### Download Instructions

1. Visit the [Instacart Market Basket Analysis dataset page](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis) on Kaggle
2. Click "Download All" (requires free Kaggle account)
3. Extract the downloaded files
4. Place the following CSV files in the `dataset/` folder:
   - `orders.csv` - Order-level metadata (3.4M orders, ~180 MB)
   - `products.csv` - Product catalog (49K products, ~2.5 MB)
   - `departments.csv` - Department taxonomy (21 departments, <1 MB)
   - `aisles.csv` - Aisle taxonomy (134 aisles, <1 MB)
   - `order_products__prior.csv` - Historical order-product relationships (32M records, ~550 MB)

**Timeframe:** Historical order data from Instacart's platform

**File size note:** `order_products__prior.csv` and `orders.csv` exceed GitHub's 100 MB file limit, which is why they must be downloaded separately.

## Methodology

### Data Preparation
1. Merged orders with product, department, and aisle information
2. Created feature engineering:
   - `day_name`: Mapped numeric day-of-week to readable names
   - `day_type`: Classified as "Weekday" or "Weekend"
   - `basket_size`: Calculated items per order

### Analysis Approach
- **Temporal aggregation:** Grouped by hour of day and day of week
- **Normalization:** Calculated per-day averages to account for 5 weekdays vs 2 weekend days
- **Category analysis:** Filtered to top-performing departments for focused insights
- **Visualization:** Created comparative plots to highlight weekday vs weekend differences

### Tools & Libraries
```python
pandas          # Data manipulation and aggregation
matplotlib      # Static visualizations
seaborn         # Statistical graphics
numpy           # Numerical operations
pathlib         # File path management
```

## Repository Structure

```
instacart-market-basket/
│
├── notebook/
│   └── instacart.ipynb          # Main analysis notebook
│
├── dataset/                      # ⚠️ Not included in repo (download from Kaggle)
│   ├── orders.csv               #    (files exceed GitHub size limits)
│   ├── products.csv
│   ├── departments.csv
│   ├── aisles.csv
│   └── order_products__prior.csv
│
├── .gitignore                    # Excludes large CSV files
└── README.md                     # This file
```

**Note:** The `dataset/` folder exists locally after you download the files from Kaggle, but these CSV files are excluded from the GitHub repository via `.gitignore` due to their size.

## How to Run

### Prerequisites
```bash
# Python 3.8 or higher
python --version

# Install required packages
pip install pandas numpy matplotlib seaborn jupyter
```

### Setup Instructions

**1. Clone the repository**
```bash
git clone https://github.com/shawnho-368/instacart_market_basket.git
cd instacart_market_basket
```

**2. Download the dataset** (REQUIRED)
- Visit [Kaggle's Instacart dataset page](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)
- Download all CSV files
- Place them in the `dataset/` folder in your local repository

Your folder structure should look like:
```
instacart_market_basket/
├── dataset/
│   ├── orders.csv                    ← Downloaded from Kaggle
│   ├── products.csv                  ← Downloaded from Kaggle
│   ├── departments.csv               ← Downloaded from Kaggle
│   ├── aisles.csv                    ← Downloaded from Kaggle
│   └── order_products__prior.csv     ← Downloaded from Kaggle
└── notebook/
    └── instacart.ipynb
```

**3. Run the analysis**
```bash
# Launch Jupyter Notebook
jupyter notebook

# Open notebook/instacart.ipynb and run all cells
```

## Visualizations

The analysis includes 11 key visualizations:

1. **Order volume by day of week** - Identifies Sunday/Monday peaks
2. **Hourly order distribution** - Compares weekday vs weekend timing
3. **Normalized order volume** - Accounts for day-count differences  
4. **Basket size comparison** - Weekend vs weekday differences
5. **Hourly basket patterns** - Reveals late-night increases
6. **Department frequency** - Top categories by order count
7. **Category hourly trends** - Time-of-day patterns for top departments
8. **Multi-department comparison** - Checks for category-specific surges
9. **Weekly department patterns** - Day-of-week trends by category

## Next Steps & Extensions

### Potential Enhancements
- [ ] Product-level time-of-day analysis (e.g., coffee peaks morning, ice cream peaks evening)
- [ ] Customer segmentation based on order frequency and basket patterns
- [ ] Predictive modeling for demand forecasting
- [ ] Investigate correlation between reorder rates and time-of-day
- [ ] Geographic analysis if location data becomes available

### Limitations
- **Customer demographics:** No age, income, or household size data to enable behavioral segmentation
- **Product quantities:** Data shows which products appear in orders but not quantities purchased
- **Temporal scope:** Analysis is limited to available historical data without seasonal trends

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Dataset provided by [Instacart via Kaggle](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)
- Analysis inspired by real-world grocery delivery operational challenges
- Tools and libraries maintained by the Python data science community

---


