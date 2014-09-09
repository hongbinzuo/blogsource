title: Manacher
date: 2014-08-13 19:14:43
tags:
 - algorithms
---

最近在研究算法，今天重点学习了一下Manacher算法（俗称“马拉车”算法，也即[最长回文子串问题](http://en.wikipedia.org/wiki/Longest_palindromic_substring)的最佳解法），不禁为算法发明者拍案叫绝。算法的精巧之处在于充分利用了原问题的关键信息：回文串。

前段时间参加了[July](http://weibo.com/julyweibo)组织的算法班，遗憾的是当时算法的基础并不好没听透，所以现在只好重听一下邹博的讲课录音，听完之后似乎明白又似乎不太明白，囧。把原C++程序改成成Java代码之后，Exception退出，囧++。智商已成事实，只好使用网络搜索大法，力求加深理解。在找了一些博客之后，略感失望，可能不是人家讲得不清楚，而是自己理解能力有限吧，不过为了参考方便，还是列举如下：
<!--  more -->

 - http://www.cnblogs.com/biyeymyhjob/archive/2012/10/04/2711527.html
 - http://www.felix021.com/blog/read.php?2040
 - http://blog.csdn.net/ggggiqnypgjg/article/details/6645824
 - http://zhuhongcheng.wordpress.com/2009/08/02/a-simple-linear-time-algorithm-for-finding-longest-palindrome-sub-string/
 - http://programmingpraxis.com/2010/10/15/find-the-longest-palindrome-in-a-string/

最后，经过一番比较之后，我还是觉着LeetCode上一篇文章写得不错，尤其是配图特别适合初学者理解。细读之后，感觉比较通透，将其C++代码转译成Java代码，也运行流畅。用几个字符串进行试验，结果正确，思路也逐渐清晰了。Leetcode上作者有两篇文章，第一篇讲的是最长回文子串的其他解法，包括暴力法、动态规划等，但都达不到O(N)的时间复杂度，在第二篇文章中作者重点讲解了唯一能达到O(N)的Manacher算法，算法本身很短，而其精要处也就那么两行。LeetCode的参考链接：
 - http://leetcode.com/2011/11/longest-palindromic-substring-part-ii.html

从Manacher算法学到的一个重要原则就是，如邹博所说，假设我们知道了前i项的解，那是不是对我们求解第i+1项有所帮助呢？:)

附Java代码实现：

```java

public class Manacher {
    public static void main(String[] args){
        Manacher.testGetLongestPalindrome("babcbabcbabcxa");
    }

    private static String preProcess(String s){
        int n = s.length();

        if (n == 0) return "^$";
        String result = "^";

        for (int i = 0; i < n; i++) {
            result += "#" + s.charAt(i);
        }

        result += "#$";
        return  result;
    }

    public static void testPreProcess(String testStr){
        String result = Manacher.preProcess(testStr);
        System.out.print(result);
    }

    public static void testGetLongestPalindrome(String testStr){
        String result = Manacher.getLongestPalindrome(testStr);
        System.out.print(result);
    }

    // the original implementation in C/C++
    // the source: http://leetcode.com/2011/11/longest-palindromic-substring-part-ii.html
    public static String getLongestPalindrome(String s){
        char[] T = preProcess(s).toCharArray();

        int n = T.length;
        int[] P = new int[n];

        int C = 0, R = 0;

        for (int i = 1; i < n-1; i++) {
            int i_mirror = 2*C - i; // equals to i' = C - (i-C)

            if ( i < R ) {
                P[i] = Math.min(R-i, P[i_mirror]);
            } else{
                P[i] = 0;
            }

            // Attempt to expand palindrome centered at i
            while( T[i+1+P[i]] == T[i-1-P[i]] )
                P[i]++;

            // if palindrome centered at i expand past R
            // adjust center based on expanded palindrome
            if ( i + P[i] > R) {
                C = i;
                R = i + P[i];
            }
        }

        int maxLen = 0;
        int centerIndex = 0;
        for (int i = 1; i < n-1 ; i++) {
            if (P[i] >  maxLen) {
                maxLen = P[i];
                centerIndex = i;
            }
        }

        int beginIndex = (centerIndex-1-maxLen)/2;

        return s.substring(beginIndex, beginIndex+maxLen);

    }
}

```
