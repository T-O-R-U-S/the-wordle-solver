# The Wordle Solver

This website takes a list of all five-letter English words and gives you the most
accurate results.

### Algorithm

The algorithm used to solve the Wordle riddles is fairly simple.

First, it takes each letter and finds how many unique letters are in it.

`irate` wins over something like `hedge` because it has less repeated letters;
however, that is not the only factor that goes into deciding the best letter.

The second factor is letter frequency. Since `e` is more frequent than `q`, words
like `quire` are less favoured over `irate`.