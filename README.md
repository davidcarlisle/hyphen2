# hyphen2

## Experiments in hyphenating compound words in luatex

LuaTeX allows a callback function to modify the hyphenation pass and
also allows each discretionary node to record the assoicated penalty
for breaking at this point.

This code attempts to address the issue of hyphenating words that are
formed as a compound with no hyphen by first using a language that
only distinguishes breaks between compounds, and then hyphenating each
compound separately.

So `\xshowhyphens{wellbeing babysitter dishwater}`

Produces terminal output

 well-[1]be-[100]ing baby-[1]sit-[100]ter dish-[1]wa-[100]ter  


Showing that a penalty of 1 is applied to breaks well-being,
baby-sitter, dish-water, and the higher penalty 100 applied to breaks
wellbe-ing. babysit-ter and dishwa-ter.

Possible issues and variants

* Currently the word parts are hyphenated as individual words so
  subject to the usual \lefthyphenmin etc, it may be better to
  hyphenate the complete compound in the second pass and then merge the
  two sets of breakpoints (this is more complicated but doable.

* Currently only two hypenpenalty values are used, with a low penalty
  at compound word breaks and a high penalty for others. This means
  that words that are _not_ compounds only get the high penalty.
  You could set the high penalty 50 50 which would retain the original
  behaviour but it usually takes a higher value to really discourage
  these breaks in compounds. It might be better to have three values
  and on;y use the high/low settings in words that have a break given
  by the compound word match.

* Ideally you would have language patters set up do matvh compound
  words, here I just use a language with no \patterns just a list of
  compound words given as \hyphenation exceptions.
  


