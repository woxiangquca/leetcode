---


---

<blockquote>
<p>Given an unsorted integer array, find the smallest missing positive<br>
integer.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/first-missing-positive/">题目</a></p>
<h2 id="桶排序把原数组是为哈希表，哈希函数为fnumsi--numsi-1">桶排序||把原数组是为哈希表，哈希函数为f(nums[i]) = nums[i]-1</h2>
<blockquote>
<p><strong>索引为  <code>i</code>  的位置上应该存放的数字是  <code>i + 1</code></strong> 让每一个合法（大于0小于等于size）的数都存放在他该在的地方 这样的话第一个非法数据的索引+1就是缺失的</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">firstMissingPositive</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>

        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">while</span> <span class="token number">1</span> <span class="token operator">&lt;=</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">&lt;=</span> size <span class="token operator">and</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">!=</span> nums<span class="token punctuation">[</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">:</span><span class="token comment">#一直交换 把nums[i]放到nums[nums[i]-1]上直到nums[i]的值非法 也就是说 如果这里的数刚开始不非法但是交换后非法 则说明这个数组里一定缺少i+1 </span>
                nums<span class="token punctuation">[</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token punctuation">,</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token punctuation">,</span> nums<span class="token punctuation">[</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token comment">#每交换一次都有一个数到他该有的位置</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> i <span class="token operator">+</span> <span class="token number">1</span> <span class="token operator">!=</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span>
                <span class="token keyword">return</span> i <span class="token operator">+</span> <span class="token number">1</span>
        <span class="token keyword">return</span> size <span class="token operator">+</span> <span class="token number">1</span>  
</code></pre>
<p>时间复杂度为O(n)的原因是 每交换一次必有一个数在他应该在的位置 所以这样下来一共需要交换n次</p>

