# Football Scouting Analytics: Finding Undervalued Players Through Performance and Transfer Data

A data-driven football scouting project integrating player performance, market valuation, and transfer history to identify high-value recruitment opportunities and support evidence-based decisions on player recruitment, retention, monitoring, and transfer review.

## Executive Summary

I built a scouting and recruitment framework that weighs a player's sporting performance against their market value and transfer history — designed to give recruitment teams evidence to work from instead of gut feel or reputation.

To do this, I integrated four sources: player profiles, competition-level performance records, historical market valuations, and transfer history. The goal was to move past simple performance rankings and give a more objective basis for recruitment, retention, and squad investment calls.

I aggregated performance records to the player-season level using Python, then aligned each player-season with the closest available market valuation. From there, I built a composite Sporting Value Score out of key performance indicators, and used market-value bands and performance bands to classify player value. What jumped out immediately was how much sporting performance and market valuation can diverge — strong on-pitch output doesn't reliably translate into a proportionally high market value. A Spearman correlation confirmed a statistically significant positive relationship between sporting contribution and market valuation (ρ = 0.304, p < 0.001), but the relationship is only moderate, which tells me market value is shaped by more than sporting output alone.

I also looked at transfer characteristics and how they relate to long-term recruitment success. Transfer type and transfer-fee category both showed a statistically significant association with success: conventional transfers stood out against drafts, and fees between 1M and 10M carried roughly three times the odds of long-term success compared with zero-fee transfers. That said, the model's pseudo-R² (0.0115) is low, which means transfer characteristics alone only explain a small slice of what drives long-term success.

I translated all of this into four practical classifications — Retain, Recruit, Monitor, and Transfer Review. Across the final actionable player-seasons, 28.10% landed in Retain, 23.18% in Recruit, 42.53% in Monitor, and 6.19% in Transfer Review. My aim was to give a sporting director and recruitment department an evidence-based screening tool: something that helps them spot recruitment opportunities, protect valuable players already on the books, and flag players whose price tag looks out of step with what they're actually producing on the pitch.

Overall, this project is my attempt at showing how performance data, market valuation, and transfer history can work together in one practical scouting workflow — backing recruitment decisions with evidence rather than raw stats or market price in isolation.

## Impact of the Project

This project turns four fragmented, multi-million-row datasets — player profiles, performance records, market valuations, and transfer history — into a single decision tool a recruitment department could actually use. Instead of ranking players on raw stats or reputation alone, the framework flags exactly where sporting output and market value disagree, and translates that gap into a clear call: Recruit, Retain, Monitor, or Transfer Review.

Practically, this means:

- Spotting players whose sporting contribution is undervalued relative to their market price — the kind of signal a scouting department wants before a fee rises.
  
- Giving evidence, not just gut feel, for which transfer profiles (fee range, transfer type) have historically led to longer-term success.
  
- Producing a repeatable classification any analyst could re-run on a new season's data, rather than a one-off report.

## What I Contributed to This Project

I worked across the whole analytical pipeline:

- Data quality assessment and cleaning

- Standardizing player, season, and performance information
  
- Player-season aggregation
  
- Integrating performance, market-value, and transfer data
  
- Feature engineering for the sporting-value and market-value analysis
  
- Exploratory data analysis
  
- Statistical testing of the relationships I found during EDA
  
- Building the scouting decision framework
  
- Developing the Power BI dashboards to communicate the confirmed findings
  
- Turning the statistical results into recruitment-oriented insights and recommendations

## Project Objective

To integrate player performance, market valuation, and transfer history into a scouting intelligence framework that supports evidence-based recruitment, contract renewal, and squad investment decisions.

## Research Questions

1. Which players provide the highest sporting value relative to their market valuation?

   
2. Which transfer characteristics are associated with successful long-term recruitment outcomes?

   
3. Which players should be retained, recruited, or transferred based on objective performance and financial evidence?

## Stakeholders

- Sporting Director
  
- Recruitment Department

## Dataset Overview

I worked with four datasets from Kaggle, covering player identity and characteristics, sporting output, financial valuation, and historical transfer activity:

| Dataset | Raw rows × cols | Final rows × cols |
|---|---|---|
| Player Profiles | 92,671 × 34 | 92,671 × 20 |
| Player Performance | 1,878,719 × 20 | 1,878,719 × 16 |
| Player Market Value | 901,429 × 10 | 901,429 × 10 |
| Transfer History | 1,101,440 × 3 | 1,101,317 × 3 |

