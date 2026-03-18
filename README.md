# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] Describe the game's purpose.
   - The game is a number guessing challenge where the player tries to find a secret number within a limited number of attempts.
   - It gives directional feedback (go higher or go lower) and tracks score based on outcomes and attempt count.

- [x] Detail which bugs you found.
   - Attempts left shown in the UI was inconsistent with backend state and could appear off by one.
   - Game-over and restart flow was broken in some paths, including difficulty changes and New Game behavior.
   - Out-of-range guesses were not handled as fair invalid inputs in gameplay flow.
   - State-related reruns made behavior feel inconsistent from click to click.

- [x] Explain what fixes you applied.
   - Kept critical game state in Streamlit session state and reset it through a dedicated `reset_game(...)` function.
   - Stabilized secret number behavior so it persists during play and only changes on explicit reset/difficulty reset.
   - Enforced range validation through shared logic helpers and aligned attempts/status handling with expected game flow.
   - Verified logic outcomes with `pytest` and validated state/rerun behavior through manual gameplay checks.

## 📸 Demo

- [ ] [Insert a screenshot of your fixed, winning game here]

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
