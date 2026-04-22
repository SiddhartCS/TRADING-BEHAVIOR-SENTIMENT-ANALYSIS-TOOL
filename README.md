================================================================================
TRADING BEHAVIOR & SENTIMENT ANALYSIS TOOL
================================================================================
Version: 1.0
Last Updated: 2026
Author: ATMS Trading Bot Project

================================================================================
OVERVIEW
================================================================================

This tool analyzes historical trading data against market sentiment indicators
(Fear & Greed Index) to identify patterns in trader behavior and performance.

The analysis covers:
- Performance metrics across different market sentiment conditions
- Behavioral patterns (trade frequency, leverage usage, long/short bias)
- Trader segmentation by leverage and activity levels
- Predictive modeling for trade outcome probability

================================================================================
REQUIREMENTS
================================================================================

Python Version: 3.8 or higher

Required Libraries:
- pandas >= 2.0.0
- numpy >= 1.24.0
- matplotlib >= 3.7.0
- seaborn >= 0.12.0
- scikit-learn >= 1.3.0

Installation Command:
pip install pandas numpy matplotlib seaborn scikit-learn

================================================================================
FILE STRUCTURE
================================================================================

project/
├── analysis.py                 # Main analysis script
├── historical_data.csv         # Trade history data (INPUT)
├── fear_greed_index.csv        # Sentiment data (INPUT)
├── sentiment_performance.csv   # Performance metrics by sentiment (OUTPUT)
├── trader_profiles.csv         # Individual trader profiles (OUTPUT)
├── performance_analysis.png    # Visualization (OUTPUT)
├── behaviour_analysis.png      # Visualization (OUTPUT)
├── segment_analysis.png        # Visualization (OUTPUT)
└── README.txt                  # This file

================================================================================
INPUT FILE FORMATS
================================================================================

1. historical_data.csv
   Required columns:
   - timestamp_ist          : Trade timestamp (format: DD-MM-YYYY HH:MM)
   - account                : Trader account identifier
   - coin                   : Trading pair/symbol
   - direction              : Trade direction (buy/sell)
   - side                   : Long/Short indicator
   - execution_price        : Entry price
   - size_tokens            : Position size in tokens
   - size_usd               : Position size in USD
   - closed_pnl             : Realized profit/loss
   - fee                    : Trading fees
   - start_position         : Initial position value
   - trade_id               : Unique trade identifier

2. fear_greed_index.csv
   Required columns:
   - date                   : Date (format: YYYY-MM-DD)
   - value                  : Index value (0-100)
   - classification         : Sentiment label (Extreme Fear/Fear/Neutral/Greed/Extreme Greed)

================================================================================
OUTPUT FILES
================================================================================

1. sentiment_performance.csv
   Columns:
   - classification         : Market sentiment label
   - avg_daily_pnl         : Average daily profit/loss in USD
   - total_pnl             : Total profit/loss in USD
   - avg_win_rate          : Percentage of profitable days
   - avg_trade_size        : Average trade size in USD
   - avg_trades_per_day    : Average number of trades per day

2. trader_profiles.csv
   Columns:
   - account               : Trader identifier
   - avg_leverage          : Average leverage proxy
   - total_pnl             : Total profit/loss
   - trade_count           : Total number of trades
   - lev_segment           : Leverage category (low/medium/high/extreme)
   - freq_segment          : Activity category (low/mid/high)

3. Visualization Files (PNG format):
   - performance_analysis.png  : Bar charts of PnL and win rate by sentiment
   - behaviour_analysis.png    : Trade frequency vs leverage by sentiment
   - segment_analysis.png      : PnL heatmap by sentiment and leverage segment

================================================================================
USAGE
================================================================================

1. Prepare your data files:
   - Place historical_data.csv and fear_greed_index.csv in the script directory
   - Ensure column names match the required format (case-insensitive)

2. Run the analysis:
   python analysis.py

3. Review outputs:
   - Console will display summary statistics and key insights
   - CSV files will be generated for further analysis
   - PNG files will be saved with visualizations

================================================================================
KEY METRICS EXPLAINED
================================================================================

1. Sentiment Classification (Fear & Greed Index):
   - Extreme Fear (0-20)   : Market panic, potential buying opportunity
   - Fear (21-40)          : Caution, defensive positioning
   - Neutral (41-60)       : Balanced market sentiment
   - Greed (61-80)         : Optimism, risk-on behavior
   - Extreme Greed (81-100): Euphoria, potential market top

2. Leverage Proxy:
   Calculated as: sum(|start_position|) / sum(|size_usd|)
   This estimates the effective leverage used by traders.

3. Long Bias:
   Ratio of long trades to total trades. Values >0.5 indicate bullish bias.

4. Win Rate:
   Percentage of days with positive PnL.

================================================================================
TROUBLESHOOTING
================================================================================

Issue: "File not found" error
Solution: Ensure historical_data.csv and fear_greed_index.csv are in the
          same directory as the script.

Issue: "Column not found" error
Solution: Check that column names match the expected format. The script
          converts all column names to lowercase and replaces spaces with
          underscores automatically.

Issue: Empty dataframe after filtering
Solution: Verify that your data contains trading actions (not just transfers
          or conversions). The script filters out non-trading actions.

Issue: Memory error with large dataset
Solution: The script processes data efficiently but very large files (>1M rows)
          may require additional RAM. Consider sampling your data.

================================================================================
CUSTOMIZATION
================================================================================

To modify the analysis:

1. Change sentiment thresholds:
   Edit the sentiment_map dictionary in the script.

2. Adjust trader segmentation:
   Modify the safe_qcut function parameters for different segment sizes.

3. Add new features for predictive modeling:
   Extend the 'features' list in the Predictive Modeling section.

4. Change visualization colors:
   Edit the 'colors' list in the Performance and Behaviour sections.

================================================================================
NOTES & LIMITATIONS
================================================================================

1. Data Quality:
   - Trades with missing timestamps are dropped
   - Non-trading actions (conversions, auto-deleveraging) are filtered out
   - Duplicate trade IDs are noted but not automatically removed

2. Leverage Calculation:
   - The leverage proxy is an estimate based on position start values
   - Actual leverage may differ due to margin requirements

3. Predictive Modeling:
   - Model is basic Random Forest for demonstration
   - Minimum 100 samples required for training
   - Results should be validated with out-of-sample testing

4. Sentiment Data:
   - Missing sentiment values result in those rows being dropped
   - Ensure sentiment data covers the full date range of trades


================================================================================
VERSION HISTORY
================================================================================

v1.0 (2026-04)
- Initial release
- Sentiment-based performance analysis
- Trader behavior profiling
- Segmentation by leverage and activity
- Basic predictive modeling
- Visualization exports

================================================================================
END OF README
================================================================================
