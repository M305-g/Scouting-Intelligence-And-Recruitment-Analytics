# Scouting-Intelligence-And-Recruitment-Analytics: Identifying High-Value Transfer Opportunities Through Performance and Market Analysis

A data-driven football scouting project integrating player performance, market valuation, and transfer history to identify high-value recruitment opportunities and support evidence-based decisions on player recruitment, retention, monitoring, and transfer review.

**Executive Summary**

I built a scouting and recruitment framework that weighs a player's sporting performance against their market value and transfer history — designed to give recruitment teams evidence to work from instead of gut feel or reputation. The analysis integrates player profiles, competition-level performance records, historical market valuations, and transfer history to move beyond simple performance rankings and provide a more objective basis for recruitment, retention, and squad investment decisions.

Using Python, performance records were aggregated to the player-season level and aligned with the latest available market valuation within the relevant season. A composite Sporting Value Score was developed from key performance indicators, while market-value bands and performance bands were used to classify player value. The analysis identified substantial variation between sporting performance and market valuation, demonstrating that strong sporting output does not consistently translate into proportionally high market value. Spearman correlation confirmed a statistically significant positive association between sporting contribution and market valuation (ρ = 0.304, p < 0.001), but the relatively modest strength of the relationship indicates that market value is influenced by factors beyond sporting output alone.

For recruitment intelligence, the analysis further examined transfer characteristics and long-term recruitment outcomes. Statistical analysis confirmed that transfer type and transfer-fee category are associated with long-term success. Conventional transfers showed a statistically significant association with success compared with drafts, while transfer-fee groups between 1M and 10M demonstrated approximately three times the odds of long-term success compared with zero-fee transfers. However, the low model pseudo-R² (0.0115) indicates that transfer characteristics alone explain only a small proportion of the variation in long-term success.

The resulting scouting framework translates these findings into practical player classifications: Retain, Recruit, Monitor, and Transfer Review. Among the final actionable player-season records, 28.10% were classified as Retain, 23.18% as Recruit, 42.53% as Monitor, and 6.19% as Transfer Review. These classifications provide the sporting director and recruitment department with an evidence-based screening framework for identifying potential recruitment opportunities, protecting high-value sporting assets, and flagging players whose financial valuation may require further review.

Overall, the project demonstrates how performance data, market valuation, and transfer history can be integrated into a practical scouting intelligence workflow, supporting recruitment decisions with quantitative evidence rather than relying solely on individual performance statistics or market price.

**Impact of the Project**

The project demonstrates how football data can be transformed from large, fragmented datasets into actionable scouting intelligence.

The framework supports three practical areas:

Identification of players with strong sporting value relative to market valuation.
Evaluation of transfer characteristics associated with long-term recruitment success.
Classification of player-seasons into scouting decisions such as Recruit, Retain, Monitor and Transfer Review.

**What I Have Contributed to This Project**

I contributed to the complete analytical workflow, including:

Data quality assessment and cleaning.
Standardization of player, season and performance information.
Player-season aggregation.
Integration of performance, market-value and transfer information.
Feature engineering for sporting value and market-value analysis.
Exploratory data analysis.
Statistical testing of relationships identified during EDA.
Development of an objective scouting decision framework.
Power BI dashboard development for communicating confirmed analytical findings.
Translation of statistical results into recruitment-oriented insights and recommendations.


**Project Objective**

To integrate player performance, market valuation and transfer history into a scouting intelligence framework that supports evidence-based recruitment, contract renewal and squad investment decisions.

**Research Questions**
   
Which players provide the highest sporting value relative to their market valuation?
Which transfer characteristics are associated with successful long-term recruitment outcomes?
Which players should be retained, recruited or transferred based on objective performance and financial evidence?

   **Stakeholders**
   
Sporting Director

Recruitment Department


**Dataset Overview**

The project integrates four datasets:

Dataset	Raw Structure	Final Structure
Player Profiles	92,671 × 34	92,671 × 20
Player Performance	1,878,719 × 20	1,878,719 × 16
Player Market Value	901,429 × 10	901,429 × 10
Transfer History	1,101,440 × 3	1,101,317 × 3

The datasets provide complementary information covering player identity and characteristics, sporting output, financial valuation and historical transfer activity.

**Tools & Technologies**

Python — Beginner to Intermediate

Used for:

Data cleaning

Data transformation

Data integration

Feature engineering

Exploratory data analysis

