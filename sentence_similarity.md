## Description 
Given two sentences <code>words1, words2</code> (each represented as an array of strings), and a list of similar word pairs <code>pairs</code>, determine if two sentences are similar.

For example, "great acting skills" and "fine drama talent" are similar, if the similar word pairs are <code>pairs = [[&quot;great&quot;, &quot;fine&quot;], [&quot;acting&quot;,&quot;drama&quot;], [&quot;skills&quot;,&quot;talent&quot;]]</code>.

Note that the similarity relation is not transitive. For example, if "great" and "fine" are similar, and "fine" and "good" are similar, "great" and "good" are not necessarily similar.

However, similarity is symmetric. For example, "great" and "fine" being similar is the same as "fine" and "great" being similar.

Also, a word is always similar with itself. For example, the sentences <code>words1 = [&quot;great&quot;], words2 = [&quot;great&quot;], pairs = []</code> are similar, even though there are no specified similar word pairs.

Finally, sentences can only be similar if they have the same number of words. So a sentence like <code>words1 = [&quot;great&quot;]</code> can never be similar to <code>words2 = [&quot;doubleplus&quot;,&quot;good&quot;]</code>.

## Solution ideas

## Solutions
### Solution 1 (two cycles)
```python
def sentence_similarity(words1, words2, pairs):
  if len(words1)!=len(words2):
    return False
  for word1, word2 in zip(words1, words2):
    if word1 == word2:
      continue
    flag=0
    for pair in pairs:
      if (word1 in pair) and (word2 in pair):
        flag=1
    if flag == 0:
      return False
  return True
```
### Solution 2 (set)
```python
def sentence_similarity(words1, words2, pairs):
  if len(words1)!=len(words2):
    return False
  set_similar_pairs = set((pair[0], pair[1]) for pair in pairs)
  res = all((word1==word2) or ((word1, word2) in set_similar_pairs) or ((word2, word1) in set_similar_pairs) for word1, word2 in zip(words1, words2))
  return res
```
