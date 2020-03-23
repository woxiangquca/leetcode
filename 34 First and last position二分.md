---


---

<blockquote>
<p>Given an array of integers nums sorted in ascending order, find the<br>
starting and ending position of a given target value.</p>
<p>Your algorithm’s runtime complexity must be in the order of O(log n).</p>
<p>If the target is not found in the array, return [-1, -1].</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/">题目</a></p>
<h2 id="二分法（适用于在有重复元素中是用二分法查找的模板）">二分法（适用于在有重复元素中是用二分法查找的模板）</h2>
<blockquote>
<p>用两次二分法分别找出起始位置和结束位置<br>
要找到最左端的元素 就要在小于等于时缩小r=mid 使得区间向左紧缩 <strong>这也是这个方法为什么能找到左右边界的原因</strong><br>
要找到最右端的元素 就要在大于等于时增大l=mid+1（因为除法的原因 mid会更加靠近l 所以为了保证循环继续 必须这样 并且循环条件要为l&lt;r 否则加入r和l相等 则mid=l=r 如果进入r=mid 就会死循环）<br>
关于细节 详见<a href="https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/er-fen-cha-zhao-suan-fa-xi-jie-xiang-jie-by-labula/">这里</a></p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">searchRange</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">,</span> target<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> nums<span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>
        
        l<span class="token punctuation">,</span>r <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        start<span class="token punctuation">,</span>end <span class="token operator">=</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span>
        
        <span class="token keyword">while</span> l<span class="token operator">&lt;</span>r<span class="token punctuation">:</span>
            mid <span class="token operator">=</span> <span class="token punctuation">(</span>l<span class="token operator">+</span>r<span class="token punctuation">)</span><span class="token operator">//</span><span class="token number">2</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&lt;</span> target<span class="token punctuation">:</span>
                l <span class="token operator">=</span> mid<span class="token operator">+</span><span class="token number">1</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                r <span class="token operator">=</span> mid
        <span class="token keyword">if</span> l <span class="token operator">==</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>
        <span class="token keyword">if</span> nums<span class="token punctuation">[</span>l<span class="token punctuation">]</span> <span class="token operator">==</span> target<span class="token punctuation">:</span>
            start <span class="token operator">=</span> l
        <span class="token keyword">else</span><span class="token punctuation">:</span>   <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>
                    
        l<span class="token punctuation">,</span>r <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">while</span> l<span class="token operator">&lt;</span>r<span class="token punctuation">:</span>
            mid <span class="token operator">=</span> <span class="token punctuation">(</span>l<span class="token operator">+</span>r<span class="token punctuation">)</span><span class="token operator">//</span><span class="token number">2</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&gt;</span> target<span class="token punctuation">:</span>
                r <span class="token operator">=</span> mid
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                l <span class="token operator">=</span> mid<span class="token operator">+</span><span class="token number">1</span>
        end <span class="token operator">=</span> l<span class="token number">-1</span><span class="token comment">#收紧右侧边界时会使l=mid+1 所以跳出循环后nums[l]绝对不等于target（nums[mid]） 需要-1</span>
        <span class="token comment">#上面这段也可以像下面这样写 注意如果是r = mid-1的话需要用右中位数</span>
        <span class="token triple-quoted-string string">'''
        l,r = 0,len(nums)-1
        while l&lt;r:
            mid = l+(r-l+1)//2
            if nums[mid] &gt; target:
                r = mid-1
            else:
                l = mid
        end = r
        '''</span>
        <span class="token comment">#这里没有判断边界条件是因为在寻找左边界时如果没找到就直接结束程序了 能到这里说明一定找到了</span>
        
        <span class="token keyword">return</span> <span class="token punctuation">[</span>start<span class="token punctuation">,</span>end<span class="token punctuation">]</span>
</code></pre>
<h2 id="优化版本（需要吃透）">优化版本（需要吃透）</h2>
<blockquote>
<p>改变是 left 参数的引入，它是一个 boolean 类型的变量，指示我们在遇到 target == nums[mid] 时应该做什么(大于或小于的情况在两次查找中一样 大于就hi=mid 小于就lo=mid+1)。如果 left 为 true ，那么我们递归查询左区间，否则递归右区间。考虑如果我们在下标为 i 处遇到了 target ，最左边的 target 一定不会出现在下标大于 i 的位置，所以我们永远不需要考虑右子区间。当求最右下标时，道理同样适用。</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token comment"># returns leftmost (or rightmost) index at which `target` should be inserted in sorted</span>
    <span class="token comment"># array `nums` via binary search.</span>
    <span class="token keyword">def</span> <span class="token function">extreme_insertion_index</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">,</span> target<span class="token punctuation">,</span> left<span class="token punctuation">)</span><span class="token punctuation">:</span>
        lo <span class="token operator">=</span> <span class="token number">0</span>
        hi <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>

        <span class="token keyword">while</span> lo <span class="token operator">&lt;</span> hi<span class="token punctuation">:</span>
            mid <span class="token operator">=</span> <span class="token punctuation">(</span>lo <span class="token operator">+</span> hi<span class="token punctuation">)</span> <span class="token operator">//</span> <span class="token number">2</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span> <span class="token operator">&gt;</span> target <span class="token operator">or</span> <span class="token punctuation">(</span>left <span class="token operator">and</span> target <span class="token operator">==</span> nums<span class="token punctuation">[</span>mid<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                hi <span class="token operator">=</span> mid
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                lo <span class="token operator">=</span> mid<span class="token operator">+</span><span class="token number">1</span>

        <span class="token keyword">return</span> lo


    <span class="token keyword">def</span> <span class="token function">searchRange</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">,</span> target<span class="token punctuation">)</span><span class="token punctuation">:</span>
        left_idx <span class="token operator">=</span> self<span class="token punctuation">.</span>extreme_insertion_index<span class="token punctuation">(</span>nums<span class="token punctuation">,</span> target<span class="token punctuation">,</span> <span class="token boolean">True</span><span class="token punctuation">)</span>

        <span class="token comment"># assert that `left_idx` is within the array bounds and that `target`</span>
        <span class="token comment"># is actually in `nums`.</span>
        <span class="token keyword">if</span> left_idx <span class="token operator">==</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span> <span class="token operator">or</span> nums<span class="token punctuation">[</span>left_idx<span class="token punctuation">]</span> <span class="token operator">!=</span> target<span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>

        <span class="token keyword">return</span> <span class="token punctuation">[</span>left_idx<span class="token punctuation">,</span> self<span class="token punctuation">.</span>extreme_insertion_index<span class="token punctuation">(</span>nums<span class="token punctuation">,</span> target<span class="token punctuation">,</span> <span class="token boolean">False</span><span class="token punctuation">)</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>
</code></pre>

