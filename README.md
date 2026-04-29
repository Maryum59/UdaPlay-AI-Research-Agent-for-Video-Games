# UdaPlay — An AI Assistant That Answers Video Game Questions

UdaPlay is an AI assistant that can answer questions about video games. You ask it something like *"When was Super Mario 64 released?"* and it finds the answer — first by checking its own private library of games, and only going to the internet if the library does not have what you need. It also remembers what you talked about before.

This project is built in two parts, in two separate notebooks. Part 1 builds the game library. Part 2 builds the AI assistant that uses it.

---

## The Two Files

| File | What It Does |
|---|---|
| `Udaplay_01_starter_project.ipynb` | Creates a private library of 15 famous video games |
| `Udaplay_02_starter_project.ipynb` | Builds the AI assistant that searches that library to answer questions |

You must run File 1 first. File 2 will not work without the library that File 1 creates.

---

## Part 1 — `Udaplay_01_starter_project.ipynb`
### Building the Game Library

Before the AI can answer anything, it needs a collection of game information to search through. This notebook creates that collection.

**How it works in plain English:**

Imagine you have 15 index cards, one for each famous game. Each card has the game's name, the console it was on, the year it came out, and a short description. You store all 15 cards in a box.

But here is the clever part — instead of reading every card when someone asks a question, the system gives each card a secret score based on its meaning. When a question comes in, it finds whichever card's score is closest to the question's score and brings that card forward.

This means you can search by *meaning*, not just by exact words. If you ask *"a Mario game on Nintendo"*, it will find Super Mario 64 even if you never typed those exact words.

---

### The 15 Games in the Library

| # | Game | Console | Year |
|---|---|---|---|
| 1 | Gran Turismo | PlayStation 1 | 1997 |
| 2 | Grand Theft Auto: San Andreas | PlayStation 2 | 2004 |
| 3 | Gran Turismo 5 | PlayStation 3 | 2010 |
| 4 | Marvel's Spider-Man | PlayStation 4 | 2018 |
| 5 | Marvel's Spider-Man 2 | PlayStation 5 | 2023 |
| 6 | Pokémon Gold and Silver | Game Boy Color | 1999 |
| 7 | Pokémon Ruby and Sapphire | Game Boy Advance | 2002 |
| 8 | Super Mario World | SNES | 1990 |
| 9 | Super Mario 64 | Nintendo 64 | 1996 |
| 10 | Super Smash Bros. Melee | GameCube | 2001 |
| 11 | Wii Sports | Wii | 2006 |
| 12 | Mario Kart 8 Deluxe | Nintendo Switch | 2017 |
| 13 | Kinect Adventures! | Xbox 360 | 2010 |
| 14 | Minecraft | Xbox One | 2013 |
| 15 | Halo Infinite | Xbox Series X\|S | 2021 |

---

### Testing the Library

At the end of Part 1, there is a test search to prove the library works. The question asked was:

> *"Mario platformer game Nintendo"*

The library returned these 5 results, ranked from most to least relevant:

| Rank | Game | Console | Year |
|---|---|---|---|
| 1 | Super Mario 64 | Nintendo 64 | 1996 |
| 2 | Super Mario World | SNES | 1990 |
| 3 | Mario Kart 8 Deluxe | Nintendo Switch | 2017 |
| 4 | Super Smash Bros. Melee | GameCube | 2001 |
| 5 | Pokémon Gold and Silver | Game Boy Color | 1999 |

Notice it understood the meaning of the question — it did not need the words to match exactly.

---

## Part 2 — `Udaplay_02_starter_project.ipynb`
### Building the AI Assistant

Now that the game library exists, this notebook builds UdaPlay — the AI assistant that uses it.

---

### How UdaPlay Answers Your Question

UdaPlay always follows the same 3 steps, in the same order, every single time:

```
Step 1 — Check the private game library first
              ↓
Step 2 — Ask itself: "Is what I found actually useful?"
              ↓
         YES → give the answer from the library
         NO  → go to Step 3
              ↓
Step 3 — Search the internet for the answer
              ↓
         Give the final answer
```

**Think of it like a librarian.** When you walk in with a question, they first check the shelves inside. If they find a useful book, they answer from it. If the library does not have what you need, only then do they go search online. They never go online first without checking the shelves.

