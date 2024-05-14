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

This <span style="font-weight:bold;">regex</span> search pattern will only return <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">true</span> if the compared string satisfies <span style="font-weight:bold;text-decoration:underline;">all</span> of the stated criteria. Let's do a quick breakdown on what, exactly, this expression is looking for:

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
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [OR Operator](#or-operator)
- [Flags](#flags)
- [Resources](#resources)

## Regex Components

<span style="font-weight:bold;">Regular expressions</span> are literals, meaning they must be wrapped in forward-slashes on both ends to be recognized as expressions in JavaScript. Alternatively, it is also possible to create a regex object by using a <span style="font-weight:bold;">RegExp Constructor</span>. For this tutorial, we will be using the literal notation, but feel free to review the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) on <span style="font-weight:bold;">RegExp</span> if you're curious about the alternate method.

Now let's dive in and take a closer look at the various componenets of a regex!

## Anchors

Both the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> and dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> symbols are considered to be <span style="font-weight:bold;">anchors</span>.

The caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor symbol is used to start the regex pattern, specifying that the string should begin with whatever characters directly follow it. This could be implemented in one of two ways:

- Checking the string for an exact match, such as <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^RegEx</span>, which would match either <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"RegEx"</span> or <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"RegEx Tutorial"</span>. Due to regex being <span style="font-weight:bold;">case-sensitive</span>, it would not match a string beginning with <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"regex"</span>.
- Checking the string against a range of possible matches. This is accomplished using <span style="font-weight:bold;">bracketed expressions</span>, which we'll go over in its own section.

The dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor symbol is used to end the regex pattern, specifying that the string should end with whatever characters directly precede it. The dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor accepts either an exact string to match or a range of possible matches, same as the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor.

Let's refer back to the first and last parts of our URL matching example:

```JS
const regex = /^(https?:\/\/)? ... \/?$/;
```

FIrst, our regex checks if the string begins with whatever is within the parentheses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">( )</span> (which separate it from the rest of the expression) directly following the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor. In our case it checks for an http or https protocol followed by a colon and two forward-slashes, either will match due to the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> <span style="font-weight:bold;">quantifier</span> symbol after the "s" in https. This group is also optional due the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier outside the parentheses.

In the last part of our expression, we are checking if the string ends in a trailing forward-slash, as those characters directly precede the dollar-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">$</span> anchor. It is again optional due to the presence of the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier.

Remember, in literal notation, if we want to check for a forward-slash it must be <span style="font-weight:bold;">escaped</span> with a back-slash each time. We'll talk about the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> and other quantifiers in the next section.

## Quantifiers

You can think of <span style="font-weight:bold;">quantifiers</span> as rules that are placed on the individual groups in your expression, to set the limits on what will be considered a matching string. They are commonly used to set a group's character limit, or whether a group isn't required for a string to match. Let's take another look at our URL regex example:

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
```

In our expression, the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">+</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\*</span>, and <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ }</span> symbols are all <span style="font-weight:bold;">quantifiers</span>. Quantifiers are inherently <span style="font-weight:bold;">greedy</span>, which means they will attempt to match their specified pattern as many times as possible. Here's a break-down of each quantifier and its purpose:

- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> - Matches the pattern zero or one time, a way to mark a group as optional.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">+</span> - Matches the pattern one or more times, a way to allow for infinite matches.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\*</span> - Matches the pattern zero or more times, a way to allow for infinite or no matches.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ }</span> - Curly braces allow for three different ways to specify how a string should match:
  - <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ n }</span> - Matches the pattern exactly <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"n"</span> number of times.
  - <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ n, }</span> - Matches the pattern at least <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"n"</span> number of times.
  - <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ n, x }</span> - Matches the pattern from a minimum of <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"n"</span> number of times to a maximum of <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"x"</span> number of times.

## Greedy and Lazy Match

All quantifiers can be either <span style="font-weight:bold;">greedy</span> or <span style="font-weight:bold;">lazy</span>, but are <span style="font-weight:bold;">greedy</span> by default. In order to make any of the above quantifiers <span style="font-weight:bold;">lazy</span>, simply add the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> symbol after it, this will cause that quantifier to match as few occurrences as possible instead of as many as possible.

Let's look at each part of our regex example again to see how it uses <span style="font-weight:bold;">quantifiers</span> as well as <span style="font-weight:bold;">greedy and lazy match</span>:

- The `(https?:\/\/)?` group uses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifiers to match a string beginning with http, https, or one that doesn't contain a protocol at all.
- The `([\da-z\.-]+)` group uses a <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">+</span> quantifier to match a string that contains at least one domain name.
- The `\.([a-z\.]{2,6})` group uses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">{ }</span> quantifiers to match a string that contains a top-level domain between 2 and 6 characters long.
- The `([\/\w \.-]*)` group uses a <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\*</span> quantifier to match a string that contains any number of paths, even zero.
- The final `\/?$` group uses a <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier to match a string that may or may not contain a trailing forward-slash.

## Bracket Expressions

In a regular expression, anything inside a pair of square brackets <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ ]</span> is considered to be a <span style="font-weight:bold;">bracket expression</span>. Bracket expressions represent a range of characters in the string we wish to match. For this reason, bracket expressions are also sometimes known as <span style="font-weight:bold;">positive character groups</span> due to them defining anything what we want to <span style="font-weight:bold;">include</span>.

As an example, we can write a bracket expression as <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ abc ]</span>, which will match a string that contains a lowercase <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"a"</span> or <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"b"</span> or <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"c"</span> regardless of the number of occurrences. In the case of this example, all of the following strings would match: <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"aaa"</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"cba"</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"bottle"</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"bobcat"</span> and <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"albacore"</span>.

Most often, you'll see a hyphen <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">-</span> symbol used between either numbers or letters, this represents a range between the stated characters that will match anything it contains. For example, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ a-z ]</span> is the exact same as writing the entire alphabet between square brackets.

Let's look at our URL regex example again to see how <span style="font-weight:bold;">bracket expressions</span> are being used:

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
```

- In the `([\da-z\.-]+)` group, a string will match as long as it contains any digit 0-9 (specified by the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\d</span> <span style="font-weight:bold;">character class</span>), and/or any lowercase letter from a-z, and/or a period or hyphen.
- In the `([\/\w \.-]*)` group, a string will match as long as it contains any lowercase or uppercase letter a-z, a number 0-9, or an underscore <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\_</span> (specified by the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\w</span> <span style="font-weight:bold;">character class</span>), and/or a period or hyphen.

If desired, you can turn any bracket expression into a <span style="font-weight:bold;">negative character group</span> by adding the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> symbol directly after the open-bracket. For example, the expression <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ ^0-9A-Z ]</span> would match any string that <span style="font-weight:bold;text-decoration:underline;">does not</span> contain numbers or uppercase letters.

If you were wondering about those character classes from before, great news! Next up, we take a closer look at what classes can do.

## Character Classes

In regex, a <span style="font-weight:bold;">character class</span> is a convenient shorthand for defining a set of characters to compare against a string. If that functionality sounds familiar, it may be because <span style="font-weight:bold;">bracket expressions</span> are also a form of character class, in addition to the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\w</span> and <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\d</span> classes we saw within each expression. Here are some examples of common classes you might encounter while using regex:

- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">.</span> - The "period" class, it matches any character except the newline character <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\n</span>.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\d</span> - The "digit" class, it matches any Arabic numeral digit from 0-9.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\w</span> - The "word" class, it matches any letter a-z regardless of case, any numeral digit 0-9, and underscores <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\_</span>.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\s</span> - The "space" class, it matches a single whitespace character, including tabs and line breaks.

In order to change the digit, word, or space classes to match their inverse value, you can capitalize the letter after the backslash. For example, the <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\D</span> class matches any character that is <span style="font-weight:bold;text-decoration:underline;">not</span> a digit from 0-9.

Throughout this tutorial, you may have noticed that we have been referring to sections of the regex within parentheses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">( )</span> as "groups". We'll get into why in the next section.

## Grouping and Capturing

In regex, <span style="font-weight:bold;">grouping constructs</span> are used to break out sections of the expression (known as <span style="font-weight:bold;">subexpressions</span> or <span style="font-weight:bold;">groups</span>) so that individual parts of a string can be compared to specific rules. The main way to group a section in a regex is by using a set of parentheses <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">( )</span> surrounding the part of the expression you wish to isolate.

Let's take one last look at our entire URL regex example using everything we've learned so far, to see how grouping constructs have been used to separate the different sections:

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
```

- First, we see that the `^(https?:\/\/)?` subexpression is grouped so that we target only the protocol in the URL, ensuring everything within it either occurs first in the string, due to the caret <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">^</span> anchor symbol, or does not occur at all, due to the question mark <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?</span> quantifier symbol.
- Next, we see that the `([\da-z\.-]+)` subexpression is grouped so that we target only the domain name in the URL, ensuring that there is at least one occurrence of a valid domain name, due to the plus-sign <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">+</span> quantifier symbol.
- Next, we see that the `([a-z\.]{2,6})` subexpression is grouped so that we only target the top-level domain in the URL, ensuring that there is only one occurrence of a valid top-level domain (such as <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">.com</span> or <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">.org</span>), which is between 2-6 characters long.
- Lastly, we see that the `([\/\w \.-]*)*` subexpression is grouped so that we only target the paths in the URL, ensuring that there can be any number of valid paths, due to the star <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">\*</span> quantifier symbol.

But why should you use grouping constructs, and why are some parts of our regex outside the groups? A few reasons for that are:

- Quantifiers attached to a subexpression apply their rules to the entire group.
- Subexpressions are strict, they will look for a string that exactly matches their contents.
- Grouping constructs improve regex readability, and provide more control over its functionality towards a specific section of a string.

Grouping constructs also have two primary categories, <span style="font-weight:bold;">capturing</span> and <span style="font-weight:bold;">non-capturing</span>. This tutorial won't be going into detail about how the two categories differ, but the brief explanation is that <span style="font-weight:bold;">capturing</span> groups will capture the matched character sequences for possible re-use, while <span style="font-weight:bold;">non-capturing</span> groups will not. In order to make a grouping construct non-capturing, simply add the characters <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">?:</span> at the beginning of an expression inside the parentheses.

With grouping constructs covered, we have now fully explained each part of our regex example to check if a string is a valid URL! Take a moment to look over the full code block below and try to parse-out how each step is validating the provided URL string.

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/;
const string = "https://github.com/Aoliva96/regex-tutorial";

const isMatch = regex.test(string);
console.log(isMatch); // Expected output: true
```

Hopefully, the functionality is a lot clearer now that you know how the whole expression is structured!

There is of course, much more that can be done with regex. For the rest of this tutorial, we will briefly touch on two other common regex categories you might encounter.

## OR Operator

You may remember that bracket expressions do not require the matched string to meet all the stated requirements in the pattern. This means that the expression <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ \da-z_- ]</span> searches for alphanumeric characters <span style="font-weight:bold;text-decoration:underline;">or</span> underscores <span style="font-weight:bold;text-decoration:underline;">or</span> hyphens. You may end up wanting to use that same logic outside of a bracket expressions, within a grouping construct, or between two different subexpressions.