## Tools & Technologies

**Python** — data cleaning, integration across four datasets, player-season aggregation, feature engineering for the sporting-value score, exploratory data analysis, and statistical testing (Spearman correlation, logistic regression).

**Power BI** — interactive dashboards for sporting value vs. market value, recruitment/retention classifications, and transfer-market patterns, built for a sporting director and recruitment department audience.

## Data Preparation & Cleaning

### Player Profiles

The original dataset had 92,671 rows and 34 columns. I worked through:

- Data-type assessment and correction
  
- Converting date fields (date of birth, joining information)
  
- Missing-value assessment
  
- Position standardization
  
- Creating a `position_group` field
  
- Foot standardization
  
- Citizenship assessment
  
- Current-club status classification
  
- Reviewing contract-related fields
  
- Removing non-essential columns I'd agreed weren't needed

The cleaned dataset kept all 92,671 rows, down to 20 columns.

### Player Performance

The original dataset had 1,878,719 rows and 20 columns. Here I handled:

- Duplicate assessment
  
- Missing-value investigation

- Standardizing season names to YY/YY format
  
- Reviewing competition and team-level records
  
- Removing columns I didn't need
  
- Keeping the relevant performance and disciplinary variables
  
- Treating missing `goals` and `minutes_played` values
  
- Correcting invalid `goals_conceded = -1` entries to NaN

The cleaned dataset kept all 1,878,719 rows, down to 16 columns.

### Player Market Value

The original dataset had 901,429 rows and 10 columns. I prepared it for player-season market-value integration, including converting the valuation date into a usable date format. It stayed at 901,429 rows and 10 columns.

### Transfer History

The original dataset had 1,101,440 rows and 3 columns. I found and removed 123 duplicate records, leaving a final dataset of 1,101,317 rows × 3 columns.

## Data Integration

Player performance was originally recorded at the competition/team level, so I aggregated it up to the player-season level, which gave me 784,260 unique player-season records.

I aligned market valuations to these player-seasons using the latest available valuation on or before the end of each season. That gave me market-value data for 553,640 player-seasons, while 230,620 player-seasons had no available valuation.

I then filtered the integrated dataset down to reliable performance and valuation information before building the sporting-value and scouting framework.

Separately, I integrated the transfer data with performance data to look at how transfer characteristics relate to long-term recruitment outcomes.

## Exploratory Data Analysis

### EDA 1 — Data Preparation & Understanding

The four datasets sit at different observation levels and cover different time spans, and player performance in particular had multiple records per player-season because of competition and team participation.

After aggregation, I had 784,260 player-season records, and after aligning market valuation, 553,640 of those had valuation data attached.

This step made it clear to me that careful player-season aggregation and temporal alignment had to come first — there was no way to compare sporting performance with financial valuation honestly without it.

### EDA 2 — Sporting Performance

I represented player-season sporting performance through appearances, goals, assists, and minutes played.

There was a lot of variation in output — some exceptionally high goal-and-assist contributions, with the highest combined figure hitting 102. I also noticed some players repeating high performances across multiple seasons, not just having one standout year.

This told me goals alone were a poor proxy for contribution — I needed to combine several indicators to get a fair read on a player's value.

### EDA 3 — Sporting Performance vs Market Value

High sporting output didn't map cleanly onto market value — I found player-seasons with very similar goal contributions sitting at markedly different valuations.

A Spearman rank correlation confirmed a statistically significant positive relationship between sporting contribution and market valuation (ρ = 0.304, p < 0.001).

Higher output does tend to line up with higher valuation, but the relationship isn't strong enough for me to say sporting performance alone determines market value. This is exactly why I approached the first research question by assessing sporting value *relative to* financial valuation, rather than just ranking players by raw performance.

### EDA 4 — Transfer Market Profile

The Transfer History dataset breaks into four categories:

| Transfer type | Count |
|---|---|
| Transfer | 844,401 |
| Loan | 128,079 |
| Return from loan | 127,665 |
| Draft | 1,172 |

Transfer fees were heavily concentrated at zero — 1,061,320 records had a fee of zero — and the dataset spans 62 seasons, from 00/01 through 25/26.

This told me a transfer record on its own doesn't mean a paid transfer happened. I had to treat transfer type and transfer-fee status as two separate things when assessing recruitment outcomes, not one signal.

### EDA 5 — Transfer Characteristics & Long-Term Recruitment Success

