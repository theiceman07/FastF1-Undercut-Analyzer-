# 🏎️ FastF1 Undercut Analyzer (Google Colab)

An interactive, single-cell **Formula 1 race analysis** notebook built with **FastF1**.  
It auto-loads a race session, cleans lap data, visualizes team pace and tyre degradation, and **detects potential undercut/overcut battles** with side-by-side telemetry overlays.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/<YOUR_USER>/<YOUR_REPO>/blob/main/<YOUR_NOTEBOOK>.ipynb)

---

## ✨ What this notebook does

- 🔄 **Smart session selection**  
  Choose latest completed race automatically, by round, or by GP name.
- 🧹 **Robust data cleaning**  
  Uses `pick_quicklaps()` + outlier trimming and sanity filters.
- 🧰 **Race summaries**  
  - Results table (position, team, best lap, etc.)  
  - **Stint summary** (compound & stint length)
- 📊 **Team race pace**  
  Boxplot of quick-lap pace by team.
- 🧵 **Tyre degradation**  
  Scatter + per-driver trendlines (lap time vs lap).
- 🔁 **Undercut/overcut detector**  
  Finds drivers who pitted within a given lap window and compares lap times **before/after** their stops.
- 📈 **Telemetry overlay**  
  Fastest-lap **Speed / Throttle / Brake** overlays for two drivers (battle pair or top-2 finishers).
- ⚡ **Caching & retries**  
  Uses a local cache and gentle retries for reliability in Colab.

---

## ⚙️ Parameters (edit at the top)

| Key | Purpose | Values / Notes |
|---|---|---|
| `STRATEGY` | How to pick the session | `"auto"` (latest in `YEAR`), `"by_name"` (use `GRAND_PRIX`), `"by_round"` (use `ROUND`) |
| `YEAR` | Championship year | e.g., `2024` |
| `GRAND_PRIX` | Race name (partial ok) | e.g., `"Bahrain"`, `"Monza"` *(used if `STRATEGY="by_name"`)*
| `ROUND` | Round number | `1..22` *(used if `STRATEGY="by_round"`)*
| `SESSION` | Session code | `"R"` (race), `"Q"`, `"SQ"`, `"S"`, `"FP1/2/3"` |
| `LAPTIME_MIN_S` | Drop laps faster than this (glitches) | default `50` |
| `OUTLIER_Q` | Trim top slow outliers among quick laps | default `0.99` (drop slowest 1%) |
| `MAX_TELEMETRY_DRIVERS` | Max drivers in telemetry overlay | default `2` |
| `PIT_WINDOW_LAPS` | Pits within ±N laps count as a battle | default `3` |

> Tip: For a specific race, set `STRATEGY="by_name"`, `YEAR=2024`, `GRAND_PRIX="Bahrain"` (or any partial name).

---

## ▶️ How to run (Colab)

1. Click the **Open in Colab** badge above (replace the link with your repo path).  
2. Run the notebook **top to bottom**. First cell installs dependencies.  
3. (Optional) Edit **`PARAMS`** to pick a different race/session.  
4. Scroll to the outputs: results, stint table, team boxplot, tyre-deg, **undercut timeline**, and **telemetry overlays**.

The notebook creates a cache at `/content/f1cache` so repeated runs are faster.

---

## 📸 Outputs you’ll see

- **Results table** (Position, Team, Best lap, etc.)  
- **Stint summary** per driver (compound & length)  
- **Team pace boxplot** (quick-laps)  
- **Tyre degradation plot** with per-driver trendlines  
- **Undercut/overcut timeline** (lap time vs lap with pit-in markers)  
- **Telemetry overlays** (Speed, Throttle & Brake) for the battle pair or top-2 finishers

---

## 🛠️ Dependencies

Installed automatically in the first cell:
```text
fastf1
pandas
matplotlib
numpy

🧩 How the notebook is structured

Install & imports

Parameters (PARAMS)

Cache enable (/content/f1cache)

Matplotlib + FastF1 plotting setup

Helper functions

choose_session (auto/by_name/by_round with retries)

clean_laps, stint_summary

team_pace_boxplot, tyre_deg_plot

find_undercut_pair, gap_before_after, plot_undercut_timeline

telemetry_overlay

Session load & results table

Laps, summaries, and visualizations

Undercut detection + telemetry overlay

Done message & re-run hint

🧪 Notes & tips

If the live schedule API is slow, the code retries and falls back to 2024 Bahrain Race.

Telemetry overlay needs at least two valid quick laps; otherwise the notebook shows the top-2 finishers.

Plots hide extreme outliers to keep visuals readable.

🙏 Acknowledgements

Built on top of FastF1
 by @theOehrly and contributors.

Data provided via public F1 timing sources accessed through FastF1.

📜 License

This notebook is for educational/research purposes.
If you publish or share, please credit FastF1 and this repository.
