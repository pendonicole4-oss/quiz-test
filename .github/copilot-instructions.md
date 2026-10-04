# Copilot instructions

## Project structure and architecture

This repository is a single-file, dependency-free browser application. The page structure, theme and responsive styles, quiz content, interaction logic, and results screen all live in the root `index.html`; there is no separate build pipeline or module boundary.

The quiz is data-driven: the `questions` array supplies each prompt, options, correct option index, and explanatory fact. `renderQuestion()` builds the answer buttons for the current item, `chooseAnswer()` locks the question and updates feedback and score, and `showResults()` / `restart()` switch between the quiz and results states. Keep these transitions and the displayed progress, score, and accessibility state in sync when changing quiz behavior.

## Commands and validation

There are no configured build, test, or lint commands. Run the app by opening `index.html` directly in a browser. The repository's VS Code MCP configuration provides Playwright for browser checks. For a focused check, answer questions using both keyboard and pointer, verify correct and incorrect feedback and score changes, complete all ten questions, and restart from the results screen.

## Code conventions

- Keep the app self-contained in `index.html`; use browser-native HTML, CSS, and JavaScript rather than adding a framework or runtime dependency.
- Keep quiz content in the `questions` data array and derive displayed question and result state from that data and the current score.
- Preserve the existing design system: CSS custom properties define light and dark palettes, `prefers-color-scheme` selects the palette, and responsive and reduced-motion behavior are handled in CSS media queries.
- Use native `<button>` elements for answers and actions. Maintain visible keyboard focus, focus transitions after answering and when showing results, and the existing live announcements for changing question, score, and feedback.
- Build answer labels with DOM text nodes/text content, and retain the correct/incorrect classes and feedback states so answer content is not interpreted as markup.
