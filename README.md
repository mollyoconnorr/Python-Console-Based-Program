# Console-Based WORDLE Game

## Description

This is a **text-based Wordle game** written in Python. 

- The player has **6 attempts** to guess a **secret 5-letter word**.  
- After each guess, the game provides **feedback for each letter** using **colors and symbols**:

  - **Green (`✓`)** = correct letter in the correct spot  
  - **Yellow (`~`)** = correct letter but in the wrong spot  
  - **Red (`x`)** = letter not in the word  

- The symbols are displayed **directly below the letters** to help the player track their guesses, similar to the official Wordle game.

## Files Required

To run this program, you need two text files in the same folder as the Python script:

1. **words.txt** – a smaller list of common 5-letter words used to pick the secret word.  
2. **complex_words.txt** – a larger list of valid 5-letter words used to **validate the player's guesses**.  

Each file should have **one word per line**.

---

## How to Run

1. Make sure **Python 3.11** or higher is installed.  
2. Place `words.txt` and `complex_words.txt` in the same folder as `main.py`.  
3. Run the program:

```bash
python main.py
```
---

## Interesting Feature: Dual Word Lists

This Wordle game uses **two separate word lists** to enhance gameplay and ensure accurate validation:

### Validation List
- **Size:** 16,153 five-letter words (from `wordlist.txt`)  
- **Purpose:** Used to validate player guesses.  
- **Subset:** 5,757 words originally used by Donald Knuth in the **Stanford Graph Base (SGB)**.  
  - Ensures that guesses are **real English words** recognized in the dataset.  
- **Source files:**  
  - `complex_words.txt` — larger set of five-letter words for validation.  
  - `words.txt` — more common words included to cover everyday vocabulary.  

### Answer List
- **Size:** Contains more common five-letter words.  
- **Purpose:** Used as potential **secret words** in the game.  
- Randomly selected to ensure that the secret word is guessable and keeps gameplay fair.

### Why Two Lists?
Separating **valid guesses** from **possible answers** allows the game to:  
1. Validate player input against a comprehensive dictionary without limiting potential secret words.  
2. Ensure that secret words are reasonably guessable, improving gameplay experience.  

**Source:** Both datasets were originally obtained from [J. Burkardt's Word List](https://people.sc.fsu.edu/~jburkardt/datasets/words/words.html)



## Challenge: Handling Repeated Letters

This game handles repeated letters similarly to the official Wordle rules. 

For example:

```python
# Secret word = "FLAME"
# Guess = "AALII"
```

There is **only one `A`** in the secret word.

Even though the guess has **two `A`s**, only one is marked yellow (`~`).

The second `A` is marked red (`x`) because there is no second `A` in the secret word.

This is implemented in the code with the following logic:

```python
if guess_letters[i] in secret_count and secret_count[guess_letters[i]] > 0:
    # mark yellow (~) and reduce the count
else:
    # mark red (x)
```

This ensures that the feedback is accurate for repeated letters, so the player doesn’t get extra yellow marks for letters that appear fewer times in the secret word.

