# Visualization — Matplotlib & Seaborn (Theory and Best Practices)

Purpose: Guidance on visualizing finance data clearly and correctly using `matplotlib` and `seaborn`.

## Overview
- `matplotlib` is the foundational plotting library; `seaborn` builds on it and provides statistical plotting conveniences and nicer defaults.
- Focus on time-series charts, aggregated bar/column charts, histograms, boxplots for outliers, and heatmaps for correlation matrices.

## Common plots for finance
- Line chart for time series: `plt.plot()` or `df.plot()` with `DatetimeIndex`
- Bar chart for categorical totals: `sns.barplot` or `df.groupby().sum().plot(kind='bar')`
- Histogram for distributions: `plt.hist()` or `sns.histplot()`
- Boxplot for detecting outliers: `sns.boxplot()`
- Heatmap for correlation: `sns.heatmap(df.corr(), annot=True)`

Best practices
- Always label axes and add a clear title; include units (e.g., USD)
- Convert dates to `DatetimeIndex` and resample before plotting high-frequency data (e.g., daily → monthly)
- Use aggregation (`groupby`, `resample`) to reduce noise and overplotting
- Use colorblind-friendly palettes: `sns.color_palette('colorblind')`
- Save figures with adequate DPI and size: `plt.savefig('chart.png', dpi=200)`
- Prefer `seaborn` for quick stylized plots, but drop to `matplotlib` for fine-grained control

Common mistakes
- Plotting raw tick-level data without aggregation, producing unreadable charts
- Using default colors and small fonts that fail in presentations
- Over-plotting too many series on one axis without normalization or separate axes
- Forgetting to sort by date before plotting time series

Visualization workflow
1. Prepare aggregated DataFrame (resample or groupby)
2. Choose chart type that fits the question
3. Format axes, labels, legend, and tick frequency
4. Save and review in the target medium (slide, report, web)

References
- Matplotlib: https://matplotlib.org/
- Seaborn: https://seaborn.pydata.org/