Long-term success rates varied clearly across transfer-fee groups:

| Fee group | Long-term success |
|---|---|
| 0 fee | 8.02% |
| 1M or below | 21.29% |
| 1M–5M | 22.53% |
| 5M–10M | 22.65% |
| Above 10M | 18.03% |

And across transfer type:

| Transfer type | Long-term success |
|---|---|
| Transfer | 9.01% |
| Return from loan | 7.07% |
| Loan | 6.68% |
| Draft | 5.63% |

Statistical testing confirmed both transfer type and transfer-fee category are associated with long-term recruitment success. Against the 0-fee reference group, every non-zero fee group showed a statistically significant association, with the 1–10M range carrying roughly three times the odds of success. For transfer type, conventional transfers stood out as significant against drafts, while loans and returns-from-loan weren't significant at the 0.05 level.

What this told me is that transfer-fee category carries more evidence of a link to long-term success than transfer type does — but on its own, neither explains most of what actually drives that success.

### EDA 6 — Scouting Intelligence & Player Value

After filtering, my integrated player-value dataset held 261,158 player-season observations.

The sporting-value score came out to:

- Mean: 50.00
  
- Median: 49.88
  
- Minimum: 7.65
  
- Maximum: 90.73

And market value:

- Mean: 1,721,902
- 
- Median: 350,000
  
- Minimum: 10,000
  
- Maximum: 200,000,000

The correlation between sporting-value score and raw market value was 0.195, rising to 0.340 against log market value.

I built the Sporting Value Score from goals, assists, appearances, and minutes played, and deliberately kept disciplinary variables separate rather than letting cards drag down the overall score. I normalized each indicator first so that variables on different scales could contribute fairly, then weighted direct sporting contributions — goals and assists — more heavily, while appearances and minutes played captured involvement and consistency. I chose this balance to reward measurable on-pitch output without ignoring players who show up and contribute steadily over a season.

From there, I classified players into performance and market-value bands and assigned scouting decisions:

| Classification | Count | Share |
|---|---|---|
| Monitor | 72,655 | 42.53% |
| Retain | 47,998 | 28.10% |
| Recruit | 39,592 | 23.18% |
| Transfer Review | 10,571 | 6.19% |

Sporting value and market valuation are clearly related, but not interchangeable — that modest correlation is exactly why I think a combined performance-financial framework makes more sense for scouting decisions than either measure alone.

### EDA 7 — Transfer Fees & Sporting Performance

Looking at transfer records linked with performance data, sporting performance varied noticeably by transfer type:

| Transfer type | Mean sporting value |
|---|---|
| Draft | 44.27 |
| Loan | 48.54 |
| Return from loan | 49.01 |
| Transfer | 48.61 |

Among paid transfers, higher fee bands lined up with progressively higher average sporting performance:

| Fee band | Sporting value | Appearances | Goals | Assists |
|---|---|---|---|---|
| Low | 53.46 | 28.54 | 4.40 | 2.38 |
| Moderate | 56.10 | 30.92 | 4.86 | 2.81 |
| High | 58.34 | 33.19 | 5.44 | 3.11 |
| Very High | 61.93 | 35.56 | 6.64 | 3.95 |

The statistical test came back at 0.2017, p < 0.001.

Higher-fee paid transfers are associated with stronger observed sporting performance — but I want to be careful not to read that as proof that paying more *causes* better performance.

## Statistical Analysis

I used statistical testing to check the relationships I'd already spotted during EDA, not to introduce new claims the data hadn't already suggested.

**Sporting contribution vs. market valuation**
Spearman ρ = 0.304, p < 0.001 — a statistically significant but only moderate-to-weak relationship.

**Transfer characteristics vs. long-term recruitment success**
The logistic regression model was significant overall (LLR p < 0.001). Transfer-fee groups showed significantly higher odds of success than the 0-fee group:

| Fee group | Odds ratio |
|---|---|
| 1M or below | 2.95 |
| 1M–5M | 3.18 |
| 5M–10M | 3.20 |
| 10M+ | 2.40 |

The model's pseudo-R² was 0.0115 — low enough that I read this as showing an association, not something close to full prediction. Transfer characteristics matter, but they're clearly not the whole story behind long-term success.

## Power BI Dashboards & Visualizations

I designed the dashboards to show only what the statistics actually support — not to introduce new claims the data can't back.

