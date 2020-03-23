---


---

<blockquote>
<p>Given a collection of numbers that might contain duplicates, return all possible unique permutations.</p>
</blockquote>
<h2 id="回溯剪枝">回溯+剪枝</h2>
<blockquote>
<p>与46主体部分一样不过需要剪枝<br>
<strong>剪枝的逻辑为</strong>：假如当前准备给序列末尾添加x，那么就在原集合中寻找x前的离x最近且与x相等的数（使用辅助数组repeat），查看这些数是否已经在序列中，如果有一个不在，说明可以剪枝<br>
<strong>原因</strong>：因为我们给序列添加数的逻辑为for i  in range(size)，是从前往后遍历的。所以如果现在在序列的第t位放x2,且x2之前有出现x1，则之前必有遍历到在序列的第t位放x1的情况，且x1==x2<br>
<strong>注意</strong>：假设序列中有x1…xn且x1 == x2 == … == xn，则在判断xn是否需要剪枝时只需看xn-1是否出现在已有序列里，如果xn-1出现，则前面的必然出现，如果xn-1没出现，就已经可以表明xn需要剪枝</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permuteUnique</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        repeat <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">]</span>
            
        <span class="token keyword">def</span> <span class="token function">dfs</span><span class="token punctuation">(</span>path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span> <span class="token operator">==</span> size<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>path<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
                <span class="token keyword">return</span>

            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">not</span> used<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">and</span> <span class="token punctuation">(</span>repeat<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">&lt;</span> <span class="token number">0</span> <span class="token operator">or</span> used<span class="token punctuation">[</span>repeat<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">True</span>
                    path<span class="token punctuation">.</span>append<span class="token punctuation">(</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>

                    dfs<span class="token punctuation">(</span>path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>

                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">False</span>
                    path<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>

        <span class="token keyword">def</span> <span class="token function">find_repeat</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>i<span class="token number">-1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    <span class="token keyword">if</span> nums<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">==</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span> 
                        repeat<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> j<span class="token comment"># repeat[i] = i之前离i最近的与nums[i]相等的数</span>
                        <span class="token keyword">break</span>
            
        find_repeat<span class="token punctuation">(</span><span class="token punctuation">)</span>
        used <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token boolean">False</span> <span class="token keyword">for</span> _ <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">]</span>
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dfs<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>
        <span class="token keyword">return</span> res
</code></pre>
<blockquote>
<p>也可以先排序，这样就不需要repeat数组，直接可以判断nums[i]和nums[i-1]</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>

    <span class="token keyword">def</span> <span class="token function">permuteUnique</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>

        <span class="token keyword">def</span> <span class="token function">dfs</span><span class="token punctuation">(</span>nums<span class="token punctuation">,</span> size<span class="token punctuation">,</span> depth<span class="token punctuation">,</span> path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> depth <span class="token operator">==</span> size<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>path<span class="token punctuation">.</span>copy<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
                <span class="token keyword">return</span>
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> <span class="token operator">not</span> used<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span>

                    <span class="token keyword">if</span> i <span class="token operator">&gt;</span> <span class="token number">0</span> <span class="token operator">and</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">==</span> nums<span class="token punctuation">[</span>i <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">and</span> <span class="token operator">not</span> used<span class="token punctuation">[</span>i <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
                        <span class="token keyword">continue</span>

                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">True</span>
                    path<span class="token punctuation">.</span>append<span class="token punctuation">(</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>
                    dfs<span class="token punctuation">(</span>nums<span class="token punctuation">,</span> size<span class="token punctuation">,</span> depth <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">,</span> path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>
                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">False</span>
                    path<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>

        size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">if</span> size <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>

        nums<span class="token punctuation">.</span>sort<span class="token punctuation">(</span><span class="token punctuation">)</span>

        used <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token boolean">False</span><span class="token punctuation">]</span> <span class="token operator">*</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dfs<span class="token punctuation">(</span>nums<span class="token punctuation">,</span> size<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>可以参考<a href="https://leetcode-cn.com/problems/permutations-ii/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liwe-2/">题解</a></p>

