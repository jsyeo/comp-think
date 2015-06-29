# Introduction

## Why Racket?

In this workshop, racket will the language of instruction. You might
ask, why [Racket](http://racket-lang.org) and not Javascript, Python
or Ruby? The reason is simple, a language is here today and gone
tomorrow. What's popular and in used today may not be used
tomorrow. Therefore what matters is the teaching of concepts like
computational thinking instead of teaching the language as an
end. This is a computational thinking workshop and not a programming
workshop, after all.

So, why Racket? Well, that's because of two reasons, the first being
that Racket's syntax is extremely minimal. It consists of simply
brackets (or parentheses, depending on where you studied English) and
everything is a function. Students can quickly get up to speed with
the language very quickly and get things done. Secondly, the reason we
chose Racket is because of DrRacket. DrRacket is an IDE that is
extremely powerful and great for learning. Both the language and IDE
are designed for teaching programming. The IDE can display images
right in the IDE. Like this:

![images in DrRacket](http://i.imgur.com/jDE79ZB.png)

The IDE also excels at debugging. When an user mouse overs a variable,
arrows will appear to show where its defined and occurrences of the
variable are also highlighted.

## Getting Started with DrRacket

### Getting DrRacket

DrRacket is shipped with the Racket language. Simply point your
browser to http://download.racket-lang.org/ and install it.

### Getting Yourself Acquainted with DrRacket

After installing, start the DrRacket application. You should see the
screen split into two halves. The top half is your definitions panel,
the bottom half is the interactions panel.

Enter `#lang racket` into the definitions panel. This will tell
DrRacket to use the Racket language. Do you not need to know the
details behind this. You just need to know that Racket is a language
to build other languages. Using the `#lang` directive, you can define
which language to use.

### Diving into Racket

Try to guess what this line of Racket code compute:

```lisp
(+ 40 2)
```

Once you have made your guess, enter it into the interactions panel to
check if you have guessed correctly. To do so, click on the
interactions panel to focus on it. You should see a blinking cursor
after the `>` symbol. This means that the interaction panel is waiting
for the user to enter his input. Try entering `(+ 40 2)` now and press `Enter`.

You should see this.

```lisp
> (+ 40 2)
42
```

Now, try to guess what each of these lines compute:

```lisp
(+ 3 5 2)
(/ 10 (+ 3 2))
(sqrt 9)
```

If you've guessed 10, 2 and 3, you can pat yourself on the back
because you can read Racket code! Do enter these expressions into
Racket to confirm your guesses.
