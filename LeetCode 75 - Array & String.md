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
