# Quiz JSON Format Guide

This document explains how to write question files for the quiz website.

-----

## File Format

Questions are stored in a `.json` file as an **array of question objects**. Each object represents one question.

```json
[
  { ... },
  { ... }
]
```

-----

## Question Structure

Each question object has three required fields:

|Field     |Type            |Description                                               |
|----------|----------------|----------------------------------------------------------|
|`question`|string          |The question prompt shown to the user                     |
|`options` |array of strings|The list of answer choices                                |
|`answer`  |string          |The correct answer — must exactly match one of the options|

-----

## Example

```json
[
  {
    "question": "What is the capital of France?",
    "options": ["London", "Berlin", "Paris", "Madrid"],
    "answer": "Paris"
  },
  {
    "question": "Which mathematical symbol is used for Pi?",
    "options": ["∑", "Ω", "π", "∆"],
    "answer": "π"
  }
]
```

-----

## Rules

- **`answer` must exactly match an option.** The comparison is case-sensitive, so `"paris"` will not match `"Paris"`.
- **Include at least 2 options** per question. 4 options is the recommended standard.
- **Each option in a question should be unique.** Duplicate options are confusing and may cause issues.
- **Unicode characters are supported** — you can use symbols, accented letters, emoji, etc., as shown in the Pi example above.
- The file must be **valid JSON**. Use a validator like [jsonlint.com](https://jsonlint.com) if you’re unsure.

-----

## Common Mistakes

### ❌ Answer doesn’t match any option

```json
{
  "question": "What color is the sky?",
  "options": ["Red", "Blue", "Green"],
  "answer": "blue"
}
```

`"blue"` ≠ `"Blue"` — the answer won’t be recognized as correct.

### ✅ Fixed

```json
{
  "question": "What color is the sky?",
  "options": ["Red", "Blue", "Green"],
  "answer": "Blue"
}
```

-----

### ❌ Answer is not in the options list

```json
{
  "question": "What is 2 + 2?",
  "options": ["3", "5", "6"],
  "answer": "4"
}
```

`"4"` is not one of the options — the question can never be answered correctly.

### ✅ Fixed

```json
{
  "question": "What is 2 + 2?",
  "options": ["3", "4", "5", "6"],
  "answer": "4"
}
```