Utilizing the <span style="font-weight:bold;">OR operator</span> <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">|</span> also known as a "pipe", the expression <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">[ abc ]</span> could be written as <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">( a | b | c )</span>. Lets look at the following expression as an example:

```JS
(abc):(xyz)
```

This would look for an exact match for <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">abc</span>, then a colon <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">:</span>, then an exact match for <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">xyz</span>. We can use the OR operator to convert it to the following expression:

```JS
(a|b|c):(x|y|z)
```

Now, the strings <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"abc:xyz"</span>, <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"acb:xyz"</span> and <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"a:z"</span> would all match, but <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">"xyz:abc"</span> would not.

## Flags

At the very beginning of this tutorial, we started by explaining that a regular expression is considered to be a <span style="font-weight:bold;">literal</span>. As a literal, a regex must be escaped using a leading and trailing forward-slash to be correctly recognized by JavaScript. There is one exception to this rule, however, in the form of <span style="font-weight:bold;">flag components</span>. Flags are placed at the end of a regex, <span style="font-weight:bold;text-decoration:underline;">outside</span> of the wrapping forward-slashes. Flags define extra functionality or limitations of your regex, of which there are six optional flags that can be used in any combination. The following three flags are the ones you're most likely to see while working with regex:

- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">g</span> - Global search, this instructs the regex to test against all possible matches in a string.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">i</span> - Case-insensitive search, this instructs the regex to ignore letter casing when attempting to match a string.
- <span style="color:lightblue;background:#2b2b2b;padding:0 5px 2px 5px;border-radius:3px;">m</span> - Multi-line search, this instructs the regex to treat multi-line strings as multiple separate lines.

If we wanted to edit our URL regex example to utilize a case-insensitive search, it may look something like this:

```JS
const regex = /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/i;
```

Not that different! But our regex will now accept URLs that contain capital letters wherever letters are expected.

### Advanced Regex Categories

There are a few notable regex categories that go beyond the scope of this tutorial. If you're interested in learning more, do explore the following:

- Boundaries
- Back-references
- Look-ahead and Look-behind (lookaround assertions)

## Resources

Explore the following resources to expand your knowledge of regex:

[MDN Web Docs | Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

[W3Schools | The RegExp Object](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)

## About the Author

Hi there! Thanks for taking a look at my tutorial. My name is Aster Oliva and I am, at the time of writing this, a student enrolled in a full-stack developer bootcamp through UC Berkeley. I am currently working towards a career in software/web development specializing in HTML/CSS and JavaScript, learning React/JSX, MongoDB and much more! To see some of my other work, you can find me on GitHub at [github.com/Aoliva96](https://github.com/Aoliva96).

I hope you found my tutorial to be useful, and feel free to submit a comment if you have any improvements to suggest!