Statistical analysis

Power BI

Used for:

Interactive visualization
Scouting intelligence dashboards
Player segmentation
Communication of confirmed findings
Stakeholder-oriented decision support
9. Data Preparation & Cleaning
Player Profiles

The original Player Profiles dataset contained 92,671 rows and 34 columns.

Data preparation included:

Data-type assessment and correction.
Conversion of date fields such as date of birth and joining information.
Missing-value assessment.
Position standardization.
Creation of position_group.
Foot standardization.
Citizenship assessment.
Current-club status classification.
Assessment of contract-related fields.
Removal of agreed non-essential columns.

The final cleaned Player Profiles dataset contained 92,671 rows and 20 columns.

**Player Performance**

The original Player Performance dataset contained 1,878,719 rows and 20 columns.

Data preparation included:

Duplicate assessment.
Missing-value investigation.
Standardization of season names to YY/YY.
Assessment of competition and team-level records.
Removal of non-required columns.
Retention of relevant performance and disciplinary variables.
Treatment of missing goals and minutes_played.
Correction of invalid goals_conceded = -1 values to NaN.

The final cleaned Player Performance dataset contained 1,878,719 rows and 16 columns.

**Player Market Value**

The original Player Market Value dataset contained 901,429 rows and 10 columns.

The dataset was assessed and prepared for player-season market-value integration, including conversion of the valuation date information into a usable date format.

The final dataset retained 901,429 rows and 10 columns.

**Transfer History**

The original Transfer History dataset contained 1,101,440 rows and 3 columns.

Duplicate assessment identified 123 duplicate records, which were removed.

The final Transfer History dataset contained:

1,101,317 rows × 3 columns.

**Data Integration**

Player performance records were initially recorded at competition/team level. These were aggregated to the player-season level, producing 784,260 unique player-season records.

Market valuations were aligned to player-seasons using the latest available valuation on or before the end of the relevant season.

This produced market-value information for 553,640 player-seasons, while 230,620 player-seasons had no available market valuation.

The integrated player-value dataset was subsequently filtered for reliable performance and valuation information before developing the sporting-value and scouting framework.

Transfer information was separately integrated with player performance to evaluate transfer characteristics and their relationship with long-term recruitment outcomes.


**Exploratory Data Analysis — EDA 1–7**

    
EDA 1 — Data Preparation & Understanding

The four datasets operate at different observation levels and cover different time periods. Player performance contains multiple records for players within the same season because of competition and team participation.

After aggregation, 784,260 player-season records were identified. Market valuation was temporally aligned with these player-seasons, resulting in 553,640 player-seasons with available market valuations.

Insight: Careful player-season aggregation and temporal alignment were necessary before comparing sporting performance with financial valuation.

EDA 2 — Sporting Performance

Player-season sporting performance was represented through appearances, goals, assists and minutes played.

The analysis identified substantial variation in sporting output, including exceptionally high goal-and-assist contributions. The highest combined goal-and-assist contribution observed was 102.

Repeated high-performing player-seasons were also observed for some players across different seasons.

Insight: This told me goals alone were a poor proxy for contribution — I needed to combine several indicators to get a fair read on a player's value."

EDA 3 — Sporting Performance vs Market Value

High sporting output was associated with substantially different market valuations. Player-seasons with similarly high goal contributions could have markedly different market values.

Spearman rank correlation confirmed a statistically significant positive association between sporting contribution and market valuation:

ρ = 0.304, p < 0.001

Insight: Higher sporting output tends to be associated with higher market valuation, but the relationship is not strong enough to conclude that sporting performance alone determines market value.

This supports the project's Q1 approach of assessing sporting value relative to financial valuation, rather than simply ranking players by performance.

EDA 4 — Transfer Market Profile

The Transfer History dataset contains four transfer categories:

Transfer: 844,401
Loan: 128,079
Return from loan: 127,665
Draft: 1,172

Transfer fees were highly concentrated at zero, with 1,061,320 records having a transfer fee of zero.

The dataset covers 62 seasons, from 00/01 through 25/26.

Insight: A transfer record does not necessarily represent a paid transfer. Transfer type and transfer-fee status therefore need to be interpreted separately when assessing recruitment outcomes.

EDA 5 — Transfer Characteristics & Long-Term Recruitment Success

Observed long-term success differed across transfer-fee groups.

The long-term success proportions were:

