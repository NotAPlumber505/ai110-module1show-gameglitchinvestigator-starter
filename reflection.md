# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

Bugs found:
1. When the same number is guessed, the "attempts allowed" do not go down even though they should go down when you guess (the number does not go down on the frontend, but in the backend it does as shown in the developer debug information).
2. After making only a few guesses, the game was already over, and my "attempts" allowed did not go down in the UI to 0 when this happened.
3. When I switched difficulties after the game was over, it would not let me restart and be stuck on game over. I had to refresh the website to restart my game, as the "New Game" button does not restart the game.
4. The "attempts left" for each difficulty is one off between the sidebar's number and the number shown on the main page.
5. Guesses beyond ranges (i.e., "range: 1 to 100") but guessing -1 or 150, for example, should be considered "invalid guesses" and not counted towards attempts, but they are counted in the application, indicating that these ranges are not explicitly enforced.

When I first ran it, the UI looked playable but the behavior was inconsistent from one click to the next. The biggest issues were state-related: attempts shown in different parts of the UI did not match, and game-over could trigger in a confusing way after only a few guesses. Restart behavior was also broken because changing difficulty or pressing New Game did not always recover the app cleanly. I also confirmed that out-of-range guesses were being handled poorly for gameplay fairness and needed proper validation.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used Copilot in VS Code plus ChatGPT as a second opinion when I got stuck on Streamlit state behavior. One correct suggestion was to keep game variables in `st.session_state` and initialize them once, then reset them only through a dedicated reset function; I verified this in the Developer Debug Info panel by seeing the secret stay stable between submits and only change on New Game or difficulty switch. A misleading suggestion was effectively assuming unit tests around `check_guess` were enough to validate the full app, because those tests can pass while the UI/state flow is still wrong. I verified that mismatch by manually playing several rounds and observing behavior that tests did not cover.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I treated a bug as fixed only when both the app behavior matched expectations and the tests still passed. I ran `pytest -q` and got 3 passing tests, which confirmed win, too-high, and too-low outcomes in the pure logic layer. Then I manually tested New Game, difficulty switching, invalid input, and attempt counting to catch state/rerun issues that unit tests do not currently exercise. AI helped me separate what belongs in testable logic helpers versus what still needs manual verification in Streamlit interactions.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

The secret number kept changing originally because Streamlit reruns the script top-to-bottom on user interaction, so any plain variable assignment for the secret could be recreated each submit. A rerun is not a page refresh in the traditional sense, but it does re-execute the script, which means values disappear unless they are stored in session state. I now explain session state as a per-user memory dictionary that survives reruns during that browser session. The change that stabilized the secret was initializing it only if missing in `st.session_state` and routing resets through `reset_game(...)` instead of recreating it every run.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse is validating with both automated tests and a short manual checklist for UI/state workflows, because each catches different failures. Next time I work with AI, I would ask for a concrete test plan earlier (including edge cases like invalid range guesses and difficulty changes) instead of only requesting code edits. This project made me treat AI-generated code as a draft that needs verification, not as a final answer. AI sped up iteration, but I still had to drive the debugging strategy and confirm behavior myself.
