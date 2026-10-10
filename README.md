# Marketing KPI Analysis with n8n + AI

Data is randomly generated and located at the link: https://docs.google.com/spreadsheets/d/1kK2VIHIZH5nR_jKC0mhBq3uNQdiKJPAo4UFPBS60y4o/edit?usp=sharing.
Sheet 'campaigns' contains original data; sheet 'campaigns_analyst' contains n8n workflow output.
An n8n workflow that reads campaign data from Google Sheets, calculates key marketing KPIs, saves them to a new sheet tab, and uses an AI agent to write an analysis with budget recommendations. Every run commits the AI report to the `reports/` folder of this repository.

## How it works
1. **Read Marketing Data** - loads campaign data from Google Sheets (impressions, clicks, conversions, spend, revenue)
2. **Calculate KPIs** - computes metrics overall, per channel and per campaign
3. **Save to campaigns_analyst tab** - writes every campaign with its KPIs back to the sheet
4. **AI Marketing Analyst** - an AI agent (gpt-5-mini) interprets the results and recommends where to move budget
5. **Commit to GitHub** - the report is saved as `reports/marketing-report-<date>.md`

## KPIs
| Metric | Formula |
|---|---|
| CTR | clicks / impressions x 100 |
| CPC | spend / clicks |
| CPA | spend / conversions |
| ROAS | revenue / spend |
| Conversion rate | conversions / clicks x 100 |

## Results (sample data, 30 campaigns)
- Spend: **11,525 PLN** -> Revenue: **131,300 PLN**
- CTR **8.36%**, CPC **0.79 PLN**, CPA **10.22 PLN**, ROAS **11.39**, CR **7.7%**
- Best channels by ROAS: Email (56.7), Organic (35.7), Meta (13.0)
- Weakest campaigns: Google Display - Prospecting (ROAS 1.46), LinkedIn - Traffic (ROAS 1.82), YouTube - Awareness (ROAS 2.09)
- AI recommendation: pause the weakest campaigns and move ~1,844 PLN to top-performing channels

See the full AI-generated reports in [reports/](reports/).

## Run it yourself
1. Import the workflow JSON into n8n
2. Connect your Google Sheets, OpenAI and GitHub credentials
3. Point the Google Sheets nodes to your sheet (columns: campaign, channel, campaign_type, date, impressions, clicks, conversions, spend_pln, revenue_pln)
4. Click **Execute workflow**

## Tech
n8n - Google Sheets - OpenAI - GitHub - JavaScript