0 fee: 8.02%
1M or below: 21.29%
1M–5M: 22.53%
5M–10M: 22.65%
Above 10M: 18.03%

Transfer type also showed different observed success proportions:

Transfer: 9.01%
Return from loan: 7.07%
Loan: 6.68%
Draft: 5.63%

Statistical analysis confirmed that transfer characteristics were associated with long-term recruitment success.

Compared with the 0-fee reference group, all non-zero fee groups had statistically significant associations with long-term success, with the 1–10M groups showing approximately three times the odds of success.

For transfer type, conventional Transfer was statistically significant relative to Draft, while Loan and Return from loan were not statistically significant at the 0.05 level.

Insight: Transfer-fee category provides stronger evidence of association with long-term success than transfer type in this analysis. However, transfer characteristics alone explain only a small proportion of the variation in recruitment success.

EDA 6 — Scouting Intelligence & Player Value

The integrated player-value dataset contained 261,158 player-season observations after filtering.

The sporting-value score had:

Mean: 50.00
Median: 49.88
Minimum: 7.65
Maximum: 90.73

Market value had:

Mean: 1,721,902
Median: 350,000
Minimum: 10,000
Maximum: 200,000,000

The correlation between sporting-value score and raw market value was 0.195, while the correlation with log market value was 0.340.

Players were classified into performance and market-value bands and subsequently assigned scouting decisions.

Among the actionable player-seasons:

Monitor: 72,655 — 42.53%
Retain: 47,998 — 28.10%
Recruit: 39,592 — 23.18%
Transfer Review: 10,571 — 6.19%

The Sporting Value Score was constructed from key player-performance indicators including goals, assists, appearances, and minutes played, with disciplinary variables considered separately rather than allowing cards to dominate the overall score. The indicators were normalized before being combined so that variables measured on different scales could contribute comparably to the final score. Greater weight was given to direct sporting contributions such as goals and assists, while appearances and minutes played captured player involvement and consistency. This weighting was selected to balance measurable on-pitch output with sustained participation, providing a practical performance-based measure for comparing players across the scouting dataset.


Insight: Sporting value and market valuation are related but not interchangeable. The relatively modest correlation supports the use of a combined performance-financial framework for scouting decisions.

EDA 7 — Transfer Fees & Sporting Performance

Among transfer records linked with performance data, player sporting performance varied across transfer types.

Mean sporting-value scores were:

Draft: 44.27
Loan: 48.54
Return from loan: 49.01
Transfer: 48.61

Among paid transfers, higher transfer-fee groups showed progressively higher average sporting performance:

Fee Band	Sporting Value	Appearances	Goals	Assists
Low	53.46	28.54	4.40	2.38
Moderate	56.10	30.92	4.86	2.81
High	58.34	33.19	5.44	3.11
Very High	61.93	35.56	6.64	3.95

The statistical test produced:

statistic = 0.2017, p < 0.001

Insight: Higher-fee paid transfers are associated with higher observed sporting performance. However, the association should not be interpreted as proof that paying a higher fee causes better sporting performance.


**Statistical Analysis**

The statistical analysis was used to test relationships identified during EDA rather than to generate unsupported new concepts.

Key confirmed results include:

Sporting contribution vs market valuation

Spearman ρ = 0.304
p < 0.001

This confirms a statistically significant positive association, but only a moderate-to-weak relationship.

Transfer characteristics vs long-term recruitment success

The logistic regression model was statistically significant overall (LLR p < 0.001).

Transfer-fee groups showed significantly higher odds of long-term success than the 0-fee reference group:

1–1M: OR = 2.95
1M–5M: OR = 3.18
5M–10M: OR = 3.20
10M+: OR = 2.40

The model's pseudo-R² was 0.0115, indicating that transfer characteristics explain only a small proportion of the variation in long-term recruitment success.

Therefore, the results demonstrate association rather than causation or complete prediction.

**Power BI Dashboards & Visualizations**

The Power BI component will communicate only the confirmed analytical results.

Dashboard 1 — Sporting Value & Market Value

Focus:

Sporting-value distribution.
Market-value distribution.
Performance bands.
Market-value bands.
Sporting value versus market valuation.
Identification of high sporting value relative to financial valuation.


Dashboard 2 — Recruitment & Retention Intelligence

Focus:

Recruit, Retain, Monitor and Transfer Review distribution.
Player-season scouting classifications.
Performance bands versus market-value bands.
Recruitment targets.
Retention targets.
Transfer-review players.
Position and club-level scouting information where appropriate.