**Dashboard 1 — Sporting Value & Market Value**
Sporting-value distribution, market-value distribution, performance bands, market-value bands, sporting value versus market valuation, and identifying high sporting value relative to financial valuation.

**Dashboard 2 — Recruitment & Retention Intelligence**
Recruit/Retain/Monitor/Transfer Review distribution, player-season scouting classifications, performance bands versus market-value bands, recruitment and retention targets, transfer-review players, and position/club-level scouting information where it's useful.

**Dashboard 3 — Transfer Market & Recruitment Success**
Transfer-type distribution, transfer-fee distribution and bands, long-term recruitment success by fee category, the confirmed statistical associations, and sporting performance across transfer-fee bands.

## Key Findings

Four things stood out to me by the end of this project.

Sporting performance and market valuation move together, but not tightly enough that I'd treat one as a stand-in for the other.

There are real, substantial gaps between a player's sporting value and their financial valuation — and that gap is exactly where recruitment opportunities tend to hide.

Transfer-fee category has a meaningful, statistically significant link to long-term recruitment success, with the strongest odds sitting in the 1–10M range.

But transfer characteristics alone don't explain much of what drives that success — the low pseudo-R² tells me other factors (player, team, competition, context) are doing a lot of the work I haven't captured here.

## Stakeholder-Specific Recommendations

**Sporting Director** — Use this combined sporting-value and market-value framework as a supporting tool for squad investment decisions, not a replacement for judgment. Players shouldn't be assessed on market valuation alone.

**Recruitment Department** — Prioritize players who show strong sporting value relative to their financial valuation, using the performance and market-value bands to structure scouting priorities. For transfer planning, pay attention to the higher observed long-term success in non-zero fee groups, especially 1–10M — but don't assume that paying more automatically buys a better outcome.

## Recruitment Decision Framework

- **Recruit** — potential targets with strong sporting evidence relative to valuation
  
- **Retain** — high-performing players who represent real sporting value
  
- **Monitor** — players who need more evaluation before a firm decision
  
- **Transfer Review** — players whose valuation looks high relative to their observed sporting output, and therefore worth a closer look

## AFCON Relevance & Practical Application

I think this framework adapts well to a national-team scouting environment — combining objective player performance with financial and transfer-market information rather than leaning on reputation.

For an AFCON-level context specifically, it could help identify players with strong sporting output who don't necessarily carry the highest market valuations — useful for resource-efficient scouting, where selection decisions should rest on measurable evidence rather than name recognition. I can also see it being adapted to compare players by position, competition, and recent form when building future national-team shortlists.

## Limitations

- Market value isn't the same as actual transfer price, and can reflect things beyond sporting performance.
  
- The transfer-fee data is heavily skewed toward zero-fee records, which needs careful interpretation.

- Transfer characteristics showed a significant statistical link to long-term success, but the model only explains a small share of the outcome variation.

- This scouting framework is an analytical classification system — it isn't a substitute for professional scouting judgment, tactical evaluation, medical assessment, or contract considerations.
  
- The historical data spans different competitions and football environments, which can limit how directly players compare to one another.

## Future Improvements

I'd like to build on this by adding:

- Age and career-stage analysis
- 
- Position-specific performance metrics
- 
- Competition-strength adjustment
- 
- More advanced scouting metrics
- 
- Injury and availability information
- 
- Contract status and remaining duration
- 
- Wage information
- 
- Team tactical context
- 
- Longitudinal player development
- 
- More advanced predictive modelling, once the statistical foundation is stronger

## Conclusion

Working through this project showed me how much performance, valuation, and transfer data need to be read together — none of them tell the full story on their own.

Sporting performance and market valuation are positively linked, but not tightly enough that I'd treat financial valuation as a stand-in for sporting quality. The transfer analysis backs up a real, statistically significant link between transfer-fee category and long-term recruitment success, while also making clear that transfer characteristics by themselves only go so far in explaining it.

What I take from this is a more evidence-based way to approach recruitment: look at sporting contribution, weigh it against financial valuation, factor in transfer context, and let that combined picture guide scouting priorities — rather than leaning on market value alone.

Next, I want to bring team tactical context into this framework — looking at how a player's role, positioning, and output shift depending on the system and teammates around him, rather than judging performance in isolation. That would sharpen the sporting-value score and give recruitment teams a much fairer read on whether a player's numbers are a product of the player or the system.

Mwanahamisi Juma


Football Data Analyst


+255787338398


Mwanahamis050@gmail.com
