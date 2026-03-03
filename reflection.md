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

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
