# MattsCodingCorner - Regex-Tutorial

 My goal is to create a tutorial on a regular expressions (regex), breaking down each part and explaining its function. Navigate through the provided guide to make this tutorial both informative and accessible to fellow developers.

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

Regex anchors are special characters or sequences that don't match any actual characters in the text but instead represent positions within the text. They are used to assert whether a pattern appears at a specific location within a string. There are two main types of regex anchors:

1. **`^` - Caret (Beginning of Line Anchor):**
   - The caret (`^`) asserts that the pattern following it must appear at the beginning of a line.
   - For example, the regex `^Hello` will only match if the string starts with "Hello."

2. **`$` - Dollar Sign (End of Line Anchor):**
   - The dollar sign (`$`) asserts that the pattern preceding it must appear at the end of a line.
   - For example, the regex `World$` will only match if the string ends with "World."

Here are some practical examples of how to use these anchors:

- `^Hello`: Matches strings that start with "Hello."

  - `Hello, world!` - Match
  - `Hi there, Hello!` - No match

- `World$`: Matches strings that end with "World."

  - `Hello, World!` - Match
  - `World, Hello!` - No match

- `^Hello$`: Matches strings that consist of only "Hello."

  - `Hello` - Match
  - `Hello, world!` - No match

- `^$`: Matches empty lines (lines with no characters).

  - ` ` - Match (an empty line)
  - `Hello, world!` - No match

These anchors are crucial for specifying where a pattern should appear in a string, helping to ensure that a regex matches the desired parts of the text. They're particularly useful in scenarios like form validation, where you want to make sure that the input conforms to a specific format at the beginning or end of a line.

### Quantifiers

*notice the patterns*

Regex quantifiers are special characters in regular expressions that define how many times a particular element should be matched in the text. They allow you to define patterns that repeat or occur a specific number of times. Here are some common regex quantifiers:

1. **`*` - Asterisk (Zero or More):**
   - Matches zero or more occurrences of the preceding element. 
   - For example, `a*` will match "a," "aa," "aaa," and so on.

2. **`+` - Plus (One or More):**
   - Matches one or more occurrences of the preceding element. 
   - For example, `a+` will match "a," "aa," "aaa," but not an empty string.

3. **`?` - Question Mark (Zero or One):**
   - Matches zero or one occurrence of the preceding element. 
   - For example, `a?` will match "a" or an empty string.

4. **`{n}` - Exact Quantity:**
   - Matches exactly "n" occurrences of the preceding element.
   - For example, `a{3}` will match "aaa."

5. **`{n,}` - At Least "n" Quantity:**
   - Matches "n" or more occurrences of the preceding element.
   - For example, `a{2,}` will match "aa," "aaa," "aaaa," and so on.

6. **`{n,m}` - Between "n" and "m" Quantity:**
   - Matches between "n" and "m" occurrences of the preceding element.
   - For example, `a{2,4}` will match "aa," "aaa," or "aaaa," but not "a" or "aaaaa."

Quantifiers are especially useful when you need to match repeating patterns, such as finding email addresses, phone numbers, or dates in a text. They allow you to create more flexible and concise regex patterns to match various instances of the same element.

For example, to match a valid date format in MM/DD/YYYY, you could use the regex pattern `^\d{2}/\d{2}/\d{4}$`. This pattern specifies that there should be exactly two digits, followed by a slash, two more digits, another slash, and four digits to form a complete date. The `{2}` and `{4}` in the pattern are quantifiers that specify the exact quantity.

### Grouping Constructs

*break it down*

Grouping constructs in regular expressions allow you to treat part of a regular expression as a single unit or subpattern. They are enclosed within parentheses `(` and `)`. Grouping constructs serve several important purposes in regex:

1. **Capturing Groups:**
   - You can create capturing groups by placing parentheses around part of a regular expression. Capturing groups remember the text they match, making it accessible for further processing.
   - For example, if you have the regex `(\d{2})/(\d{2})/(\d{4})`, it will capture day, month, and year in a date format like "01/15/2023."

2. **Non-Capturing Groups:**
   - By adding `?:` at the beginning of a group `(?:...)`, you create a non-capturing group. It still groups the pattern but does not capture the matched text.
   - This is useful when you want to group parts of a pattern for logical grouping or to apply quantifiers without capturing the result.
   - For example, `(?:https?|ftp)://` matches URLs that start with "http://" or "https://" but does not capture the protocol.

3. **Backreferences:**
   - You can reference a previously captured group's content later in the regex using backreferences, typically denoted as `\1`, `\2`, etc. This is valuable for matching repeated content.
   - For example, the regex `(\w+) and \1` would match "word and word," where the second occurrence refers to the first captured word.

4. **Alternation:**
   - Groups can be used for alternation, where you want to match one of several patterns. You place the alternatives within parentheses.
   - For example, `(apple|banana|cherry)` matches any of the specified fruits.

