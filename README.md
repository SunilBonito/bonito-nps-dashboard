# Bonito Designs — NPS Intelligence Dashboard

A live, GitHub-hosted dashboard for tracking Overall NPS and Design NPS across all four Experience Centres (Andheri, Thane, HSR, HRBR).

## Setup (one-time)

1. Create a new GitHub repository (e.g. `bonito-nps-dashboard`).
2. Push these files into the repo:
   ```
   bonito-nps-dashboard/
   ├── index.html
   ├── README.md
   └── data/
       ├── final_nps.csv
       └── design_nps.csv
   ```
3. Go to **Settings → Pages**, select branch `main`, folder `/ (root)`, save.
4. Your dashboard will be live at `https://<your-username>.github.io/bonito-nps-dashboard/`.

## Monthly refresh workflow

Every month (or after each fortnight if you prefer), do this:

1. Export the two reports as CSV and rename them:
   - Overall NPS → `final_nps.csv`
   - Design NPS → `design_nps.csv`
2. Replace the files in the `data/` folder of your repo (drag-drop in GitHub web UI works fine).
3. Commit. The dashboard updates immediately on next page load.

That's it. No code changes, no rebuild.

## What's on the dashboard

**Overview** — headline KPIs (NPS, CSAT, fill rates), MoM trend lines, branch ranking
**Overall NPS** — score histogram, sub-category averages, promoter/passive/detractor split
**Design NPS** — net satisfaction trend, design sub-attributes
**Fortnight Review** — current vs previous vs same-fortnight-last-year, with eligible PIDs / sent / responded / fill rate / NPS, plus a trailing 8-fortnight table
**People** — leaderboards for Designer / PM / CRM / Design Manager (min 5 responses)
**Detractors** — full list of 0–6 scorers and "Disappointed" customers with comments, exportable to Excel
**Value × NPS** — scatter plot and tier-wise NPS to see whether project size correlates with satisfaction

## Filters (apply to entire dashboard)

- **Time window**: 12 / 6 / 3 months or all-time
- **Branch**: filter to one Experience Centre
- **Refresh** button: pulls the latest CSV from GitHub

## Notes for management

- **Design "NPS" is actually a 5-point CSAT scale** (Extremely Satisfied → Extremely Disappointed). The Design tab shows Net Satisfaction computed as (Positive − Negative) / Total × 100. This is called out on the Design tab.
- **Fortnight cycles** = 1st–15th and 16th–end-of-month, as agreed.
- The "Eligible PIDs" count in fortnight cards uses **Customer Checklist Signed** (for Overall NPS) or **3D Sign-Off Date** (for Design NPS) as the eligibility anchor — adjust this in the code if your team uses a different trigger.
- The 5-response minimum on the People leaderboard prevents one-off lucky scores from skewing rankings. Adjust the threshold in `renderPeople()` if needed.

## Tech stack

- Pure HTML/CSS/JS, no build step
- PapaParse for CSV parsing
- Chart.js for visualisations
- SheetJS (XLSX) for Excel export
- Hosted free on GitHub Pages

## Troubleshooting

- **Dashboard says "could not load CSVs"** — check that `data/final_nps.csv` and `data/design_nps.csv` exist in the repo. File names are case-sensitive.
- **Filling rate looks wrong** — the dashboard counts a row as "sent" if Feedback Sent Date is present, and "responded" if there's a non-empty score. If your CSV uses different column headers, the headers must match exactly.
- **Some months are missing in the trend** — that means there's no Feedback Date in that month. Expected behaviour.
