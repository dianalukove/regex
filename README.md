# regex# Regex Tutorial: Zip-Code Validation

Welcome to my regex tutorial! Here, I will be summarizing the purpose and usage of regular expressions, also known as "regex". In this demonstration, I will show how the principle properties of regular expressions are applied to a zip-code validation regex.

## Introduction

A regex is a sequence of characters that specifies search query patterns to help developers match, locate, and manage text. Regex are language-agnostic, meaning that they can be used with any programming language.

Regex are extremely useful in validating and extracting information from any text by searching for matches of their specified patterns. Because of their flexibility, they can be applied to a wide range of uses, such as in algorithms, search engines, word processors, and even text-editors.

In this tutorial, we will be examining the following zip-code validation example.

```
^\d{5}(?:[-\s]\d{4})?$
```

This regex was written to satisfy three criteria conditions when validating zip codes. The zip codes it will find will match the following patterns:

1. 12345
2. 12345-6789
3. 12345 1234

Although it may look like a randomized set of characters, each of the elements of this regular expression has a specific meaning. Regular expressions are constructed from distinct building blocks. Let's dive into each of these elements together.

## Table of Contents

- [Anchors](#anchors)
- [Character Classes](#character-classes)
- [Quantifiers](#quantifiers)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Summary](#summary)

## Regex Components

### Anchors

Boundary matchers, more commonly known as "anchors", do not match a character. Rather, they match a boundary by examining the positions between characters. The most common anchors are `^` and `$`. The caret symbol `^` matches the beginning of a line, whereas the dollar sign `$` matches the end of the line. These two anchors are often used together to test when a string fully matches the pattern specified by the regex.

In our zip-code validation regex, we can see that the beginning of the expression is marked by the caret `^` and the end is marked by the dollar sign `$`. Therefore, our expression will search for strings that have their first digit as the first character on the line, and the last digit is the last character on the line.

### Character Classes

Character classes distinguish kinds of characters, such as distinguishing between letters and digits. In our example regex, we use the digit character class `\d`.

The digit character class is a character shorthand that matches any digit from 0 to 9. it is similar to the the expresssion [0-9]. The difference is that [0-9] will only ever match the characters `0123456789`, while `\d` may match other digit characters such as eastern arabic numerals `٠١٢٣٤٥٦٧٨٩`.

We also use the whitespace character class `\s`. This parameter within our regular expression will return a space, tab, carriage return, a line feed, or a form feed. In our example, `\s` is denoting that we want to return a space as a valid character in that position.

### Quantifiers

Quantifiers specify how many instances of a character, group, or character class must be present in a string for a match to be found. If a number is contained within curly brackets `{n}`, that means that the string matched must match exactly n number of times.

Reviewing our example, we can see that the quantifiers in our example include `{5}`, matching a string that is exactly 5 characters long, and `{4}`, matching a string that is exactly 4 characters long.

We also use the quantifier `(...)?`. A question mark `?` immediately following a character or group of characters indicates that our regex will match zero or one instance of that character or group of characters. In our example, this means that anything contained within the parenthesis is an optional matching parameter.

### Grouping and Capturing

You can group sub-patterns in sections enclosed in parenthesis. They group the contained expressions into one single unit. We saw one of the advantages of grouping above when speaking about quantifiers. Our regex example uses `(...)?`, where the entire expression inside of the parenthesis is treated as one unit. The question mark after this group indicates that our regex will match either zero or one instance of that group, making the grouped expression optional.

Grouping comes into play when determining which strings are captured by our regex. Regular expressions return strings that match the regex's specifications. However, there are times when you may not want to return certain parts of the data that you are parsing over. This is where capturing vs non-capturing groups come into play.

If you use a **capturing** group, denoted by your regex expression contained within a set of parentheses `(regex)`, then the return value is an array holding all the specific information you have gathered from your regex.

If you use a **non-capturing** group, denoted by `(?:regex)`, anything defined within the parenthesis of this regex expression will be excluded from the resulting array. This can be useful when you are trying to work with only specific parts of your data.

```
(?:[-\s]\d{4})
```

In our regex example, we use a **non-capturing** group `(?:...)`. This is useful because we only need to find and return the first 5 digits of the zipcode, while the remaining characters are useful in finding a match, but not necessary for us to understand the zip code.

### Bracket Expressions

Bracket expressions are lists of characters enclosed by square brackets `[]`. They will match any of the enclosed characters. You can specify a range of characters by using a hyphen, but if the hyphen appears as the first or last character enclosed in the square brackets, then it is taken as a literal hyphen to be included in the class as a normal character.

This applies to our regex example, which specifically searches for either a whitespace character, denoted by `\s`, or a hyphen in the `[-\s]` portion of our expression. The hyphen must be placed as the first or last character within the brackets so that it is not mistaken as a range character, like in the expression `[0-9]`.

### Summary

Now that we've discussed each individual element of our zip-code verification regex, let's put it all togther. As a refresher, here is our regex:

```
^\d{5}(?:[-\s]\d{4})?$
```

This regex matches any strings that meet the following conditions:

1. 12345
2. 12345-6789
3. 12345 1234

Therefore, our regular expression:

1. `^` Looks for the start of the string at the beginning of the line.
2. `\d{5}` Matches any string that contains digit characters and is 5 characters long. (satisfies conditions 1, 2, and 3)
3. `(...)` This is a grouping mechanism that works to define a set of requirements as one cohesive unit. This is important when we define our non-capturing group to exclude certain portions of our query results from the returned array. This is also important for step 4, where we define an optional parameter that applies to everything contained within these parenthesis.
   - `?:` This, paired with the surrounding grouping parenthesis, helps us define a non-capturing group so that anything contained within the parenthesis is not returned in the resulting array. This is useful because we only need to find and return the first 5 digits of the zipcode, while the remaining characters are useful in finding a match, but not necessary for us to understand the zip code.
   - `[-\s]` This uses a bracket expression to match either a hyphen (for condition 2) or a space (for condition 3) as a valid character.
   - `\d{4}` Matches any string that contains digit characters and is 4 characters long. (satisfies conditions 2 and 3)
4. `...?` The pattern before the question mark is considered optional. (satisfies condition 1)
5. `$` Denotes the end of the string as the last character in the line.

-Diana is a Full Stack Developer with a passion for learning. To browse her projects or find her contact information, visit her [GitHub] https://github.com/dianalukove