5. **Grouping for Quantifiers:**
   - Groups allow you to apply quantifiers to a specific part of the pattern. For example, `(ab){3}` matches "ababab."

6. **Nested Groups:**
   - You can nest groups inside other groups to create more complex expressions. This is useful for handling intricate patterns.

Grouping constructs help you structure and control the behavior of regular expressions, making them a powerful tool for pattern matching, text extraction, and data manipulation. They also enhance code readability and maintainability by allowing you to break down complex regex into smaller, more understandable components.

### Bracket Expressions

*define the pattern*

In regular expressions, bracket expressions, also known as character classes, are used to define a set of characters that can match a single character at a specific position in the input text. They are enclosed within square brackets `[ ]` and allow you to specify a list of characters or character ranges that should be matched.

Here are some key points about bracket expressions in regex:

1. **Character Sets:**
   - Inside the brackets, you list the characters that you want to match. For example, `[aeiou]` matches any lowercase vowel (a, e, i, o, u).

2. **Character Ranges:**
   - You can define character ranges using a hyphen `-`. For example, `[a-z]` matches any lowercase letter, and `[0-9]` matches any digit.

3. **Negation:**
   - You can negate a character class by placing a caret `^` at the beginning. For example, `[^aeiou]` matches any character that is not a lowercase vowel.

4. **Special Characters within Character Classes:**
   - Some characters have special meanings within character classes. To match these special characters as literal characters, you can escape them with a backslash `\`. For example, `[-()]` matches either a hyphen or parentheses.

5. **Combining Character Classes:**
   - You can combine character classes within a larger regex pattern to create more complex matching rules. For example, `[A-Za-z0-9]` matches any alphanumeric character.

Here are a few examples of how bracket expressions are used in regex:

- `[aeiou]`: Matches any lowercase vowel.
- `[0-9]`: Matches any digit.
- `[^aeiou]`: Matches any character that is not a lowercase vowel.
- `[A-Za-z]`: Matches any uppercase or lowercase letter.
- `[\d\s]`: Matches any digit or whitespace character.
- `[0-9a-fA-F]`: Matches a hexadecimal digit.

Bracket expressions provide a concise and powerful way to define character patterns in regular expressions. They are especially useful when you want to match specific sets of characters or ranges of characters within your text data.

### Character Classes

*what a crazy group of characters*

In regular expressions (regex), character classes, also known as character sets or character ranges, are a way to specify a group of characters that can match a single character at a particular position in the input text. They are defined using square brackets `[ ]` and allow you to express a set of characters you want to match in a more concise manner. Character classes are particularly helpful when you want to match characters that share common characteristics or attributes.

Here are some key characteristics of character classes within regex:

1. **Square Brackets:** Character classes are enclosed within square brackets, such as `[abc]`, which matches any of the characters 'a,' 'b,' or 'c.'

2. **Character Sets:** Inside the square brackets, you list the characters you want to match. For example, `[aeiou]` matches any lowercase vowel.

3. **Character Ranges:** You can define character ranges within character classes using a hyphen `-`. For example, `[a-z]` matches any lowercase letter from 'a' to 'z,' and `[0-9]` matches any digit from '0' to '9.'

4. **Negation:** You can negate a character class by placing a caret `^` at the beginning. For example, `[^aeiou]` matches any character that is not a lowercase vowel.

5. **Special Characters:** Some characters, like hyphens or square brackets, may have special meanings inside character classes. To match these characters literally, you can escape them with a backslash. For instance, `[-()]` matches either a hyphen or an open or close parenthesis.

6. **Combining Character Classes:** You can combine multiple character classes within a larger regex pattern to match more complex patterns. For instance, `[A-Za-z0-9]` matches any alphanumeric character.

Character classes in regex are a powerful way to specify patterns that involve sets of characters with common characteristics. They enhance the flexibility and expressiveness of regular expressions, making it easier to match and manipulate text data.

### The OR Operator

*It's my way OR the highway*

In regular expressions (regex), the OR operator is represented by the vertical bar `|`. It allows you to specify alternative patterns, and it matches the text against any of the provided alternatives. Essentially, it functions as a logical OR, enabling you to match different patterns within a single regular expression.

Here are some key points about the OR operator in regex:

1. **Syntax:** The OR operator is denoted by `|`, and it's used to separate alternative patterns. For example, `pattern1|pattern2` matches either `pattern1` or `pattern2`.

2. **Matching Alternatives:** When the regex engine encounters the OR operator, it will attempt to match the text against the patterns on either side of the `|`. If any of the alternatives matches, the whole regular expression is considered a match.

3. **Priority:** The regex engine prioritizes the leftmost alternative that matches. If both alternatives are valid matches, it selects the one that appears first in the regular expression.

Here are some examples of how the OR operator is used in regex:

- `apple|banana` matches either "apple" or "banana" in the text.

- `(red|green|blue) car` matches "red car," "green car," or "blue car."

- `\d{3}|\d{4}` matches a sequence of either three or four digits.

- `(Jan|Feb|Mar)uary` matches "January," "February," or "Marchuary."

- `http(|s)://` matches URLs that start with "http://" or "https://".

