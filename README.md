Pitcher K% Projection Model
Overview

This project uses R to build a projection model that predicts each MLB pitcher's 2025 strikeout rate (K%) using only data from before 2025.

Data

The model uses FanGraphs pitcher data from 2021-2025 (season, K%, batters faced, Stuff+, and age). The dataset is not included in this repository. To reproduce the results, place a CSV named k_2026.csv with those columns in the same folder as Trial_Project.Rmd and knit the file.

Method

A Marcel-style shrinkage baseline blends a pitcher's three most recent seasons, weighted by recency and batters faced, and pulls the result toward the league-average K%. The recency weights, batters-faced cap, and shrinkage strength were chosen by a grid search that only used 2022-2024 data. Pitchers with very little history get a simple age-based ridge regression instead. I also tested a ridge layer on top of Marcel for established pitchers and kept the simpler baseline because it was easier to explain.

Tools
R
R Markdown
Marcel projection method (shrinkage estimator)
Ridge Regression
2025 Results

The model was evaluated against actual 2025 outcomes. Compared with simple baselines:

Established pitchers (640): 5.9 points of error vs. 7.2 for "same as last year"
All pitchers (873): 8.1 points of error vs. 8.7 for the league average
62% of predictions landed within 5 points of the actual K%
84% of predictions landed within 10 points
