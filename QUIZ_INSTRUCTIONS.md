# OMSCS Quiz Data Format

## Question Format

Every quiz is **multiple choice with exactly 4 options: A, B, C, D**, plus an **"I don't know"** option.

- If I pick A/B/C/D → store `userAnswer` as the chosen letter, `correct` as true/false, ask for confidence (1/2/3)
- If I pick "I don't know" → store `userAnswer: "?"`, `correct: false`, `confidence: 1` automatically (no need to ask)

All 4 options must always be saved, along with `correctOption` and `userAnswer`.

## JSON Schema

```json
{
  "id": "quiz_001",
  "date": "2026-03-03T22:00:00Z",
  "course": "CS 6601 - Artificial Intelligence",
  "topic": "Search (BFS, DFS, A*)",
  "question": "What is the time complexity of A* in the worst case?",
  "options": {
    "A": "O(n)",
    "B": "O(b^d)",
    "C": "O(log n)",
    "D": "O(n^2)"
  },
  "correctOption": "B",
  "userAnswer": "A",
  "correct": false,
  "difficulty": "easy",
  "confidence": 2
}
```

## Field Reference

| Field | Type | Notes |
|-------|------|-------|
| `id` | string | Sequential: `quiz_001`, `quiz_002`, … |
| `date` | string | ISO 8601 UTC |
| `course` | string | Full name, e.g. `CS 6601 - Artificial Intelligence` |
| `topic` | string | Must match a key in `topic_stats` |
| `question` | string | Full question text |
| `options` | object | All 4 options — keys A, B, C, D |
| `correctOption` | string | The correct option letter: `A`, `B`, `C`, or `D` |
| `userAnswer` | string | The option I chose: `A`, `B`, `C`, `D`, or `"?"` for I don't know |
| `correct` | boolean | `true` if `userAnswer === correctOption` (always `false` when `"?"`) |
| `difficulty` | string | `easy`, `medium`, or `hard` |
| `confidence` | number | `1` = guessed, `2` = somewhat sure, `3` = confident — always `1` when `userAnswer` is `"?"` |