---

### The 3 Tools UdaPlay Uses

UdaPlay has 3 tools it can pick from, like buttons it can press:

---

**Tool 1 — Search the Library**

This searches through the 15 games stored in Part 1. It finds the 5 games most closely related to your question and brings them back.

---

**Tool 2 — Judge the Results**

After searching, UdaPlay asks a second AI to look at what was found and answer one question:

> *"Is this actually useful to answer what the person asked?"*

- If yes → UdaPlay writes the answer from what it found
- If no → UdaPlay moves on to Tool 3

---

**Tool 3 — Search the Internet**

Only used when Tool 2 says the library results were not good enough. This tool searches the internet and brings back real web pages and links. The final answer will include those sources so you know where the information came from.

---

### Real Questions the Agent Answered

**Question 1:** *"When was Pokémon Gold and Silver released?"*

- Checked the library → found Pokémon Gold and Silver card ✓
- Judged the results → good enough ✓
- Internet search → not needed
- **Answer:** *"Pokémon Gold and Silver were released in 1999 for the Game Boy Color."*

---

**Question 2:** *"Which one was the first 3D Mario game?"*

- Checked the library → found Super Mario 64 card ✓
- Judged the results → good enough ✓
- Internet search → not needed
- **Answer:** *"The first 3D Mario game is Super Mario 64, released in 1996 for the Nintendo 64."*

---

**Question 3:** *"Was Mortal Kombat X released for PlayStation 5?"*

- Checked the library → found Spider-Man 2 and Halo, but no Mortal Kombat X ✗
- Judged the results → not useful ✗
- Internet search → used → found Reddit and official PlayStation page
- **Answer:** *"Mortal Kombat X was not made for PlayStation 5. It was a PlayStation 4 game, but PlayStation 5 owners can still play it because the PS5 can run most older PS4 games."*

---

### Every Answer Comes With 3 Pieces of Information

UdaPlay does not just give you a plain answer. Every response includes:

| What You Get | What It Means |
|---|---|
| **The Answer** | The actual response to your question |
| **The Source** | Where it came from — the private library or the internet |
| **Confidence** | How sure UdaPlay is — High, Medium, or Low |

---

### UdaPlay Remembers What You Said Before

UdaPlay keeps a memory of your past questions and answers, saved in a file on your computer. Even if you close the program and open it again later, it loads the last 5 conversations so it has some background knowledge.

This also means it can handle follow-up questions naturally:

- You ask: *"When was Super Mario 64 released?"*
- UdaPlay answers: 1996, Nintendo 64
- You ask: *"What console was it on?"*
- UdaPlay knows "it" means Super Mario 64 → answers: Nintendo 64
- You ask: *"Was it a 3D game?"*
- UdaPlay still remembers → answers: Yes, it was one of the first 3D platform games

Without memory, the second and third questions would make no sense because UdaPlay would not know what "it" referred to.

---

## How the Two Files Connect

```
File 1 — Udaplay_01_starter_project.ipynb
  Loads 15 games → saves them to a folder called "chromadb" on your computer
          ↓
File 2 — Udaplay_02_starter_project.ipynb
  Opens that "chromadb" folder → builds the AI assistant on top of it
  AI assistant answers your questions using those 15 game cards
```

---

## How to Run This Project

**What you need:**
- Python installed on your computer
- Jupyter Notebook
- An API key from OpenAI (to power the AI)
- An API key from Tavily (a web search tool used when the library does not have the answer)

**Install the required tools:**
```
pip install chromadb openai python-dotenv tavily-python pydantic
```

**Create a file called `.env` in the same folder and add your keys:**
```
OPENAI_API_KEY=your_openai_key_here
CHROMA_OPENAI_API_KEY=your_openai_key_here
TAVILY_API_KEY=your_tavily_key_here
OPENAI_BASE_URL=https://openai.vocareum.com/v1
```

**Run in this order:**
1. Open `Udaplay_01_starter_project.ipynb` and run all cells top to bottom
2. Open `Udaplay_02_starter_project.ipynb` and run all cells top to bottom

---

## Course

This project is part of the **AI Agents with LLMs** course on Udacity.
