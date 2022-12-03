### 2468.Split-Message-Based-on-Limit

此题有很大的迷惑性，二分法试探切割的份数的做法是错误的。并不是份数越多，就越容易满足要求。比如说，分割成99份，一定比分割成98份可以装下更多的字符，因为多了一个字段。但是分割成100份，不见得能比分割成99份装下更多的字符。这是因为前者每个字段的overhead是`<xx/100>`，而后者每个字段的overhead是`<xx/99>`，前者每个字段反而要少装1个字符，即使多一个字段，也不见得能弥补得过来（特别是当limit比较小的话）。

由此可见，本题的关键其实在于确定“份数”里多有少个数字。如果份数是固定的k位数，那么自然是份数越多，就越容易满足要求。所以我们先估算需要多少位数的份数。如果是一位数，那么我们就查看分成9份最多能装多少字符；如果是两位数，那么我们就查看分成99份最多能装多少字符；如果是三位数，那么我们就查看分成999份最多能装多少字符... 当发现最多能装的字符数大于message的长度，那么我们就知道份数的digit number。

如果份数的digit number确定下来之后，比如说是三位数，我们就可以暴力构造答案了。虽然我们暂时不知道具体的份数，但可以用xxx代替。即`*****<1/xxx>`,`*****<2/xxx>`,其中`*****`表示可以填充的字符。不停地添加字段，直至恰好把message都填充完，此时我们就可以确定“份数”了。再将具体的“份数”替换原有的`xxx`就是答案。