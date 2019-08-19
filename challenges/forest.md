# Forest

## Problems

- do we write our own parser and lexer or do we use generators

- SOLVED: write our own with:

[This tutorial on how to write an interpreter](https://ruslanspivak.com/lsbasi-part1/)  

### Compiler vs interpreter

**Compiler** translates source code in language X into machine language.

**Interpreter** processes and executes program without translating it into machine language first

**Other terms**

**Lexeme** is a sequence of characters that form a token  

**Parsing** is the process of recognising a phrase in a stream of tokens

---

# Forest todo

- [x] list of terms
- [x] documentation
- [x] learn more Python syntax
- [x] find out how to implement a command line-like executable playground on a web page


---

## First coding session

* test-driving using unittest (Python's own testing framework)
* run test with `python -m unittest echo_test.py` 

## MVP mob coding

* `isalpha()` method to the rescue!
* further reduction of MVP


## Grammar rules

1. empty statement grammar rule (BEGIN END)
2. put in a [spec like this one for LOLCODE](https://github.com/justinmeza/lolcode-spec/blob/master/v1.2/lolcode-spec-v1.2.md)

## HOW TO - adding more grammar rules to Forest

1. Add requisite tokens
2. Check grammar - add any necessary rules
3. Build the AST (abstract syntax tree) - create_ast_for_rule method
4. Evaluate tree - in Interpreter - add to the visit_tree method & new visit_ast method 
5. create new class for AST if it doesn't already exist
