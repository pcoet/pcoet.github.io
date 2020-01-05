---
title: Lexing and parsing
category: Programming
---

* https://en.wikipedia.org/wiki/Automata_theory
* https://en.wikipedia.org/wiki/Formal_grammar
* https://github.com/jamiebuilds/the-super-tiny-compiler

Lately I've been interested in interpreters and compilers and how they parse programming languages. In particular, I've been working on a TypeScript implementation of the project described in Thorsten Ball's [Writing an Interpreter in Go](https://interpreterbook.com/). At this point, I've partially completed a lexer and a parser. This post explains some of the things I've learned from working through the tutorial and doing my own research.

## Language applications

Following Terrence Parr, we can think of compilers and interpreters as language applications that transform input across the stages of a pipeline. The pipeline is typically composed of multiple components. Often the pipeline will include a lexer and a parser, and it could also include other components, such as a preprocessor or an assembler. The components depend on the input and the desired output.

A compiler transforms a high-level programming language (the source) into a target representation &mdash; typically a lower-level language or machine code. The high-level languages that compilers translate are formal languages. A formal language can be described in terms of an alphabet, a set of strings over the alphabet, and a grammar that defines the rules for combining the strings into valid sentences. High-level programming languages are typically context-free languages that can be described in terms of context-free grammars. Compilers and other language applications can parse context-free grammars efficiently.

A transpiler is a compiler that transforms a high-level source language into another high-level language. In recent years, transpilation has become a more visible part of front-end engineering, as developers adopt tools like [TypeScript](https://www.typescriptlang.org/) and [Babel](https://babeljs.io/) that let them use cutting-edge JavaScript features in their source code and then transform those features into backward-compatible syntax that's understood by older browsers and runtimes.

Interpreters are similar to compilers, in that they typically perform lexical analysis and parsing on a high-level programming language. But instead of transforming the high-level language into machine code or bytecode, the interpreter actually executes it.

## Lexer

* Performs lexical analysis or tokenization on an input string.
* The characters of the input string are used to generate a sequence of meaningful tokens.
* The lexer first scans the input for lexemes, which are character sequences that match a token pattern. Then the lexer evaluates, or assigns values to, the lexemes, thereby converting them into tokens. Thus, the lexer is a tokenizer.
* A token is a string with an assigned meaning.
* In the process of lexical analysis, the familar parts of a programming language (e.g. keywords, operators, identifiers) are tokenized, or converted into token names and token values. A token name might be `keyword`, and a token value might be `function` or `const`.
* A lexer can use various means to identify tokens, including regular expressions, dictionary definitions, and delimiters.
* During lexical analysis, the lexer may also remove (or eat) certain lexemes, such as white space characters.
* After the input is tokenized, it's ready to be parsed.
* There are various lexer generators available so that you don't have to code a lexer by hand. A lexer generator might let you define tokens using regex, and then create a lexer based on those tokens.

## Parser

* There are various models of parsing. The one used in Ball's Go interpreter example is top-down operator precedence parsing, aka Pratt parsing. This is, as Ball points out, an alternative to Backus-Naur-Form parsing of context-free grammars.
* Parsing is also called syntactic analysis.
* Parsing - analyzing a string of symbols that conforms to the rules of a formal grammar. Typical output is a parse tree or abstract syntax tree that serves as an intermediate representation and shows how the symbols are related. Tokens are represented as nodes of the abstract syntrax tree. These nodes can then have methods associated with them, to transform the tokens, or they can be visited by a visitor that performs the transformation.
* Compilers and interpreters rely on parsers.
* Parsers produce a syntax tree that represents relationships among tokens, and also check for valid syntax.
* Lexical analysis comes before parsing.
* You can create a parser programatically using a parser generator.
* Templating is something out do with the output of a parser - you format it.
* HTML and XML are markup languages that require parsing. Computer languages also do.
* You can use regular expressions as part of lexing, parsing, or both.
* The lexer generates the tokens that the parser operates on. The parser cares about the syntactic relationships among the tokens.
* Parser has to make sure that tokens comprise a valid expression. Often a valid expression is defined by a context-free grammar.
* Parsing cay be done top down (left to right) or bottom up.
* The parser's job is to recognize stuff, to 

## Domain-specific language
* Useful for a partiular, specialized field.
* Not a general-purpose language.
* Examples: Gradle, HTML, LaTex
* Types: markup, modeling, programming, specification
* A DSL could be a visual language or a modeling language, rather than a textual language.
* A DSL might be compiled to code or to some other artifact, like a media file.
* A DSL can be a stand-alone compiled language, or it can be a library within a programming language.
* One goal of a DSL is to be expressive, to express the requirements of the domain.

## Grammar
* A grammar lets you differentiate valid from invalid sequences in strings or streams. A sequence comprises symbols, which could be characters, bytes, etc.
* A grammar groups sequences of symbols into valid sentences. Sentences are composed of tokens. Tokens are the leaves of the tree.
* A regular expression defines a grammar.
* Context-free grammar (CFG) - A type of formal grammar identified by Noam Chomsky.

## Regular language
* Another type of formal grammar identified by Noam Chomsky. Can be operated on by regex. A regular language can be reduced to a single production rule for a grammar.
* A regular language can be defined by a regular expression. A regular language is a formal language.
* A regular language can be processed by a finite automata.

## Regular expressions
* A regex is a character sequence that defines a pattern in a string. You can use the pattern to search for matches in text, and for lexical analysis in a compiler or interpreter. The characters in a regex are either metacharacters or literal characters.

## Turing complete
* A programming language is Turing complete if it can simulate a Turing machine. More generally, if a problem is computable, it's computable in a Turing-complete language. In common usage, general-purpose programming languages are Turing complete, and DSLs are not.

## Templating
* Templates help with the generation of structured output.

## Resources

* Thorsten Ball, [Writing an Interpreter in Go](https://interpreterbook.com/)
* Chet Corcos, [Introduction to Parsers](https://medium.com/@chetcorcos/introduction-to-parsers-644d1b5d7f3d)
* Software Construction on MIT OpenCourseWare, [Reading 17: Regular Expressions & Grammars](https://ocw.mit.edu/ans7870/6/6.005/s16/classes/17-regex-grammars/)
* John E. Hopcroft et al. [Introduction to Automata Theory, Languages, and Computation](https://www.pearson.com/us/higher-education/program/Hopcroft-Introduction-to-Automata-Theory-Languages-and-Computation-3rd-Edition/PGM64331.html)
* Terrence Parr, [Language Implementation Patterns](https://pragprog.com/book/tpdsl/language-implementation-patterns)