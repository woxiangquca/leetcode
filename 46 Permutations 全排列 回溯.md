---


---

<blockquote>
<p>Given a collection of <strong>distinct</strong> integers, return all possible permutations.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/permutations/">题目</a></p>
<h2 id="递归">递归</h2>
<p><img src="https://pic.leetcode-cn.com/0bf18f9b86a2542d1f6aa8db6cc45475fce5aa329a07ca02a9357c2ead81eec1-image.png" alt="enter image description here"></p>
<blockquote>
<p>put(index)含义为把nums[index]放置到序列中</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permute</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        tmp <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        n <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        valid <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token boolean">True</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">]</span>
        
        <span class="token keyword">def</span> <span class="token function">put</span><span class="token punctuation">(</span>index<span class="token punctuation">)</span><span class="token punctuation">:</span>
            valid<span class="token punctuation">[</span>index<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">False</span><span class="token comment">#先放置</span>
            tmp<span class="token punctuation">.</span>append<span class="token punctuation">(</span>nums<span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">)</span>
            
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>tmp<span class="token punctuation">)</span> <span class="token operator">==</span> n<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>copy<span class="token punctuation">.</span>deepcopy<span class="token punctuation">(</span>tmp<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token comment">#注意python append使用浅拷贝 只传地址 所以必须要深拷贝或者append(tmp[:])</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#再递归</span>
                    <span class="token keyword">if</span> valid<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span> put<span class="token punctuation">(</span>i<span class="token punctuation">)</span>
                
            valid<span class="token punctuation">[</span>index<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">True</span><span class="token comment">#再弹出</span>
            tmp<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>
        
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span> put<span class="token punctuation">(</span>i<span class="token punctuation">)</span> <span class="token comment">#这个方法的不足就是需要初始放置</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>有点啰嗦，可以把初始的循环和put内的循环合并，如下</p>
<blockquote>
<p>work()代表给tmp后面填加一个数。如果用c语言写就是work(index)，代表给tmp[index]赋值，但由于index永远是最后一位，所以在python中可以省略</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permute</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        tmp <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        n <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        valid <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token boolean">True</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">]</span>
        
        <span class="token keyword">def</span> <span class="token function">work</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>tmp<span class="token punctuation">)</span> <span class="token operator">==</span> n<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>copy<span class="token punctuation">.</span>deepcopy<span class="token punctuation">(</span>tmp<span class="token punctuation">)</span><span class="token punctuation">)</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span>
                    <span class="token keyword">if</span> valid<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span> 
                        valid<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">False</span>
                        tmp<span class="token punctuation">.</span>append<span class="token punctuation">(</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>
                        work<span class="token punctuation">(</span><span class="token punctuation">)</span>
                        valid<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">True</span>
                        tmp<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>
        
        work<span class="token punctuation">(</span><span class="token punctuation">)</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>这里使用一些递归的技巧，不用全局变量，把path和res当作参数传递</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permute</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        
        <span class="token keyword">def</span> <span class="token function">dfs</span><span class="token punctuation">(</span>path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span> <span class="token operator">==</span> size<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>path<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
                <span class="token keyword">return</span>

            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> <span class="token operator">not</span> used<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">:</span>
                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">True</span>
                    path<span class="token punctuation">.</span>append<span class="token punctuation">(</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>

                    dfs<span class="token punctuation">(</span>path<span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>

                    used<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">False</span>
                    path<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>
                    
        used <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token boolean">False</span> <span class="token keyword">for</span> _ <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">]</span>
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dfs<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span> used<span class="token punctuation">,</span> res<span class="token punctuation">)</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>可以把path数组和used数组的变化体现在参数传递中，不用单独写出来</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permute</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
	    size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        <span class="token keyword">if</span> size <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token keyword">def</span> <span class="token function">dfs</span><span class="token punctuation">(</span>path<span class="token punctuation">,</span> state<span class="token punctuation">,</span> res<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span> <span class="token operator">==</span> size<span class="token punctuation">:</span>
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>path<span class="token punctuation">)</span>
                <span class="token keyword">return</span>

            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token punctuation">(</span>state <span class="token operator">&gt;&gt;</span> i<span class="token punctuation">)</span> <span class="token operator">&amp;</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
                    dfs<span class="token punctuation">(</span>path <span class="token operator">+</span> <span class="token punctuation">[</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span> state <span class="token operator">^</span> <span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">&lt;&lt;</span> i<span class="token punctuation">)</span><span class="token punctuation">,</span> res<span class="token punctuation">)</span>
        state <span class="token operator">=</span> <span class="token number">0</span>
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dfs<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span> state<span class="token punctuation">,</span> res<span class="token punctuation">)</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>更清晰的解释可以看<a href="https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liweiw/">题解</a></p>
<h2 id="动态规划（非递归）">动态规划（非递归）</h2>
<blockquote>
<p>递推式：如果 nums 长度为 1，比如 nums = [1]，全排列显然是 { [1] }，共一个元素；<br>
当 nums 长度为 2，比如 nums = [1, 2]，其全排列为：对于 [1] 全排列的每一项的所有间隙插入 2，即 {[2, 1], [1, 2]}；<br>
当 nums 长度为 3 时，比如 [1, 2, 3]：<br>
第一步：{ [1] }<br>
第二步：{[2, 1], [1, 2]}<br>
第三步：{[3, 2, 1], [2, 3, 1], [2, 1, 3], [3, 1, 2], [1, 3, 2], [1, 2, 3]}；</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">permute</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        n <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span>
        dp <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">]</span>
        dp<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>append<span class="token punctuation">(</span><span class="token punctuation">[</span>nums<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">)</span>

        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span>
            len_ <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>dp<span class="token punctuation">[</span>i<span class="token number">-1</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
            <span class="token keyword">for</span> index <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>dp<span class="token punctuation">[</span>i<span class="token number">-1</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> insert_index <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>len_<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    dp<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">.</span>append<span class="token punctuation">(</span>copy<span class="token punctuation">.</span>deepcopy<span class="token punctuation">(</span>dp<span class="token punctuation">[</span>i<span class="token number">-1</span><span class="token punctuation">]</span><span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
                    dp<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">.</span>insert<span class="token punctuation">(</span>insert_index<span class="token punctuation">,</span>nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>
        
        <span class="token keyword">return</span> dp<span class="token punctuation">[</span>n<span class="token number">-1</span><span class="token punctuation">]</span>
</code></pre>

