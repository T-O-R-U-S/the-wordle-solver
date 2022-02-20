# The Wordle Solver

This website takes a list of all five-letter English words and gives you the most
accurate results.

### Algorithm

The algorithm used to solve the Wordle riddles is fairly simple.

First, it takes each letter and finds how many unique letters are in it.

`irate` (the computer-recommended starter) wins over something like 
`hedge` because it has less repeated letters; however, that is not the 
only factor that goes into deciding the best letter.

The second factor is letter frequency. Since `e` is more frequent than `q`, words
like `quire` are less favoured over `irate`. For this, I just used a pre-determined
table for the most frequent letters in the English language. I chose this over
word frequency because word frequency would require a much larger table.

The third factor is gray letters; any words that contains a letter that Wordle
has informed the player is not in the word get pruned.

The fourth factor is yellow letters; any words that do not contain the letter
get pruned, and any words that *do* contain the letter, but have the letter
in the position where the yellow letter was found also get pruned because
it's impossible for the letter to be in that position.

The most effective factor is green letters. Any words
that do not have the green letters provided by the user in perfect
position get pruned.