---
layout: post
title: House Robber
description: "人总是在选择中迷惘"
modified: 2015-03-15
tags: [leetcode]
image:
  feature: abstract-2.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

##水水的动归
很容易想到DP 
然后 
**f[i] = max(f[i-1],f[i-2] + num[i]);** 


{% highlight c++ %}
class Solution {
public:
    int rob(vector<int> &num) {
        //f[i] = max(f[i-1],f[i-2]+num[i])
        if(num.size() <= 1) return num.empty() ? 0 : num[0];
        vector<int> f = {num[0],max(num[0],num[1])};
        for(int i = 2 ; i < num.size() ; i++)
        {
            f.push_back(max(f[i-1],f[i-2]+num[i]));
        }
        return f.back();
    }
};
{% endhighlight %}
