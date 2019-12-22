---
title: How to create a DSL, part 1
category: Programming
---

* https://en.wikipedia.org/wiki/Parsing
* https://en.wikipedia.org/wiki/Compiler
* https://en.wikipedia.org/wiki/Context-free_grammar
* https://en.wikipedia.org/wiki/Regular_expression
* https://en.wikipedia.org/wiki/Regular_language
* https://en.wikipedia.org/wiki/Automata_theory
* https://en.wikipedia.org/wiki/Formal_grammar
* https://en.wikipedia.org/wiki/Metaprogramming
* https://medium.com/@chetcorcos/introduction-to-parsers-644d1b5d7f3d
* https://tomassetti.me/guide-parsing-algorithms-terminology/
* https://tomassetti.me/ebnf/
* https://tomassetti.me/parsing-in-javascript/
* https://tomassetti.me/antlr-mega-tutorial/
* https://stackoverflow.com/questions/9452584/building-a-parser-part-i
* https://www.antlr.org/
* https://martinfowler.com/books/dsl.html
* https://www.jetbrains.com/mps/concepts/domain-specific-languages/
* http://docs.groovy-lang.org/docs/latest/html/documentation/core-domain-specific-languages.html
* https://docs.microsoft.com/en-us/visualstudio/modeling/about-domain-specific-languages?view=vs-2019
* http://blogs.perl.org/users/jeffrey_kegler/2014/09/parsing-a-timeline.html
* https://github.com/jamiebuilds/the-super-tiny-compiler
* https://github.com/zaach/jison
* https://github.com/pegjs/pegjs

For some time now, I've been interested in creating a domain-specific language (DSL). My goal is not to make something useful &mdash; although that would be great &mdash; but to learn more about the parsing of programming languages. As a first step toward creating this language, I'm researching the (pun intended) domain of DSLs. This post documents some of my findings.

## Concepts
### Domain-specific language
* Useful for a partiular, specialized field.
* Not a general-purpose language.
* Examples: Gradle, HTML, LaTex
* Types: markup, modeling, programming, specification
* A DSL could be a visual language or a modeling language, rather than a textual language.
* A DSL might be compiled to code or to some other artifact, like a media file.
* A DSL can be a stand-alone compiled language, or it can be a library within a programming language.
* One goal of a DSL is to be expressive, to express the requirements of the domain.

### Backus-Naur Form (BNF)
### Context-free grammar (CFG)
* A type of formal grammar identified by Noam Chomsky.

### Parsing
### Lexers
### Regular language
* Another type of formal grammar identified by Noam Chomsky. Can be operated on by regex.

### Regular expressions
### Syntax

### Metaprogramming

### Turing complete
* A programming language is Turing complete if it can simulate a Turing machine. More generally, if a problem is computable, it's computable in a Turing-complete language. In common usage, general-purpose programming languages are Turing complete, and DSLs are not.

## Resources

Below are some of the sources I relied on in creating this post. Note that I've only included resources with identifiable authors (i.e. not wikis and docs):

* Chet Corcos, [Introduction to Parsers](https://medium.com/@chetcorcos/introduction-to-parsers-644d1b5d7f3d)
