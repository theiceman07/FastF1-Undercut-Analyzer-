🏎️ F1 Undercut Analyzer (FastF1 Colab Project)
🔍 Analyze race strategies, tyre degradation, and telemetry with real Formula 1 data — powered by FastF1.
🧠 Overview

This project uses the FastF1
 Python library to mine and visualize Formula 1 telemetry and timing data.

Unlike most F1 data notebooks, this project focuses on identifying and analyzing undercut and overcut scenarios — where one driver gains or loses time by pitting earlier or later than a rival.

It’s built to run directly in Google Colab, fully automated, and robust against common FastF1 errors.

🚀 Features

📦 Automatic session loading
Loads the latest completed F1 race automatically, or lets you pick a specific race, round, or session (Race, Quali, Sprint, etc.).

🧹 Error-safe data cleaning
Handles invalid laps, SC/VSC periods, formation laps, and telemetry gaps gracefully.

⚙️ Race analysis toolkit

Full results table with driver and team info

Tyre stints summary

Team pace distribution (boxplot of “quick laps”)

Tyre degradation plots per driver/stint

Automatic undercut/overcut detection (finds drivers who pit within ±3 laps)

Telemetry overlay for battle drivers (speed, throttle, brake inputs)

📈 Extendable
Export data, compare drivers, visualize compounds, or compute deltas with your own extra cells.

🧩 Unique Concept

💡 “Undercut Analyzer” — a novel data mining tool for studying race strategies.

Instead of only showing fastest laps or sector times, this notebook quantifies and visualizes pit stop strategy interactions:

Detects drivers who pit within a few laps of each other.

Compares their lap times before and after the stop.

Highlights which strategy (early or late stop) was faster.

Overlays the telemetry to show why one gained time (e.g., warmer tyres, better traction, less traffic).

⚙️ Installation & Usage (Colab)

Open Google Colab

Create a new notebook

Copy and paste the full code from this repository (the single “Undercut Analyzer” cell)

Run the cell

Wait for the FastF1 data to download and cache (first run may take 1–2 minutes)

Once the outputs appear, scroll through:

Results table

Tyre stints summary

Team pace boxplot

Tyre degradation plot

Undercut/overcut battle timeline

Telemetry overlay

🔧 Configuration

At the top of the notebook, edit the PARAMS dictionary to choose what you want to analyze:

PARAMS = {
    "STRATEGY": "auto",        # "auto", "by_name", or "by_round"
    "YEAR": 2024,
    "GRAND_PRIX": "Monaco",    # used if STRATEGY = "by_name"
    "ROUND": 8,                # used if STRATEGY = "by_round"
    "SESSION": "R",            # "R", "Q", "S", "SQ", "FP1" etc.
    "PIT_WINDOW_LAPS": 3,      # how close pit stops must be to count as a 'battle'
}


Tip: You can set STRATEGY="by_name" and change GRAND_PRIX to any valid 2024 event name (e.g., "Monza", "Singapore", "Abu Dhabi").

📊 Example Outputs

Race Results – sorted by position, with lap times and points

Team Pace – boxplot comparing quick-lap distributions

Tyre Degradation – per-driver lap time trendlines

Undercut Battle – lap-time timelines before and after pit stops

Telemetry Overlay – side-by-side fastest-lap comparison (speed, throttle, brake)

🧱 Extending the Project

You can easily add more cells below the main analysis:

Compare average pace between drivers
drivers = ["VER", "LEC", "HAM"]
for d in drivers:
    avg = clean.pick_driver(d)["LapTime"].dt.total_seconds().mean()
    print(f"{d}: average lap time = {avg:.2f} s")

Plot lap times by tyre compound
df = laps.copy()
df["LapTime_s"] = df["LapTime"].dt.total_seconds()
for comp, g in df.groupby("Compound"):
    plt.scatter(g["LapNumber"], g["LapTime_s"], s=10, alpha=0.5, label=comp)
plt.legend(); plt.show()

Export lap data
laps.to_csv("/content/lap_data_export.csv", index=False)

🧰 Dependencies

FastF1

pandas

numpy

matplotlib

All are automatically installed in Colab by the script.

🧾 License

MIT License – feel free to use, adapt, and extend for your own racing analytics projects.

👨‍💻 Malligaarjunan

Created with ❤️ by [Your Name]
Powered by FastF1
 and Google Colab.
