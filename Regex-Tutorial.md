# Title Regex-Tutorial

 My goal is to create a tutorial on a specific regular expression (regex), breaking down each part and explaining its function. Navigate through the provided guide to make this tutorial both informative and accessible to fellow developers.

## Summary

**Matching Email Addresses**

Regex: `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`

This regular expression is designed to validate email addresses. It consists of three main parts:

1. `^[a-zA-Z0-9._%+-]+`: This part matches the local part of the email address before the '@' symbol. It allows alphanumeric characters, periods, underscores, percent signs, plus signs, and hyphens.

2. `@`: This part matches the '@' symbol, which separates the local part from the domain part of the email.

3. `[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`: This part matches the domain part of the email. It allows alphanumeric characters, hyphens, and periods. The '2' in `{2,}` enforces that the top-level domain (TLD) must have at least two characters.

Here's a code snippet in JavaScript to use this regex for email validation:

```javascript
const emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
const email = "example@email.com";

if (emailRegex.test(email)) {
    console.log("Valid email address");
} else {
    console.log("Invalid email address");
}
```

This code uses the `test` method of the regex to check if the email is valid according to the specified pattern.

    
## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

*Anchors are your friend*

Regex anchors are special characters or sequences that don't match any actual characters in the text but represent positions within the text. They're used to assert whether a pattern appears at a specific location within a string. 

There are two main types of regex anchors- 

1. '^' - Caret(Beginning of Line Anchor): The caret('^') asserts that the pattern following it must appear at the beginning of a line. 

### Quantifiers

### Grouping Constructs

### Bracket Expressions

### Character Classes

### The OR Operator

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
