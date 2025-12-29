# Chess Game Outcome Analysis using Econometrics

## Overview
This project applies econometric methods to analyze chess game outcomes and demonstrates how statistical models can be embedded into algorithmic decision-making. Using a dataset of rated online chess games, I estimate a logistic regression model to quantify how material imbalances and player strength affect the probability of winning. The estimated model is then incorporated into a simple chess engine using minimax search.

## Data
- Source: Lichess rated games database (2017 March ~ 11 million total games)
- Sample size: ~3000 games (subsampled for computational ease)
- Outcome variable: binary indicator for White win
- Drawn games are excluded
- All variables are defined from White’s perspective
The full dataset is not included due to size; it can be obtained directly from the Lichess public database.

## Econometric Model
The following logistic regression model is estimated:

P(White win) = logit(β0 + β1 * Material_diff + β2 * Elo_diff)

Material differences are measured using piece count imbalances:
- Pawns
- Knights
- Bishops
- Rooks
- Queens
Elo rating differences capture relative player strength.

## Key Findings
- Material advantages have large and economically meaningful effects on winning probabilities.
- Queen and rook advantages dominate marginal effects.
- Elo rating differences are statistically significant and quantitatively important.
- Estimated coefficients align closely with chess theory and human intuition.
Odds ratios are reported to facilitate economic interpretation.

## Chess Engine Integration
The estimated logistic regression model is encoded into a simple chess engine:
- Search algorithm: Minimax with alpha–beta pruning
- Search depth: 4 plies
- Evaluation function: Linear predictor from the estimated logit model

For comparison, a traditional hand-coded evaluation function using standard chess material weight is also implemented.

An interactive Jupyter-based interface allows users to:
- Play against the engine
- Switch between evaluation functions
- Observe model-based position evaluations in real time

## Model Limitations and Engine Behavior

### Castling behavior:
The engine rarely castles, which is a direct consequence of the evaluation function and search depth. Castling does not immediately change material or short-run positional metrics in terms of material, and therefore provides little incentive within a shallow minimax search. From an econometric perspective, castling represents an omitted variable. Its benefits are not directly captured by the model, although they do affect actual game outcomes.

### Binary outcome specification:
The logistic regression model treats game outcomes as binary (win vs. loss), excluding drawn games. While this simplifies estimation and interpretation, it potentially introduces selection bias, as draws are more common in balanced positions and at higher skill levels. As a result, the estimated coefficients reflect determinants of decisive outcomes rather than overall game value, which may affect external validity.

## Future Research Directions
Several extensions could improve the generalizibility of the model, empirically and strategically:

- **Multinomial or ordered outcome models** to jointly model wins, draws, and losses
- **Richer positional covariates**, such as king safety indices, center control, and pawn structure
- **Increased depth or forward-looking evaluation functions** to reduce horizon effects, where a computer ignores future negative outcomes due to low search depth
- **Out-of-sample validation** and predictive performance evaluation

These extensions would increase computational complexity but provide a more structurally complete representation of chess decision-making.

## Technologies used
- Python
- pandas, numpy
- statsmodels
- python-chess
- Jupyter Notebook


## Motivation
This project demonstrates how econometric models can be:
- Estimated from real-world data
- Interpreted quantitatively
- Embedded into algorithmic decision systems

It is intended as an applied econometrics portfolio project rather than a competitive chess engine.