Dashboard 3 — Transfer Market & Recruitment Success

Focus:

Transfer-type distribution.
Transfer-fee distribution.
Transfer-fee bands.
Long-term recruitment success by fee category.
Confirmed statistical associations.
Sporting performance across transfer-fee bands.

The dashboards are intended to visualize the confirmed findings, not to introduce additional analytical conclusions.

**Key Findings & Insights**

The project established four central conclusions.

First, sporting performance and market valuation are positively associated, but the relationship is not strong enough to treat market value as a direct measure of sporting performance.

Second, substantial differences exist between players' sporting value and their financial valuation. This creates an analytical basis for identifying potentially attractive recruitment opportunities.

Third, transfer-fee category is significantly associated with long-term recruitment success. The strongest observed odds occurred in the 1–10M fee ranges relative to 0-fee transfers.

Fourth, transfer characteristics alone are insufficient to explain recruitment success. The low pseudo-R² indicates that other player, team, competition and contextual factors are likely to contribute to long-term outcomes.

**Stakeholder-Specific Recommendations**


**Sporting Director**

Use the integrated sporting-value and market-value framework as a supporting tool when evaluating squad investment decisions. Players should not be assessed solely according to their market valuation.

**Recruitment Department**

Prioritize players demonstrating strong sporting value relative to their financial valuation, while using market value and performance bands to structure scouting priorities.

For transfer planning, give particular attention to the evidence showing higher observed long-term success among non-zero fee groups, especially the 1–10M ranges, while avoiding the assumption that higher fees automatically produce better outcomes.

**Recruitment Decision Framework**

Use the scouting classifications to prioritize attention:

Recruit: potential recruitment targets with strong sporting evidence relative to valuation.
Retain: high-performing players who represent important sporting value.
Monitor: players requiring additional evaluation before a definitive decision.
Transfer Review: players whose financial valuation is high relative to their observed sporting value and therefore warrant further review.

**AFCON Relevance & Practical Application**

The framework can be adapted to national-team scouting environments by combining objective player performance with financial and transfer-market information.

For an AFCON-level scouting context, the framework could support identification of players who demonstrate strong sporting output without necessarily having the highest market valuations.

This is particularly relevant for resource-efficient scouting, where recruitment and selection decisions should be supported by measurable sporting evidence rather than market reputation alone.

The framework could also be adapted to compare players by position, competition and recent performance when developing future national-team scouting shortlists.

**Limitations**

The analysis has several limitations.

Market value is not equivalent to actual transfer price and can reflect factors beyond sporting performance.

The transfer-fee dataset contains a very large number of zero-fee records, requiring careful interpretation.

Transfer characteristics showed statistically significant associations with long-term success, but the statistical model explained only a small proportion of outcome variation.

The scouting decision framework is an analytical classification system and should not replace professional scouting assessment, tactical evaluation, medical assessment or contractual considerations.

Historical player data also contain records from different competitions and football environments, which may limit direct comparisons between players.

**Future Improvements / Next Steps**

Future development could incorporate:

Age and career-stage analysis.

Position-specific performance metrics.

Competition-strength adjustment.

More advanced scouting metrics.

Injury and availability information.

Contract status and remaining contract duration.

Wage information.

Team tactical context.

Longitudinal player development.

More advanced predictive modelling after strengthening the statistical foundation.


**Conclusion**

This project demonstrates how player performance, market valuation and transfer history can be integrated into a practical scouting intelligence framework.

The analysis confirms that sporting performance is positively associated with market valuation, but the relationship is not sufficiently strong to treat financial valuation as a direct proxy for sporting quality. The transfer analysis also shows statistically significant associations between transfer-fee categories and long-term recruitment success, while demonstrating that transfer characteristics alone provide limited explanatory power.

The resulting framework therefore supports a more evidence-based approach to recruitment: evaluate sporting contribution, consider financial valuation, examine transfer context, and use the combined evidence to prioritize scouting decisions rather than relying on market value alone.

Next, I want to bring team tactical context into this framework — looking at how a player's role, positioning, and output shift depending on the system and teammates around him, rather than judging performance in isolation. That would sharpen the sporting-value score and give recruitment teams a much fairer read on whether a player's numbers are a product of the player or the system.

Mwanahamisi Juma

Football Performance Analyst

+255787338398

Mwanahamis050@gmail.com
