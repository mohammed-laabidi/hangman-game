<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&amp;size=30&amp;duration=3000&amp;pause=1200&amp;center=true&amp;vCenter=true&amp;width=900&amp;color=415EFC&amp;lines=Hangman;Word+guessing+game;Ten+categories%2C+seven+attempts" alt="Hangman" />

<p><strong>A word-guessing game with a virtual keyboard, seven allowed mistakes, and a drawing that fills in with each wrong letter.</strong></p>

</div>

<div align="center">

<a href="https://github.com/mohammed-laabidi/hangman-game"><img src="https://img.shields.io/github/stars/mohammed-laabidi/hangman-game?style=for-the-badge&amp;logo=github&amp;label=Stars" alt="GitHub stars" /></a>
<a href="https://github.com/mohammed-laabidi/hangman-game/fork"><img src="https://img.shields.io/github/forks/mohammed-laabidi/hangman-game?style=for-the-badge&amp;logo=github&amp;label=Forks" alt="GitHub forks" /></a>
<a href="https://github.com/mohammed-laabidi/hangman-game/issues"><img src="https://img.shields.io/github/issues/mohammed-laabidi/hangman-game?style=for-the-badge&amp;logo=github&amp;label=Issues" alt="GitHub issues" /></a>
<img src="https://img.shields.io/github/last-commit/mohammed-laabidi/hangman-game?style=for-the-badge&amp;logo=git&amp;label=Last%20Commit" alt="Last commit" />

</div>

<div align="center">

<a href="https://mohammed-laabidi.github.io/hangman-game/"><strong>Live Demo</strong></a>
&nbsp;&nbsp;|&nbsp;&nbsp;
<a href="https://github.com/mohammed-laabidi/hangman-game">Repository</a>

</div>

## Overview

Hangman is a browser implementation of the classic word game. A word is drawn at random from a local catalogue organised by category, and the player reveals it one letter at a time using an on-screen keyboard. Each incorrect letter adds a stage to the hangman drawing and increases the mistake counter; the seventh mistake ends the round.

The word list lives in `words.json`, which holds ten categories of ten words each, covering topics such as computers, fashion, sports, electronics, automotive, beauty, toys, books, and animals. The game reads this file with `fetch`, so it runs from a web server or from the GitHub Pages deployment.

The interface keeps a first-visit introduction in `localStorage`, so returning visitors go straight to the board.

## Features

<table>
<tr>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/keyboard.svg?color=%23415EFC" width="28" height="28" alt="Keyboard" />

### On-screen keyboard

Twenty-six letter buttons check the guess and mark used letters in red when they are not part of the word.

</td>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/list.svg?color=%23415EFC" width="28" height="28" alt="Categories" />

### Categorised word bank

`words.json` provides ten categories with ten words each, and the category name is displayed above the board as a hint.

</td>
</tr>
<tr>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/image.svg?color=%23415EFC" width="28" height="28" alt="Drawing" />

### Progressive drawing

Seven images in `hangman photos/` are swapped in one by one as mistakes accumulate, showing the gallows, head, and body.

</td>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/alert-circle.svg?color=%23415EFC" width="28" height="28" alt="Attempts" />

### Mistake counter

The header reports the current score as `incorrect guesses: n/7` and the round ends at the seventh error.

</td>
</tr>
<tr>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/check-circle.svg?color=%23415EFC" width="28" height="28" alt="End state" />

### Win and lose messages

When every letter is found the board shows a success message; when the attempts run out it shows a consolation message with a replay action.

</td>
<td width="50%" valign="top">

<img src="https://api.iconify.design/lucide/hard-drive.svg?color=%23415EFC" width="28" height="28" alt="First visit" />

### First-visit introduction

The rules panel is shown only once per browser; a `localStorage` flag skips it on later visits.

</td>
</tr>
</table>

## Technology Stack

<div align="center">

<img src="https://skillicons.dev/icons?i=html,css,js,git,github" alt="HTML, CSS, JavaScript, Git, and GitHub" />

</div>

