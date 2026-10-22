# F1 Race Strategy Simulator

> **Work in progress**. Currently in Phase 0 (setup).

A data-driven Formula 1 race strategy simulator. It models **tyre degradation** and **pit-stop time loss** from real timing data, runs **Monte Carlo simulations** of candidate strategies (number of stops, timing and compounds), and recommends the one with the lowest expected race time, then compares it with the strategies teams actually used.

**Core question:** *Given a circuit, conditions and a driver, which pit-stop strategy minimizes total race time, and how far was the real strategy from that optimum?*

## Motivation

I'm a Computer Engineering and Data Science student, and I've always been curious about the split-second strategy calls behind every F1 race: why one team pits early while another stays out. This project is my way of answering that question with real data while learning the full machine learning workflow end to end, from messy timing data to a validated model, a simulation and a deployed app.

## Roadmap

- [x] **Phase 0** - Setup: repository, environment, first contact with FastF1
- [ ] **Phase 1** - Exploratory data analysis
- [ ] **Phase 2** - Reproducible data pipeline (Parquet + DuckDB)
- [ ] **Phase 3** - Tyre degradation model (linear baseline → XGBoost)
- [ ] **Phase 4** - Dashboard v0 (Streamlit)
- [ ] **Phase 5** - Pit-loss estimation and Monte Carlo strategy simulation
- [ ] **Phase 6** - Cloud storage, automation and deployment
- [ ] **Phase 7** - Documentation and results

## Tech stack

Python 3.14 · FastF1 · pandas · Parquet · DuckDB · scikit-learn · XGBoost · Streamlit · Plotly

## Getting started

```bash
git clone https://github.com/mpereira11/f1-strategy-simulator.git
cd f1-strategy-simulator
python -m venv .venv            # on Windows you can use: py -3.14 -m venv .venv

# Activate the environment
.venv\Scripts\Activate.ps1      # Windows (PowerShell)
source .venv/bin/activate       # macOS / Linux

python -m pip install -r requirements.txt
```

## Project structure

```
f1-strategy-simulator/
├── data/            # local data and FastF1 cache (not versioned)
├── notebooks/       # exploration notebooks
├── src/
│   ├── data/        # data download and cleaning
│   ├── models/      # tyre degradation and pit-loss models
│   ├── simulation/  # Monte Carlo strategy simulation
│   └── app/         # Streamlit dashboard
├── tests/
└── docs/            # design decisions and notes
```

## Data sources

- [FastF1](https://github.com/theOehrly/Fast-F1): lap timing, tyres, pit stops, weather and track status (2018+)

## License

[MIT](LICENSE)