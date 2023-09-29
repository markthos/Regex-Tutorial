# Cracking The Code: Regex Demystified

In a coding galaxy not so far away, regular expressions, or regex for short, emerge as the guiding force of pattern recognition and text manipulation. These powerful tools allow programmers to bring balance to the chaos that can be data validation and text processing. In this presentation, prepare to embark on an syntactic journey into the formidable realm of regular expressions. Together, we will deconstruct their intricate components and uncover the extraordinary applications they hold.

## Summary

In this presentation, we will explore the fundamental components of regular expressions and their usage. We will cover topics such as anchors, quantifiers, the OR operator, character classes, flags, grouping and capturing, bracket expressions, greedy and lazy matching, boundaries, back-references, and look-ahead and look-behind assertions. Below is an example of a regex pattern for an email match that we will analyze:

```js
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

In regular expressions, anchors are special characters or symbols used to specify positions within a string where a match should occur. Anchors do not match any characters themselves; instead, they define the relationship between the pattern and the input string. There are two common types of anchors in regex: the ```^``` anchor and the ```$``` anchor. 

The ```^``` anchor is used to match the start of a line or string and asserts that the pattern must match at the start of the string.  In this case that refers to the grouping pattern ```([a-z0-9_\.-]+)```, which represents the username of the email. 

The ```$``` anchor is used to match the end of a line or string. In this case that refers to the grouping pattern ```([a-z\.]{2,6})```, which represents the top-level domain of the email. 


### Quantifiers

Quantifiers like ```*, +, and ?``` are essential for specifying the number of times a character or group should be matched. We'll dive into their usage and examples. The ```*``` quantifier matches zero or more consecutive occurrences of the preceding character or group.  For example, ```do*g``` matches ```dg```, ```dog```, and ```doog```. The ```+``` quantifier matches one or more consecutive occurrences of the preceding character or group. For example, ```do+g``` matches ```dog``` and ```doog```, but not ```dg```. The ```?``` quantifier matches zero or one occurrence of the preceding character or group. For example, ```do?g``` matches ```dg``` and ```dog```, but not ```doog```.

In this case we find the ```+``` quantifier here ```([a-z0-9_\.-]+)``` and here and in the second grouping. In this example the quantifier specifies that there must be one or more of the characters from the grouping pattern ```[a-z0-9_\.-]``` in the match.

Quantifiers like ```{n}, {n,}, {n,m}, and {,n}``` are more advanced and add scope to our match. The ```{n}``` quantifier is the exact quantifier and it matches exactly ```n``` occurrences of the preceding character or group. For example, ```d{3}``` would match ```ddd``` but not ```dd``` or ```dddd```. The ```{n,}``` quantifier is the minimum quantifier and it matches ```n``` or more occurrences of the preceding character or group. For example, ```d{3,}``` would match ```ddd``` and ```dddd``` but not ```dd```. The ```{n,m}``` quantifier is the range quantifier and it matches between ```n``` and ```m``` occurrences of the preceding character or group. For example, ```{2,4}``` would match ```dd```, ```ddd```, and ```dddd``` but not ```d``` or ```ddddd```. Lasly, the ```{,n}``` quantifier is the maximum quantifer and it matches ```n``` or less occurrences of the preceding character or group. For example, ```{,3}``` would match ```d```, ```dd```, and ```ddd``` but not ```dddd```.

in this case we find the range quantifer ```{n,m}``` in the last grouping ```([a-z\.]{2,6})```. In this example the quantifer specifies that there must be between 2 and 6 characters from the grouping pattern ```[a-z\.]``` in the match.

### OR Operator

The OR operator ```(|)``` allows us to match one of several alternatives. This works similar to the OR logic function in most coding languages in that at least one of the provided patterns must match for the overall expression to be considered a match. For example ```apple|banana``` would match either ```apple``` or ```banana```. It is important to note that regex evalutes patterns from left to right. This means that when one of the patterns is found it considers that a match and moves on.  For example ```apple|app``` would match ```apple``` in ```'apple pie'``` and not ```app``` because it prefers the first matching pattern.

### Character Classes

Character classes like ```[a-zA-Z0-9]```, ```[^abc]```, and ```\``` help us define a set of characters that can match a single character at a specific position in the input string. Character classes allow us to specify a range of characters, a set of characters, or predefined character groups, making your regex patterns more concise and flexible. Character classes are enclosed in square brackets ```[]``` which acts like an array of options to choose from. For example, ```[ab12]``` matches any single character that is either ```a```, ```b```, ```1```, or ```2```. We can specify ranges in the square brackets and chain them without spaces. For example, ```[a-zA-Z0-9]``` matches any single characters that are lowercase letters, uppercase letters, and/or digits. We can also negate a caracter class by putting a caret ```^``` at the beginning of a character class.  For example, ```[^abc]``` matches any character that is not ```a```, ```b```, or ```c```.  Adding a ```\``` before a special charect to match a character that is a regex special character without reading it as a special character. This is referred to as escaping characters.  For example, ```dog\?``` allows the option of searching for ```'dog?'``` without reading the regex quantifier ```?```.

In this example ```[a-z0-9_\.-]```, allows any single characters that are lowercase letters, digits, underscores, hyphens and/or periods to be used for matching.

There are also predefined classes that provide shorthand for common character classes.  
- ```\d``` matches any digit (equivalent to [0-9])
- ```\D``` matches any non-digit (equivalent to [^0-9])
- ```\w``` matches any word character (letters, digits, or underscores)
- ```\W``` matches any non-word character (equivalent to [^a-zA-Z0-9_])
- ```\s``` matches any whitespace character (spaces, tabs, line breaks)
- ```\S``` matches any non-whitespace character

In this example ```[\da-z\.-]```, allows any single characters that are lowercase letters, digits, hyphens and/or periods to be used for matching. This is the same as before but the ```/d``` allows ```[0-9]``` digits to be used for matching.

### Flags

Flags, also known as modifiers or options, are settings in regular expressions (regex) that modify the behavior of the pattern matching process. These flags are added after the closing delimiter of a regex expression and are typically represented as single letters. Flags help you control how regex patterns are applied to the input string.  Here are four common flags and what they accomplish.


- Case-Insensitive Matching ```(i flag)```: The ```i``` flag makes the regex pattern match characters regardless of their case (uppercase or lowercase).
For example, ```/apple/i``` matches ```'apple'```, ```'Apple'```, and ```'aPpLe'```.

- Global Matching ```(g flag)```: The ```g``` flag enables global matching, which means the regex pattern will search for all occurrences of the pattern in the input string, rather than stopping after the first match.
For example, ```/a/g``` would find all occurrences of ```'a'``` in the input string.

- Multiline Matching ```(m flag)```: The ```m``` flag, also known as the multiline flag, changes how the ```^``` and ```$``` anchors behave. Without this flag, ```^``` and ```$``` match the start and end of the entire string. With the m flag, they match the start and end of each line within a multiline string.
For example, ```/^abc/m``` matches ```abc``` at the start of each line in a multiline string.

- Single-Line/Dot-All Mode ```(s flag)```: The ```s``` flag, also known as the single-line or dot-all flag, alters the behavior of the dot . metacharacter. Without this flag, ```'.'``` matches any character except a newline. With the ```s``` flag, . matches any character, including newlines.
For example, ```/a.b/s``` would match ```'a\nb'``` in a multiline string.

If we wanted to use our expression to search for all emails in a string we would add ```m``` to the closing delimiter like this.  
```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/m```

### Grouping and Capturing

Regex groups ```( )``` are used for capturing and grouping parts of a pattern. They serve multiple purposes, such as:

- Capturing: You can use groups to capture specific portions of a matched text. For example, if you want to extract the username and domain from an email address, you can create two capture groups like this: ```^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$```. In this regex, there are three capture groups: one for the username, one for the domain, and one for the top-level domain.

- Grouping: Parentheses are also used for grouping and applying quantifiers or alternation to a set of characters. For instance, ```(ab)+``` matches one or more occurrences of ```'ab'``` together.

- Back-referencing: Once you've captured a group, you can refer to it later in the regex using back-references. For example, if you capture a date as ```(\d{2})/(\d{2})/(\d{4})```, you can reference these captured groups later in the regex or in a replacement pattern using ```\1```, ```\2```, and ```\3```.

### Bracket Expressions

Bracket expressions ```[ ]``` allow us to create custom character classes for precise matching. Here's how they work:

- ```[aeiou]``` matches any single vowel.
- ```[^aeiou]``` matches any single character that is not a vowel.
- ```[0-9]``` matches any single digit.
- ```[A-Za-z]``` matches any single uppercase or lowercase letter.

You can also combine multiple character classes within brackets for more complex patterns. For example, ```[A-Za-z0-9]``` matches any alphanumeric character.

In our example ```[a-z0-9_\.-]```, allows any single characters that are lowercase letters, digits, underscores, hyphens and/or periods to be used for matching.

### Greedy and Lazy Match

Greedy and lazy matching affect the way regex handles repetition:

- Greedy Matching: By default, quantifiers like ```*``` and ```+``` are greedy, meaning they match as much as possible. For example, in the regex ```a.*b```, if we search for ```'afooob'```, it will match the entire string ```'afooob'``` because ```.*``` greedily consumes everything between ```'a'``` and ```'b'```.

- Lazy Matching (Non-Greedy): To make a quantifier lazy, we can add a ```?``` after it. For example, ```a.*?b``` would match ```'ab'``` in ```'afooob'``` because ```.*?``` matches as little as possible while still allowing the overall regex to match.

We can see here, ```/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/```, that our example is greedy in some of it's matching.  Notice the ```+``` in two spots of the expression.

### Boundaries

Word boundaries ```\b``` and non-word boundaries ```\B``` are crucial for precise matching within text:

- ```\bword\b``` matches the word ```'word'``` as a whole word, not as part of another word (e.g., it does not match ```'word'``` in ```password'```).