| Technology | Purpose |
| --- | --- |
| HTML5 | Intro panel, board, and keyboard markup |
| CSS3 | Board layout, letter boxes, and two responsive breakpoints |
| JavaScript | Word selection, letter checks, drawing, and counters |
| JSON | Word catalogue stored in `words.json` |
| Fetch API | Loading the word catalogue at page start |
| Web Storage API | `localStorage` flag for the first-visit introduction |
| GitHub Pages | Static hosting of the live demo |

## Architecture

The game runs entirely in the browser. The only external resource is the local JSON catalogue, loaded once when the page starts.

```mermaid
flowchart TD
    Page["index.html"] --> Script["script.js"]
    Script -->|fetch words.json| Data["Word catalogue<br/>10 categories x 10 words"]
    Script --> Select["Pick random category and word"]
    Select --> Board["Create one box per letter"]
    Keyboard["Letter keyboard"] --> Check{"Letter in word?"}
    Check -->|Yes| Reveal["Reveal letter and mark box green"]
    Check -->|No| Mistake["Increment mistakes and swap drawing"]
    Mistake --> Final{"Seven mistakes?"}
    Final -->|Yes| Lose["Game over message"]
    Reveal --> Win{"All letters found?"}
    Win -->|Yes| Success["Victory message"]
```

## Application Flow

```mermaid
flowchart LR
    Open["Open the game"] --> Intro{"First visit?"}
    Intro -->|Yes| Rules["Rules panel"]
    Intro -->|No| Board
    Rules --> Start["Select Start"]
    Start --> Board["Random word and empty boxes"]
    Board --> Guess["Select a letter"]
    Guess --> Result{"Correct?"}
    Result -->|Yes| Fill["Letter revealed"]
    Result -->|No| Pen["Drawing advances"]
    Fill --> Finish{"Word complete?"}
    Pen --> Finish
    Finish -->|No| Guess
    Finish -->|Yes| Over["Win or lose message, then Replay"]
```

## Project Structure

```text
hangman-game/
├── index.html
├── style.css
├── script.js
├── words.json
├── hangman photos/
│   ├── status1.png
│   ├── status2.png
│   ├── status3.png
│   ├── status4.png
│   ├── status5.png
│   ├── status6.png
│   └── status7.png
└── README.md
```

## Getting Started

### Prerequisites

A modern browser. Because the game fetches `words.json`, it must be served over HTTP rather than opened as a local file.

### Installation

```bash
git clone https://github.com/mohammed-laabidi/hangman-game.git
cd hangman-game
python -m http.server 8000
```

Open `http://localhost:8000` in a browser.

## Usage

1. Read the introduction and select Start.
2. Read the category hint displayed above the board, then choose a letter.
3. Correct letters turn green and fill their boxes; wrong letters turn red and advance the drawing.
4. Reveal the whole word to win, or reach seven mistakes to lose.
5. Use Replay to reload the page with a new word, or Exit to close the tab.

Words are stored without spaces during the round, and the letter check replaces each found letter so a box is never filled twice.

## Deployment

The live demo is hosted on GitHub Pages from the repository root. The deployment serves `words.json` alongside the page, which is required for the game to start.

## Author

<table>
<tr>
<td valign="top">

**Mohammed Laabidi**

<a href="https://github.com/mohammed-laabidi"><img src="https://api.iconify.design/lucide/github.svg?color=%23415EFC" width="18" height="18" alt="GitHub" /> GitHub</a>
&nbsp;&nbsp;
<a href="https://www.linkedin.com/in/mohammed-laabidi-793a40436"><img src="https://api.iconify.design/lucide/linkedin.svg?color=%23415EFC" width="18" height="18" alt="LinkedIn" /> LinkedIn</a>
&nbsp;&nbsp;
<a href="mailto:mohammed-laabidi@gmail.com"><img src="https://api.iconify.design/lucide/mail.svg?color=%23415EFC" width="18" height="18" alt="Email" /> Email</a>

</td>
</tr>
</table>

---

If this project is useful to you, consider giving the repository a star.