The OR operator is particularly useful when you want to find text that could appear in various forms or when you want to provide multiple options for matching within a single regular expression. It allows for more flexible and concise regex patterns, making it easier to capture different variations of the same information.

### Flags

*Flag it down*

Flags in regular expressions (regex) are modifiers that you can append to the end of a regex pattern to change how the pattern is applied during matching. Flags provide additional control and customization of the matching process. In most regex implementations, flags are usually single characters that follow the closing delimiter (usually a forward slash `/`) of the regex pattern. The most common flags in regex are:

1. **Case-Insensitive (`i`):** When you use the `i` flag, the regex will perform a case-insensitive match, meaning it will ignore the distinction between uppercase and lowercase letters. For example, `/apple/i` would match "Apple," "aPpLE," "aPpLe," and so on.

2. **Global (`g`):** The `g` flag indicates that the regex should perform a global search, which means it will find all occurrences of the pattern in the input string rather than stopping after the first match. For instance, `/apple/g` will find all instances of "apple" in the input text.

3. **Multiline (`m`):** The `m` flag, also known as the multiline flag, changes the behavior of the `^` and `$` anchors. When this flag is used, `^` matches the start of each line, and `$` matches the end of each line, rather than the start and end of the entire string.

4. **Sticky (`y`):** The `y` flag, or sticky flag, indicates that the regex should start the search from the end of the previous match. This is useful when you want to find consecutive matches in a string.

5. **Unicode (`u`):** The `u` flag is used for handling Unicode characters in the regex pattern and the input string. It's essential when working with non-ASCII characters or extended Unicode character sets.

6. **Dotall (`s`):** The `s` flag, or dotall flag, changes the behavior of the dot `.` metacharacter to match all characters, including newline characters. By default, the dot `.` does not match newline characters.

7. **Extended (`x`):** The `x` flag allows you to write more readable and well-formatted regex patterns. It ignores whitespace and line breaks, allowing you to add comments and indentation to make the regex more understandable.

Flags provide flexibility and control over how regex patterns are applied. Depending on your specific matching requirements, you can use one or more flags to modify the behavior of the regex. For example, you might use the `i` flag when performing a case-insensitive search, or the `g` flag when finding multiple occurrences of a pattern within a text.

### Character Escapes

*Don't let him escape*

Character escapes in regular expressions (regex) are special sequences that begin with a backslash `\` followed by a character, which is used to match specific characters or character classes that have special meanings in regex. These escapes allow you to treat these special characters as literal characters, so you can match them in your regex patterns. Character escapes are particularly useful when you need to match characters that are typically reserved for metacharacters. 

Here are some common character escapes in regex:

1. **`\d`**: Matches any digit from 0 to 9. It is a shorthand for `[0-9]`.

2. **`\D`**: Matches any character that is not a digit. It is the negation of `\d`.

3. **`\w`**: Matches any word character, which includes letters, digits, and underscores. It is equivalent to `[a-zA-Z0-9_]`.

4. **`\W`**: Matches any non-word character, which is the negation of `\w`.

5. **`\s`**: Matches any whitespace character, including spaces, tabs, and line breaks.

6. **`\S`**: Matches any non-whitespace character, which is the negation of `\s`.

7. **`\n`**: Matches a newline character.

8. **`\t`**: Matches a tab character.

9. **`\r`**: Matches a carriage return character.

10. **`\v`**: Matches a vertical tab character.

11. **`\f`**: Matches a form feed character.

12. **`\cX`**: Matches a control character, where `X` is any letter. For example, `\cA` represents the ASCII control character `CTRL-A`.

13. **`\xhh`**: Matches a character specified by its hexadecimal ASCII code. For example, `\x41` matches the letter 'A'.

14. **`\uhhhh`**: Matches a Unicode character specified by its hexadecimal code point. For example, `\u00E9` matches the character 'é'.

15. **`\\`**: Matches a literal backslash character.

Using character escapes allows you to search for specific characters in your text without worrying about their special meaning as regex metacharacters. They are particularly useful when you want to match characters with predefined meanings or control codes in a regex pattern.

## Author

As you've made it too my repository I've written this tutorial file. I've used the sources below to make it possible and help me better understand Regular Expressions. 

- ![regex 101](https://regex101.com/)
- ![sitepoint](https://www.sitepoint.com/learn-regex/)
- ![Regular-Expressions.info](https://www.regular-expressions.info/)
- ![RegexOne](https://regexone.com/)
- ![Regular-Expressions(Youtube)](https://www.youtube.com/playlist?list=PL4cUxeGkcC9g6m_6Sld9Q4jzqdqHd2HiD)

*for the formatting help*
- ![Markdown-Cheat-Sheet](https://www.markdownguide.org/cheat-sheet/)