- ```\Bword\B``` matches ```'word'``` only when it's part of another word (e.g., it matches ```'password'``` but not ```'word'``` by itself).

### Back-references

Back-references ```(\1, \2, etc.)``` enable us to refer to previously captured groups within a regex pattern. Here are some examples:

- If you capture a date as ```(\d{2})/(\d{2})/(\d{4})```, you can use ```\1``` to refer to the captured day, ```\2``` for the month, and ```\3``` for the year.

- This is especially useful when you want to ensure that the same text appears later in the string, such as validating that an opening and closing tag match in HTML: ```<(\w+)>(.*?)<\/\1>```.

### Look-ahead and Look-behind

Look-ahead and look-behind assertions ```(?=...)``` and ```(?<=...)``` allow us to match text based on what comes before or after it:

- Positive Look-ahead ```(?=...)``` checks if a certain pattern is followed by another pattern. For example, ```foo(?=bar)``` matches ```'foo'``` only when it's followed by ```'bar'```.

- Positive Look-behind ```(?<=...)``` checks if a certain pattern is preceded by another pattern. For example, ```(?<=foo)bar``` matches ```'bar'``` only when it's preceded by ```'foo'```.

## Author

[Mark E. Thostesen](https://github.com/markthos)

A Full Stack Web-Developer NOOB
