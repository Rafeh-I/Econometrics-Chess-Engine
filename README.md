# Chess Game Outcome Analysis using Econometrics

## Overview
This project combines econometrics and algorithmic game design to analyze and play chess. Using a dataset of rated online games, I estimate a logistic regression model to quantify how material imbalances and Elo rating differences influence winning probabilities. The model is integrated into a Python-based chess engine using minimax search with alpha–beta pruning, allowing users to play against both a hand-coded evaluator and a data-driven mode;.
 
## Data
- Source: Lichess rated games database (2017 March ~ 11 million total games)
- Sample: Subsample of 3,000 games for computational ease
- Outcome variable: Binary indicator for White win; drawn games excluded
- Features: Piece differences (pawn, knight, bishop, rook, queen) and Elo rating difference
- All variables are defined from White’s perspective
  
The full dataset is not included due to size; it can be obtained directly from the Lichess public database.

## Econometric Model
The following logistic regression model is estimated:

P(White win) = logit(β0 + β1 * Material_diff + β2 * Elo_diff)

-Material differences are measured using piece count imbalances
-Elo rating differences capture relative player strength

## Key insights:
- Each additional pawn increases odds of winning by ~15%.
- Knight/bishop advantages increase odds by ~60–66%.
- Rook and queen advantages have the largest effects, with a queen advantage nearly quadrupling odds.
- Elo differences are statistically significant; +100 Elo points increase win odds by ~57%.

## Chess Engine Integration
- Search Algorithm: Minimax with alpha–beta pruning.
- Evaluation Options: Hand coded material + positional evaluation
- Logistic regression-based score from econometric model.
- Interactive Interface: Play against the engine in a Jupyter notebook using a simple UI with move input, reset, and evaluation toggle.

## Model Limitations and Engine Behavior

### Castling behavior:
The engine rarely castles, which is a direct consequence of the evaluation function and search depth. Castling does not immediately change material or short-run positional metrics in terms of material, and therefore provides little incentive within a shallow minimax search. From an econometric perspective, castling represents an omitted variable. Its benefits are not directly captured by the model, although they do affect actual game outcomes.

### Binary outcome specification:
The logistic regression model treats game outcomes as binary (win vs. loss), excluding drawn games. While this simplifies estimation and interpretation, it potentially introduces selection bias, as draws are more common in balanced positions and at higher skill levels. As a result, the estimated coefficients reflect determinants of decisive outcomes rather than overall game value, which may affect external validity.

## Future Research Directions
Several extensions could improve the generalizibility of the model, empirically and strategically:

- Non binary models such as multinomial logit to jointly model wins, draws, and losses
- Include richer positional features (king safety, pawn structure, control of center).
- Increase search depth or implement more advanced evaluation functions
- Out-of-sample validation to assess predictive performance.

These extensions would increase computational complexity but provide a more structurally complete representation of chess decision-making.

## Technologies used
-Languages: Python
-Libraries: pandas, numpy, statsmodels, python-chess, ipywidgets, matplotlib, tqdm
-Environment: Jupyter Notebook

