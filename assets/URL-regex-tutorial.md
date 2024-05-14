# Validating URLs With <span style="color:lightgreen;font-weight:bold;">REGEX</span>

Depending on your familiarity with JavaScript, you may already know that checking if a user has entered valid information can be accomplished with several built-in JS methods. For example, the three expressions below will all return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span>:

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
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
```

This <span style="font-weight:bold;">regex</span> search pattern will only return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span> if the compared string satisfies <span style="font-weight:bold;text-decoration:underline;">all</span> of the stated criteria. Lets do a quick breakdown on what, exactly, this expression is looking for:

- <span style="font-weight:bold;">(Optional):</span> The string begins with either an <span style="font-weight:bold;">http</span> or <span style="font-weight:bold;">https</span> protocol, followed by a colon and two forward-slashes
- <span style="font-weight:bold;">(Required):</span> The string has a domain name containing lowercase letters a-z, and at least one period or hyphen
- <span style="font-weight:bold;">(Required):</span> The string has a top-level domain (like <span style="font-weight:bold;">.com</span>, <span style="font-weight:bold;">.org</span> or <span style="font-weight:bold;">.net</span>) that contains lowercase letters a-z, and is 2-6 characters long
- <span style="font-weight:bold;">(Optional):</span> The string has a path after the top-level domain that begins with a forward-slash, can contain any <span style="font-weight:bold;">word</span> character (letters, numbers or underscores), as well as both periods and hyphens
- <span style="font-weight:bold;">(Optional):</span> The string ends with a trailing forward slash

In short, our expression is attempting to match URLs that start with http or https, followed by a domain name, a top-level domain of 2 to 6 characters, an optional path, and an optional trailing slash. The following code utilizing our example expression should return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span>:

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
const string = "https://github.com/Aoliva96/regex-tutorial";

const isMatch = regex.test(string);
console.log(isMatch); // Expected output: true
```

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

<span style="font-weight:bold;">Regular expressions</span> are literals, meaning they must be wrapped in forward-slashes on both ends to be recognized as expressions in JavaScript. Alternatively, it is also possible to create a regex object by using a <span style="font-weight:bold;">RegExp Constructor</span>. For this tutorial, we will be using the literal notation, but feel free to review the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) on <span style="font-weight:bold;">RegExp</span> if you're curious about the alternate method.

Now let's dive in and take a closer look at the various componenets of a regex!

### Anchors

Both the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> and dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> symbols are considered to be <span style="font-weight:bold;">anchors</span>.

The caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor symbol is used to start the regex pattern, specifying that the string should begin with whatever characters directly follow it. This could be implemented in one of two ways:

- Checking the string for an exact match, such as <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^RegEx</span>, which would match either <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"RegEx"</span> or <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"RegEx Tutorial"</span>. Due to regex being <span style="font-weight:bold;">case-sensitive</span>, it would not match a string beginning with <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"regex"</span>.
- Checking the string against a range of possible matches. This is accomplished using <span style="font-weight:bold;">bracketed expressions</span>, which we'll go over in its own section.

The dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor symbol is used to end the regex pattern, specifying that the string should end with whatever characters directly precede it. The dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor accepts either an exact string to match or a range of possible matches, same as the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor.

Lets refer back to the first and last parts of our URL matching example:

```JS
const regex = /^(https?:\/\/)? ... \/?$/;
```

FIrst, our regex checks if the string begins with whatever is within the parentheses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">( )</span> (which separate it from the rest of the expression) directly following the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor. In our case it checks for an http or https protocol followed by a colon and two forward-slashes, either will match due to the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> <span style="font-weight:bold;">quantifier</span> symbol after the "s" in https. This section is also optional due the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier outside the parentheses.

In the last part of our expression, we are checking if the string ends in a trailing forward-slash, as those characters directly precede the dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor. It is again optional due to the presence of the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier.

Remember, in literal notation, if we want to check for a forward-slash it must be <span style="font-weight:bold;">escaped</span> with a back-slash each time. We'll talk about the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> and other quantifiers in the next section.

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
