# Validating URLs With <span style="color:lightgreen;font-weight:bold;">REGEX</span>

Depending on your familiarity with JavaScript, you may already know that checking if a user has entered valid information can be accomplished with several built-in JS methods. For example, the three expressions below will all return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span> :

```JS
"Jane Doe".startsWith("J");

"Hello World".endsWith("World");

"A B C D".includes("A");
```

But what if you want to check for something more specific, or has a value that changes depending on user input? In those situations, <span style="font-weight:bold;color:lightgreen;">regular expressions</span> ( <span style="font-weight:bold;color:lightgreen;">regex</span> or <span style="font-weight:bold;color:lightgreen;">regexp</span> for short ) offer a powerful solution.

<span style="font-weight:bold;">Regular expressions</span> are comprised of a set of special characters that may seem to be completely random at first glance, but all serve a purpose in defining your desired search pattern.

## Summary

In this tutorial, we'll be looking at an example of how <span style="font-weight:bold;">regular expressions</span> can be utilized to check whether a user has entered a valid URL. The following example shows how this can be accomplished:

```JS
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

This <span style="font-weight:bold;">regex</span> search pattern will only return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span> if the compared string satisfies <span style="font-weight:bold;text-decoration:underline;">all</span> of the stated criteria. Lets do a quick breakdown on what, exactly, this expression is looking for:

- The string begins with either an <span style="font-weight:bold;">http</span> or <span style="font-weight:bold;">https</span> protocol, followed by a colon and two forward slashes <span style="font-weight:bold;">(optional)</span>
- The string has a domain name containing lowercase letters a-z, and at least one period or hyphen <span style="font-weight:bold;">(required)</span>
- The string has a top-level domain (like <span style="font-weight:bold;">.com</span>, <span style="font-weight:bold;">.org</span> or <span style="font-weight:bold;">.net</span>) that contains lowercase letters a-z, and is 2-6 characters long <span style="font-weight:bold;">(required)</span>
- The string has a path after the top-level domain that begins with a forward slash, can contain any <span style="font-weight:bold;">word</span> character (letters, numbers or underscores), and can contain both periods and hyphens <span style="font-weight:bold;">(optional)</span>
- The string ends with a trailing forward slash <span style="font-weight:bold;">(optional)</span>

In short, our expression is attempting to match URLs that start with http or https, followed by a domain name, a top-level domain of 2 to 6 characters, an optional path, and an optional trailing slash.

Don't worry if you don't understand how each criteria is being checked for yet! We'll be going into more detail below about the various special characters that make up a <span style="font-weight:bold;">regular expression</span>, how those characters work, and how to use them together.

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

Hi there! My name is Aster Oliva and I am, at the time of writing this, a student enrolled in a full-stack developer bootcamp through UC Berkeley. I am currently working towards a career in software/web development specializing in HTML/CSS, JavaScript & React/JSX. To see some of my other work, you can find me on GitHub at [github.com/Aoliva96](https://github.com/Aoliva96).

I hope you found my tutorial to be useful, and feel free to submit a comment if you have any improvements to suggest!
