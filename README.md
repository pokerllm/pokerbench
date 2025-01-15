# PokerBench: Training Large Language Models to become Professional Poker Players

**PokerBench has been accepted to AAAI 2025.**

Paper, Code and Dataset coming soon!


Dataset Link: https://huggingface.co/datasets/RZ412/PokerBench

[📂 Access the Dataset on Hugging Face]([https://huggingface.co/datasets/your-dataset-name](https://huggingface.co/datasets/RZ412/PokerBench))

# PokerBench Dataset Overview

This dataset contains natural language game scenarios and optimal decisions computed by solvers in No Limit Texas Hold’em. It is divided into pre-flop and post-flop datasets, each with training and test splits. The data is stored in both .json and .csv formats:

- JSON files: Contain the natural language prompts (instruction) and optimal decisions (output) derived from the game scenarios.

- CSV files: Contain structured game information from which the JSON files were generated. The pre-flop and post-flop CSV files have different structures to accommodate the different stages of the game.

# Dataset Structure

## JSON Files

The JSON files include the following keys for both pre-flop and post-flop datasets:

- instruction: A detailed natural language game scenario summarizing the game state, player positions, actions, and the board cards.
- output: The optimal decision for the described scenario. Possible decisions include check, fold, call, or bet/raise (with specific amounts in some cases).

### Example JSON entry:

{
  "instruction": "You are a specialist in playing 6-handed No Limit Texas Holdem. The following will be a game scenario and you need to make the optimal decision...",
  "output": "check"
}

## CSV Files

The CSV files store structured game scenario information. They include details of player actions, positions, and board state. The structure of the columns differs for pre-flop and post-flop datasets.

### Pre-Flop CSV

Columns:
1. prev_line: The sequence of player actions before the current decision point, formatted as {Position}/{Action}/{Amount}. E.g., UTG/2.0bb/BTN/call/SB/13.0bb/BB/allin.
 2.	hero_pos: The position of the player making the decision (UTG, HJ, CO, BTN, SB, or BB).
 3.	hero_holding: The player’s hole cards (e.g., KdKc for King of Diamonds and King of Clubs).
 4.	correct_decision: The optimal decision for the player (call, fold, etc.).
 5.	num_players: The number of players still in the hand at the decision point.
 6.	num_bets: The number of betting rounds/actions that have occurred so far.
 7.	available_moves: The possible decisions the player can make (e.g., ['call', 'fold']).
 8.	pot_size: The current size of the pot at the decision point.

#### Example Row:

UTG/2.0bb/BTN/call/SB/13.0bb/BB/allin/UTG/fold/BTN/fold, SB, KdKc, call, 4, 3, ['call', 'fold'], 117.0

### Post-Flop CSV

Columns: 
1. preflop_action: The sequence of player actions leading to the flop, formatted as {Position}/{Action}/{Amount}.
 2.	board_flop: The three community cards on the flop (e.g., Ks7h2d).
 3.	board_turn: The turn card, if available (e.g., Jc).
 4.	board_river: The river card, if available (e.g., 7c).
 5.	aggressor_position: The position of the most recent aggressor in the hand (OOP for out of position, IP for in position).
 6.	postflop_action: The sequence of player actions post-flop, formatted as {Position}\_{Action}\/{Position}\_{Action}. E.g., OOP_CHECK/IP_BET_5/OOP_RAISE_14.
 7.	evaluation_at: The street at which the decision is evaluated (Flop, Turn, or River).
 8.	available_moves: The possible decisions the player can make (e.g., ['Check', 'Bet 24']).
 9.	pot_size: The current size of the pot at the decision point.
 10. hero_position: The position of the player making the decision (UTG, HJ, CO, BTN, SB, or BB).
 11. holding: The player’s hole cards (e.g., 8h8c for two eights of hearts and clubs).
 12. correct_decision: The optimal decision for the player (Check, Call, Bet, etc.).

#### Example Row:

HJ/2.0bb/BB/call, Ks7h2d, Jc, 7c, OOP, OOP_CHECK/IP_CHECK/dealcards/Jc/OOP_CHECK/IP_BET_5/OOP_RAISE_14, River, ['Check', 'Bet 24'], 32, IP, 8h8c, Check

## File Descriptions
	1.	Pre-Flop Dataset:
	•	preflop_60k_train_set_game_scenario_information.csv: Structured game information for 60,000 training examples.
	•	preflop_60k_train_set_prompt_and_label.json: Natural language prompts and decisions for 60,000 training examples.
	•	preflop_1k_test_set_game_scenario_information.csv: Structured game information for 1,000 test examples.
	•	preflop_1k_test_set_prompt_and_label.json: Natural language prompts and decisions for 1,000 test examples.
	2.	Post-Flop Dataset:
	•	postflop_500k_train_set_game_scenario_information.csv: Structured game information for 500,000 training examples.
	•	postflop_500k_train_set_prompt_and_label.json: Natural language prompts and decisions for 500,000 training examples.
	•	postflop_10k_test_set_game_scenario_information.csv: Structured game information for 10,000 test examples.
	•	postflop_10k_test_set_prompt_and_label.json: Natural language prompts and decisions for 10,000 test examples.

## Usage

The dataset can be used to train and evaluate language models for decision-making in No Limit Texas Hold’em. Use the JSON files for direct training and evaluation with natural language prompts and decisions. Use the CSV files for more detailed analysis or for generating custom prompts.

