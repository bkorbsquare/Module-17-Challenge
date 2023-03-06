# Diving into Regex: Dates

Regular Expressions (or Regex) are sequences of characters that define a search parameter. These sequences are comprised of Literal and Meta characters. Literal Characters are exactly what they sound like - a one to one exact copy of what you're searching for. An example of this would be "L" when searching for the letter L. Meta Characters represent a set of Literal Characters (or lack thereof), or their position. Examples of these include "\s\s" representing two white spaces, or "\z" matching the end of a string. We use Regex to query more complex parameters efficiently. 

## Summary

Here we'll break down the components of Regex, taking a specific look at an example focusing on dates. The following Regex can find dates in the format DD/MM/YYY or DD/MM/YY.

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/


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

### Quantifiers

### OR Operator

### Character Classes

### Flags

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
