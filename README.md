#  Hangman AI - HMM & RL Integration

This project implements an **intelligent Hangman solver** using **Hidden Markov Models (HMMs)** and a **Reinforcement Learning (RL)** framework.  
The goal is to predict masked words efficiently based on probabilistic letter patterns learned from a text corpus.

---

##  Overview

Traditional Hangman agents guess letters based on overall frequency (e.g., “e”, “t”, “a”).  
This project goes beyond that by integrating **word-length-specific HMMs** and **transition/positional probability learning**, improving the success rate over a simple baseline.

It extends to **Q-Learning / Deep Q-Learning (DQL)** for reinforcement-based decision making.

---

## Features

 **Baseline Model:**  
Guesses letters using simple positional frequency analysis from the dataset.

 **HMM-Based Models:**  
Four different HMMs trained for:
- Short words (1–4 letters)
- Medium words (5–7 letters)
- Long words (8–10 letters)
- Very long words (≥11 letters)

Each model learns:
- **Transition probabilities** — likelihood of one letter following another.
- **Positional probabilities** — likelihood of letters appearing at certain positions.

 **Integrated Agent:**  
Automatically chooses the right HMM model based on word length and combines it with baseline probabilities.

 **RL:**  
integrated **Q-Learning** using:
- State = current masked word + guessed letters  
- Action = next letter guess  
- Reward = correctness / progress toward solving the word

---

## Hangman RL Agent (part 2)
A reinforcement learning agent that plays Hangman by combining Q-learning with Hidden Markov Models (HMM) for intelligent letter guessing.

## Overview

Q-Learning: Learns optimal game strategy through trial and error
Combined Intelligence: Merges statistical language knowledge with learned gameplay tactics

Reward Structure
Correct guess +2 per letter revealed
Win (complete word)+50
Wrong guess-5
Game loss-20
Repeated guess-10

- Algorithm Details
Q-Learning with HMM Guidance

## Hyperparameters:

Alpha (α): 0.1 - Learning rate (conservative updates)
Gamma (γ): 0.95 - Discount factor (values future rewards)
Epsilon (ε): 1.0 → 0.01 - Exploration rate with exponential decay
Epsilon decay: 0.9995 per episode

## Training Process

Training episodes: 30,000 games
Training corpus: Variable (loaded from corpus.txt)
Test set: 2,000 words (loaded from test.txt)
Lives per game: 6 wrong guesses allowed
HMM models: Pre-trained on word length categories (short ≤4, medium ≤7, long ≤10, very long >10)


📁 Files Required
├── ml_hackathon_team2.ipynb              # Main training notebook
├── corpus.txt                # Training word list
├── test.txt                  # Test word list (2000 words)
├── short_hmm1.pkl            # Pre-trained HMM (≤4 letters)
├── medium_hmm1.pkl           # Pre-trained HMM (5-7 letters)
├── long_hmm1.pkl             # Pre-trained HMM (8-10 letters)
├── very_long_hmm1.pkl        # Pre-trained HMM (>10 letters)
└── hmm_rl_agent.pkl          # Saved trained agent (output)



# Calculate score

Final Score = (Success Rate × 2000) - (Wrong Guesses × 5) - (Repeated Guesses × 2)
