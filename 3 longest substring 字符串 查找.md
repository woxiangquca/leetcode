---


---

<blockquote>
<p>Given a string, find the length of the longest substring without<br>
repeating characters.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/longest-substring-without-repeating-characters">题目</a></p>
<h2 id="暴力搜索法">暴力搜索法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">lengthOfLongestSubstring</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">:</span> <span class="token builtin">str</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        start <span class="token operator">=</span> <span class="token number">0</span>
        end <span class="token operator">=</span> <span class="token number">0</span>
        max_len <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">while</span> end <span class="token operator">&lt;</span> <span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#在遍历完之前</span>
	        <span class="token comment">#检查是否有跟end上元素重复的</span>
            last_repeat <span class="token operator">=</span> self<span class="token punctuation">.</span>check_repeat<span class="token punctuation">(</span>start<span class="token punctuation">,</span>end<span class="token punctuation">,</span>s<span class="token punctuation">)</span>
            <span class="token keyword">if</span> start <span class="token operator">==</span> end <span class="token operator">or</span> last_repeat <span class="token operator">==</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">:</span>
                end<span class="token operator">+=</span><span class="token number">1</span>
                <span class="token keyword">continue</span>
            max_len <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>end<span class="token operator">-</span>start<span class="token punctuation">,</span>max_len<span class="token punctuation">)</span><span class="token comment">#出现重复时 更新max_len</span>
            start <span class="token operator">=</span> last_repeat<span class="token operator">+</span><span class="token number">1</span><span class="token comment">#更新start</span>
        <span class="token keyword">return</span> <span class="token builtin">max</span><span class="token punctuation">(</span>max_len<span class="token punctuation">,</span>end<span class="token operator">-</span>start<span class="token punctuation">)</span><span class="token comment">#当遍历完后再更新一次 因为有可能最大字串在末尾</span>
    <span class="token keyword">def</span> <span class="token function">check_repeat</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span>start<span class="token punctuation">,</span>end<span class="token punctuation">,</span>s<span class="token punctuation">)</span><span class="token punctuation">:</span>
	    <span class="token comment">#有重复返回重复字符的索引</span>
        <span class="token keyword">for</span> x <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>end<span class="token number">-1</span><span class="token punctuation">,</span>start<span class="token number">-1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> s<span class="token punctuation">[</span>x<span class="token punctuation">]</span> <span class="token operator">==</span> s<span class="token punctuation">[</span>end<span class="token punctuation">]</span><span class="token punctuation">:</span>
                <span class="token keyword">return</span> x
        <span class="token comment">#无重复返回-1</span>
        <span class="token keyword">return</span> <span class="token operator">-</span><span class="token number">1</span>
</code></pre>
<p>start和end记录当前最长字符串的首尾 题中不需要记录串<br>
max_len记录长度<br>
每当start更新（说明出现了重复字符）或者字符串遍历结束时更新max_len<br>
<strong>思路是对的 但是速度奇慢无比 而且很容易出错</strong></p>
<h3 id="check_repeat方法真的很蠢-python里就用字典查找">check_repeat方法真的很蠢 python里就用字典查找</h3>
<h2 id="优化算法">优化算法</h2>
<p>大佬的</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">lengthOfLongestSubstring</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token triple-quoted-string string">"""
        :type s: str
        :rtype: int
        """</span>
        st <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
        i<span class="token punctuation">,</span> ans <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span>
        <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> s<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token keyword">in</span> st<span class="token punctuation">:</span>
                i <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>st<span class="token punctuation">[</span>s<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span> i<span class="token punctuation">)</span>
            ans <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>ans<span class="token punctuation">,</span> j <span class="token operator">-</span> i <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span>
            st<span class="token punctuation">[</span>s<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">]</span> <span class="token operator">=</span> j <span class="token operator">+</span> <span class="token number">1</span>
        <span class="token keyword">return</span> ans<span class="token punctuation">;</span>
</code></pre>
<p>90%以上<br>
或我自己在原来的基础上改的</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">lengthOfLongestSubstring</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">:</span> <span class="token builtin">str</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        start <span class="token operator">=</span> <span class="token number">0</span>
        end <span class="token operator">=</span> <span class="token number">0</span>
        max_len <span class="token operator">=</span> <span class="token number">0</span>
        hashmap <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
        <span class="token keyword">for</span> end <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> s<span class="token punctuation">[</span>end<span class="token punctuation">]</span> <span class="token keyword">in</span> hashmap<span class="token punctuation">:</span>
                start <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>start<span class="token punctuation">,</span>hashmap<span class="token punctuation">[</span>s<span class="token punctuation">[</span>end<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span>
            max_len <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>end<span class="token operator">-</span>start<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">,</span>max_len<span class="token punctuation">)</span>
            hashmap<span class="token punctuation">[</span>s<span class="token punctuation">[</span>end<span class="token punctuation">]</span><span class="token punctuation">]</span> <span class="token operator">=</span> end
        <span class="token keyword">return</span> max_len
</code></pre>
<p>85%以上<br>
我也不太清楚两种方法的区别<br>
跟我的方法思路一样 主要是用了<strong>字典</strong>来查找 很快</p>
<h2 id="滑动窗口法">滑动窗口法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">lengthOfLongestSubstring</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">:</span> <span class="token builtin">str</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> s<span class="token punctuation">:</span><span class="token keyword">return</span> <span class="token number">0</span>
        left <span class="token operator">=</span> <span class="token number">0</span>
        lookup <span class="token operator">=</span> <span class="token builtin">set</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
        n <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span>
        max_len <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span>
	        <span class="token comment">#当前遍历到s[i] 查找是否在lookup中 如果有的话就把首字符剔除 直到把重复的那个剔除为止</span>
            <span class="token keyword">while</span> s<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token keyword">in</span> lookup<span class="token punctuation">:</span>
                lookup<span class="token punctuation">.</span>remove<span class="token punctuation">(</span>s<span class="token punctuation">[</span>left<span class="token punctuation">]</span><span class="token punctuation">)</span>
                left <span class="token operator">+=</span> <span class="token number">1</span>
            lookup<span class="token punctuation">.</span>add<span class="token punctuation">(</span>s<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>lookup<span class="token punctuation">)</span> <span class="token operator">&gt;</span> max_len<span class="token punctuation">:</span>max_len <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>lookup<span class="token punctuation">)</span>
        <span class="token keyword">return</span> max_len
</code></pre>
<p>这种方法就是不用计算start和end的变化 也不需要专门记录长度 直接求set的长度就可以 不需要费脑子 就是维护一个字串 称为窗口 相当于一个队列 从左边出从右边进<br>
<strong>很快</strong> 有时比用字典还快</p>

