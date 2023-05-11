# 1768. 交替合并字符串
给你两个字符串 word1 和 word2 。请你从 word1 开始，通过交替添加字母来合并字符串。如果一个字符串比另一个字符串长，就将多出来的字母追加到合并后字符串的末尾。返回合并后的字符串。

示例 1：
```
输入：word1 = "abc", word2 = "pqr"
输出："apbqcr"
解释：字符串合并情况如下所示：
word1：  a   b   c
word2：    p   q   r
合并后：  a p b q c r
```
🤔**answer**
遍历法
```
var mergeAlternately = function(word1, word2) {
    const maxLen = Math.max(word1.length, word2.length);
    let i = 0;
    const ans = [];
    while (i < maxLen) {
        if (i < word1.length) {
            ans.push(word1[i]);
        }
        if (i < word2.length) {
            ans.push(word2[i]);
        }
        ++i;
    }
    return ans.join('');
};
```
# 1071. 字符串的最大公因子
对于字符串 s 和 t，只有在 s = t + ... + t（t 自身连接 1 次或多次）时，我们才认定 “t 能除尽 s”。
给定两个字符串 str1 和 str2 。返回 最长字符串 x，要求满足 x 能除尽 str1 且 x 能除尽 str2 。

示例：
```
输入：str1 = "ABCABC", str2 = "ABC"
输出："ABC"
```
```
输入：str1 = "LEET", str2 = "CODE"
输出：""
```
🤔**answer**

方法1:
```
var gcdOfStrings = function(str1, str2) {
    let ans = '';
    for(i = 1; i <= str1.length; i++) {
        const str = str1.slice(0, i);
        //两个字符串被split后没字符了，并且最大公因子保留最大长度
        if(str1.split(str).every(item => item === '') && str2.split(str).every(item => item === '') && ans.length < str.length) {
            ans = str;
        }
    }
    return ans;
};
```
方法2:

看到标题里面有最大公因子这个词，于是先默写一下 gcd 算法
`const gcd = (a, b) => (0 === b ? a : gcd(b, a % b))`
总有一种好像顺手就能用上的感觉呢。
其实看起来两个字符串之间能有这种神奇的关系是挺不容易的，我们希望能够找到一个简单的办法识别是否有解。
如果它们有公因子 abc，那么 str1 就是 m 个 abc 的重复，str2 是 n 个 abc 的重复，连起来就是 m+n 个 abc，好像 m+n 个 abc 跟 n+m 个 abc 是一样的。
所以如果 str1 + str2 === str2 + str1 就意味着有解。
我们也很容易想到 str1 + str2 !== str2 + str1 也是无解的充要条件。
当确定有解的情况下，最优解是长度为 gcd(str1.length, str2.length) 的字符串。
这个理论最优长度是不是每次都能达到呢？是的。
因为如果能循环以它的约数为长度的字符串，自然也能够循环以它为长度的字符串，所以这个理论长度就是我们要找的最优解。
把刚刚写的那些拼起来就是解法了。

```
var gcdOfStrings = function(str1, str2) {
  if (str1 + str2 !== str2 + str1) return ''
  const gcd = (a, b) => (0 === b ? a : gcd(b, a % b))
  return str1.substring(0, gcd(str1.length, str2.length))
};
```
# 1431. 拥有最多糖果的孩子
给你一个数组 candies 和一个整数 extraCandies ，其中 candies[i] 代表第 i 个孩子拥有的糖果数目。
对每一个孩子，检查是否存在一种方案，将额外的 extraCandies 个糖果分配给孩子们之后，此孩子有最多的糖果。注意，允许有多个孩子同时拥有最多的糖果数目。

示例 1：
```
输入：candies = [2,3,5,1,3], extraCandies = 3
输出：[true,true,true,false,true] 
解释：
孩子 1 有 2 个糖果，如果他得到所有额外的糖果（3个），那么他总共有 5 个糖果，他将成为拥有最多糖果的孩子。
孩子 2 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
孩子 3 有 5 个糖果，他已经是拥有最多糖果的孩子。
孩子 4 有 1 个糖果，即使他得到所有额外的糖果，他也只有 4 个糖果，无法成为拥有糖果最多的孩子。
孩子 5 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
```
🤔**answer**
```
var kidsWithCandies = function(candies, extraCandies) {
    const max = Math.max.apply(null, candies);
    return candies.map(candiy => candiy + extraCandies >= max);
};
```
