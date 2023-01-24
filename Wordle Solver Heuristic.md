---
tags: AI, search, heuristic, Wordle
aliases: 
---
Date:: 2022-09-10 Saturday
Links: 
- - -
# Wordle Solver Heuristic

## 1. Play Heuristically With Character Frequency

Intuitively, what words might work well for a first guess in the game?

A natural thought is to figure out in early guesses which **vowels** ('a', 'e', 'i', 'o', 'u') exist in the target, since a word must contain at least one vowel.

More generally, one might consider words composed of **common characters** (including the vowels) over rare characters, since determining the existence of common characters provide more information for selecting the next guess.

That leads to the first heuristic rule:

**Heuristic Rule**: Give favour to words composed of common characters rather than rare characters (**Exploitation**)

**Scoring Function**: Let ${f_T}(c)$ be the frequency count of a character $c$ among words from a target set $T$. Then the score of a guess word with unique characters $c_1, c_2, ..., c_k$ could be taken as the sum $\sum_{j=0}^{k} {f_T}(c_j)$. A guess word in $T$ with the highest score would be the next guess.

After the first guess, the same heuristic rule can be applied in subsequent guesses by scoring with updated character frequencies $f_{T_i}$, where $T_i$ is the set of remaining candidates at the $i$-th guess.

---

On the other hand, sometimes, one might wish to guess words not listed in the remaining candidates (**Exploration**). For example, consider words that end with "-ound". There are over eight of them (e.g. "bound", "pound", "mound", "sound", etc).

If the remaining candidates only consist of these "-ound" words, a better guess word could be e.g. "plumb" since it has more significant letters ('p', 'b', and 'm') of those "-ound" words.

That leads to an adjusted heuristic rule:

**Adjusted Heuristic Rule**: Consider *all possible guess words*. Give favour to words composed of "significant" characters by excluding characters already shared by all remaining candidates → Calculate the adjusted frequency using the *remaining candidates*, BUT we choose the word from  the list of *all possible words!!!*

**Scoring Function**: On top of the previous scoring function, let $X_{i}$ be the set of characters that appear in every word from $T_i$. Then the score of a guess word with unique characters $c_1, c_2, ..., c_k$ could be adjusted as $\sum_{j=0, c_j \notin X_{i}}^{k} f_{T_i}(c_j)$. A word with the highest score among all possible guess words would be the next guess.

**Result**: With the adjusted heuristic rule, the solver can guess [**all 2315 words**](https://raw.githubusercontent.com/kiking0501/Wordle-Solver/master/data/small-ordered.txt)  within **six guesses** using first guesses such as "raise", "later", or "snare". And the average number of guesses is **~3.8**. Works like a charm to tackle the Wordle daily challenges

## 2. Maximise Information Entropy

**Intuition**: From the discussed heuristic rule, one might observe that a good guess word should have diversified response outcomes, where each response outcome is the feedback with respect to a potential target word.

As an example, take three "-ound" words, "bound", "pound", and "mound" as the target candidates. If we choose the guess word as "lound", all possible responses would be the same outcome: $$\text{Absent-Correct-Correct-Correct-Correct}$$ On the other hand, choosing a guess word "plumb" would result in three different response outcomes: $$\text{Absent-Absent-Correct-Absent-Present}$$ $$\text{Correct-Absent-Correct-Absent-Absent}$$ $$\text{Absent-Absent-Correct-Present-Absent}$$ Clearly, the "plumb" is a good guess word since its *diversified response outcomes* help us better determine the actual target word.

How might these response outcomes be quantified for our guess word scoring?

**Information Entropy** Let $R: \{x_1, x_2, ..., x_u\}$ be the set of all distinct response outcomes, where $u = 3^5 = 243$ (since a response outcome is composed of one of {$\text{Correct, Present, Absent}$} for five letters).

Define $X_w$ to be a discrete [[Random Variable]] with respect to a guess word $w$ that has possible outcome $x_1, x_2, ..., x_r \in R$, and each outcome $x_j$ occurs with probability $p_w(x_j)$. In Information Theory, we could measure the level of "information" of this random variable $X_w$ using the [**Shannon Entropy**](https://en.wikipedia.org/wiki/Entropy_(information_theory)): $$H(X_w) = - \sum_{j=1}^{r} \ p_w(x_j) \ \log_2\ p_w(x_j) $$where a higher entropy value indicates that $p_w(x_j)$ *spreads out more evenly* rather than being skewed.

**Scoring Function** From the above formulation, we could see that the entropy of $X_w$ is, in fact, a good measurement of *how diverse the response outcomes* $x_1, x_2, ..., x_r$ are with respect to a guess word $w$. The score of $w$ could then simply be the entropy of its associated random variable $X_w$. To compute $p_w(x_j)$, one might assume that the target word is selected uniformly and randomly. Then $$p_w(x_j) = \frac{\text{Number of target candidates that word }w\text{ results in outcome }x_j}{\text{Total number of target candidates}} $$The numerator is the reduced search space after the guess and the denominator is the previous search space it is reduced from.

The word with the maximum associated entropy among all possible guess words would be selected as the next guess.

**Result**: While the entropy computation takes much time, the solver can guess [**all 2315 words**](https://raw.githubusercontent.com/kiking0501/Wordle-Solver/master/data/small-ordered.txt)  within **five guesses** using first guesses such as "react". And the average number of guesses is **~3.6**. Solves the Wordle daily challenges with ease of mind.