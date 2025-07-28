# Macroexpand

1. How can one expand a macro?
2. Is the result printed to standard output? Or returned as an s-expression?
3. Is the expander available inside programs? From the REPL?

Points (2) and (3) are verified with the following code:

```
(define-syntax f
  (syntax-rules () 
    ((f) (display "f"))))

(define-macro (f) '(display "f"))

(define f-expanded (macroexpand '(f)))

f-expanded                      ==> is this the expanded s-exp?

(let ((x (macroexpand '(f))))
  (display 'a)
  (display x)
  (display 'b))                 ==> a(display f)b or a#voidb ?
```

| Implementation | Method | program? | REPL? | sexp? | Remark |
|---|---|---|
| Bigloo   | `expand`       | Y | Y | sexp                    | |
| Biwa     | `macroexpand`  | Y | Y | sexp                    | Biwa only supports low-level macros |
| Chibi    | `macroexpand`  | Y | Y | sexp                    | needed: `(import (chibi ast))` |
| Chicken  | `expand`       | Y | Y | sexp, renamed symbols   | |
| Chez     | `expand`       | Y | Y | sexp, renamed symbols   | |
| Cyclone  | ?              |   |   |                         | |
| Gambit   | `pp`           | N | Y |                         | not exactly a macro-expander? |
| Gauche   | `macroexpand`  | Y | Y | sexp                    | has also `macroexpand-1` and `macroexpand-all` |
| Guile    | `macroexpand`  | Y | Y | specific tree structure | |
| Kawa     | `expand`       | Y | Y | sexp                    | needed: `(require 'syntax-utils)` |
| LIPS     | `macroexpand`  | Y | Y | sexp, quoted, renamed symbols| |
| Loko     | `expand`       | Y | Y | `(display '"f")`        | |
| MIT      | ?              |   |   |                         | |
| Racket   | `expand`       | Y | Y | specific tree structure | |
| Sagittarius | ?           |   |   |                         | |
| Scheme 9 | `macro-expand` | Y | Y | sexp                    | |
| STklos   | `macro-expand` | Y | Y | sexp                    | has also `macro-expand*`|
| Unsyntax | ?              |   |   |                         | |
| Ypsilon  | `macro-expand` | Y | Y | sexp                    | |
