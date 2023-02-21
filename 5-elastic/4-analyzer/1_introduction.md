# Analyzer Concepts

​	In Elastic, there are two types of searches: exact and non-exact.
​	When performing non-exact searches, we can use analyzers. They are responsible for analyzing how much our data is "compatible" (higher `_score`) with the search parameters.

​	Most used default analyzers:

- `whitespace`: separates the words by whitespaces.
- `simple`: removes numbers, spaces, punctuation and lower case.
- `standard`: removes spaces, punctuation and lower case.
- Language specific: removes accentuation, turns words into radicals, add synonims, etc. e.g.: brazilian, english.
