# Teleprompter Code Review & Improvement TODO

This document outlines the findings from the code review of the Voice-Tracked Teleprompter (`index.html`).

## 1. Code Simplification & Performance

### [High Priority] Efficient Highlight Updates
*   **Observation:** `updateHighlight(index)` iterates through every word (`O(N)`) on every match.
*   **Problem:** Performance degrades as the script grows, especially on mobile.
*   **Action:** Update only the previous and current word classes (`O(1)`).

### [Medium Priority] DOM Element Caching
*   **Observation:** Frequent `document.getElementById` calls during highlighting and manual jumps.
*   **Action:** Store element references in `scriptData` during the `preparePrompterText` phase.

### [Low Priority] Paragraph Navigation Optimization
*   **Observation:** "back paragraph" uses repeated `findIndex` calls.
*   **Action:** Pre-calculate paragraph start indices during script parsing.

## 2. Errors in Approach

### [High Priority] Phrase Matching Word Boundaries
*   **Observation:** Uses `.join('')` for matching (e.g., `["apple", "pie"]` -> `"applepie"`).
*   **Problem:** Removes word boundaries, leading to false positives.
*   **Action:** Use `.join(' ')` or compare word arrays directly.

### [DONE] Static Matching Window in Long Utterances
*   **Observation:** `maxAllowedForward` was anchored to `currentIndex` for the entire `onresult` loop.
*   **Problem:** If a user speaks a long phrase (longer than the `LOOKAHEAD_WINDOW`), the prompter "hit a wall" and could not progress further until the next recognition event.
*   **Solution:** Anchored `maxAllowedForward` to the progressively updated `potentialNewIndex`.

### [DONE] Redundant Transcript Processing
*   **Observation:** Aggregated last 5 results every time, re-processing old words.
*   **Problem:** Inefficient and redundant searching.
*   **Solution:** Processed only starting from `event.resultIndex - 1` to target newly changed speech data efficiently.

### [Low Priority] Verbal Command Latency
*   **Observation:** Navigation commands call `recognition.stop()`.
*   **Problem:** Causes a brief listening gap while waiting for `onend` to restart.
*   **Action:** Update index and scroll without stopping recognition for navigation-only commands.

## 3. Edge Case Issues

### [High Priority] Duplicate Phrases in Lookahead
*   **Observation:** Matcher jumps to any match in `LOOKAHEAD_WINDOW`.
*   **Problem:** If a phrase repeats within the window, the prompter may jump to the wrong one.
*   **Action:** Implement "Proximity Weighting" to prefer matches closer to the current word.

### [Medium Priority] Hyphenated Words normalization
*   **Observation:** Inconsistent tokenization of hyphenated words between script parsing and Speech API.
*   **Problem:** Matches fail when "voice-tracked" is treated as one word in the script but two in speech.
*   **Action:** Normalize tokens by stripping hyphens or treating them as multi-word N-grams consistently.

### [Medium Priority] Stop-Word Jitter
*   **Observation:** Common words ("the", "and") have high weights.
*   **Problem:** Noise can trigger accidental jumps to common words.
*   **Action:** Require N > 1 matches for common stop-words.
