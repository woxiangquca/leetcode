---


---

<blockquote>
<p>Given a sorted array and a target value, return the index if the<br>
target is found. If not, return the index where it would be if it were<br>
inserted in order.</p>
<p>You may assume no duplicates in the array.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/search-insert-position/">题目</a></p>
<h2 id="二分法">二分法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">searchInsert</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">,</span> target<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        lo<span class="token punctuation">,</span>hi <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token operator">-</span><span class="token number">1</span>
        <span class="token keyword">while</span> lo <span class="token operator">&lt;=</span> hi<span class="token punctuation">:</span>
            mid <span class="token operator">=</span> lo<span class="token operator">+</span><span class="token punctuation">(</span>hi<span class="token operator">-</span>lo<span class="token punctuation">)</span><span class="token operator">//</span><span class="token number">2</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&gt;</span> target<span class="token punctuation">:</span>
                hi <span class="token operator">=</span> mid<span class="token number">-1</span>
            <span class="token keyword">elif</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&lt;</span> target<span class="token punctuation">:</span>
                lo <span class="token operator">=</span> mid<span class="token operator">+</span><span class="token number">1</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                <span class="token keyword">return</span> mid
        <span class="token keyword">return</span> lo
</code></pre>
<h2 id="模板法">模板法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">searchInsert</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">,</span> target<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        lo<span class="token punctuation">,</span>hi <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">while</span> lo <span class="token operator">&lt;</span> hi<span class="token punctuation">:</span>
            mid <span class="token operator">=</span> lo<span class="token operator">+</span><span class="token punctuation">(</span>hi<span class="token operator">-</span>lo<span class="token punctuation">)</span><span class="token operator">//</span><span class="token number">2</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&lt;</span> target<span class="token punctuation">:</span>
                lo <span class="token operator">=</span> mid<span class="token operator">+</span><span class="token number">1</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                hi <span class="token operator">=</span> mid
        <span class="token keyword">return</span> lo
</code></pre>

