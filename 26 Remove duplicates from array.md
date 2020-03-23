---


---

<blockquote>
<p>Given a sorted array nums, remove the duplicates in-place such that<br>
each element appear only once and return the new length.<br>
Do not allocate extra space for another array, you must do this by<br>
modifying the input array in-place with O(1) extra memory</p>
<p><strong>Examples:</strong><br>
Given nums = [0,0,1,1,1,2,2,3,3,4],<br>
Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.<br>
It doesn’t matter what values are set beyond the returned length.</p>
<p><strong>Clarification:</strong><br>
Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.</p>
<p>Internally you can think of this:<br>
// nums is passed in by reference. (i.e., without making a copy)<br>
int len = removeDuplicates(nums);<br>
// any modification to nums in your function would be known by the caller.<br>
// using the length returned by your function, it prints the first len elements.<br>
for (int i = 0; i &lt; len; i++) {<br>
print(nums[i]);<br>
}</p>
</blockquote>
<h2 id="我的解法">我的解法</h2>
<blockquote>
<p>不需要删除元素 只需要把后面的新出现的元素提前就可以<br>
cur记录当前数组中搜索到的最大的元素<br>
i是当前要被取代的跟前面元素重复的元素<br>
j指针搜索下一个比cur大（如果是降序的话就是小）的元素<br>
搜索到以后nums[i] = nums[j]</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">removeDuplicates</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> nums<span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token number">0</span>
        cur <span class="token operator">=</span> nums<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span>
        i <span class="token operator">=</span> <span class="token number">1</span>
        j <span class="token operator">=</span> i
        <span class="token keyword">while</span> i <span class="token operator">&lt;</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">while</span> nums<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">&lt;=</span> cur<span class="token punctuation">:</span>
                j<span class="token operator">+=</span><span class="token number">1</span>
                <span class="token keyword">if</span> j <span class="token operator">==</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token punctuation">:</span>
                    <span class="token keyword">return</span> i
            nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> nums<span class="token punctuation">[</span>j<span class="token punctuation">]</span>
            cur <span class="token operator">=</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span>
            i<span class="token operator">+=</span><span class="token number">1</span>
</code></pre>
<h2 id="优化一下">优化一下</h2>
<blockquote>
<p>仔细想一下 不需要cur值 因为每次nums[i]记录的就是最大值 只要当前j不等于i 那么就把i往后移 填上j处的值</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">removeDuplicates</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">int</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> nums<span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token number">0</span>
        cur <span class="token operator">=</span> nums<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span>
        i <span class="token operator">=</span> <span class="token number">0</span>
        j <span class="token operator">=</span> <span class="token number">1</span>
        <span class="token keyword">while</span> j <span class="token operator">&lt;</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">!=</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span>
                i<span class="token operator">+=</span><span class="token number">1</span>
                nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> nums<span class="token punctuation">[</span>j<span class="token punctuation">]</span>
            j<span class="token operator">+=</span><span class="token number">1</span>
        <span class="token keyword">return</span> i<span class="token operator">+</span><span class="token number">1</span>
</code></pre>

