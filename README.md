# Linear-Time-Construction-of-Suffix-Arrays
Project for my bioinformatics class that handles suffix array construction in linear time using the skew algorithm.

Credit to https://mailund.dk/posts/skew-python-go/ for the fix for duplicate suffixes in the radix array and handling them recursively. Code is based off of both Mark Ormesher's explanation (https://gist.github.com/markormesher/59b990fba09972b4737e7ed66912e044) and Thomas Mailund's blog for skew method in linear time.|

Test in linear time for sequences created using UCR's Random DNA sequence generator by Morris F. Maduro: 1000: 0.020137310028076172, 2000: 0.03774142265319824, 5000: 0.07602787017822266, 10000: 0.141556978225708, 100000: 1.3828442096710205.

From https://louisabraham.github.io/articles/suffix-arrays, a chunk of the implementations for suffix arrays reach well over O(n) runtime. Some causes of this are how merge natively requires at least O(n log n) runtime. Prefix doubling takes O(n log n^2) time, and even if it is shorter, prefix matrices takes O(n log n) time. Computing the longest common prefix unfortunately doesn't produce a faster runtime. The only method that achieves a runtime of O(n) other than the skew algorithm is using suffix-tree-to-suffix-array conversion, but it has a high constant for runtime. 

Compared to all of these methods, while the skew method doesn't allow for simple computation, its runtime is phenominally small and allows for quick calculation of long sequences. This is due to the recursive skew call being a fraction of the string passed in, as well as computing 3-string suffixes of 'modulo 3 = 1' and 'modulo 3 = 2' for bucket sort separate from suffixes of 'modulo 3 = 0' and merging them afterwards, having a runtime of T(N) = T(2N/3) + O(n). This gives a reasonable time of computation for long genome sequences in the biomedical field.
