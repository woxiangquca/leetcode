---


---

<blockquote>
<p>Given n pairs of parentheses, write a function to generate all<br>
combinations of well-formed parentheses.</p>
<p>For example, given n = 3, a solution set is:</p>
<p>[   “((()))”,   “(()())”,   “(())()”,   “()(())”,   “()()()” ]</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/generate-parentheses/">题目</a></p>
<h2 id="正常递归剪枝">正常递归+剪枝</h2>
<blockquote>
<p>只有在我们知道序列仍然保持有效时才添加 <code>'('</code> or <code>')'</code><br>
如果我们还剩一个位置，我们可以开始放一个左括号。 如果它不超过左括号的数量，我们可以放一个右括号。</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">(</span><span class="token builtin">object</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">generateParenthesis</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> N<span class="token punctuation">)</span><span class="token punctuation">:</span>
        ans <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token keyword">def</span> <span class="token function">backtrack</span><span class="token punctuation">(</span>S <span class="token operator">=</span> <span class="token string">''</span><span class="token punctuation">,</span> left <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span> right <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>S<span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">2</span> <span class="token operator">*</span> N<span class="token punctuation">:</span>
                ans<span class="token punctuation">.</span>append<span class="token punctuation">(</span>S<span class="token punctuation">)</span>
                <span class="token keyword">return</span>
            <span class="token keyword">if</span> left <span class="token operator">&lt;</span> N<span class="token punctuation">:</span>
                backtrack<span class="token punctuation">(</span>S<span class="token operator">+</span><span class="token string">'('</span><span class="token punctuation">,</span> left<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">,</span> right<span class="token punctuation">)</span>
            <span class="token keyword">if</span> right <span class="token operator">&lt;</span> left<span class="token punctuation">:</span>
                backtrack<span class="token punctuation">(</span>S<span class="token operator">+</span><span class="token string">')'</span><span class="token punctuation">,</span> left<span class="token punctuation">,</span> right<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span>

        backtrack<span class="token punctuation">(</span><span class="token punctuation">)</span>
        <span class="token keyword">return</span> ans
</code></pre>
<h2 id="另一种递归">另一种递归</h2>
<blockquote>
<p>对于任何一个括号组合（1对以上），可以表达为这么一种组合 ( left ) right 的形式。其中，若left 和right 两部分的括号总数为 n-1对，那么新的组合 ( left ) right则有n对<br>
这样将n对括号求解，转化为n-1对的求解，以此类推直到零对括号可以直接给出空字符串的解</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">(</span><span class="token builtin">object</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">generateParenthesis</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> N<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> N <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span> <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token string">''</span><span class="token punctuation">]</span>
        ans <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        <span class="token keyword">for</span> c <span class="token keyword">in</span> <span class="token builtin">xrange</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> left <span class="token keyword">in</span> self<span class="token punctuation">.</span>generateParenthesis<span class="token punctuation">(</span>c<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> right <span class="token keyword">in</span> self<span class="token punctuation">.</span>generateParenthesis<span class="token punctuation">(</span>N<span class="token number">-1</span><span class="token operator">-</span>c<span class="token punctuation">)</span><span class="token punctuation">:</span>
                    ans<span class="token punctuation">.</span>append<span class="token punctuation">(</span><span class="token string">'({}){}'</span><span class="token punctuation">.</span><span class="token builtin">format</span><span class="token punctuation">(</span>left<span class="token punctuation">,</span> right<span class="token punctuation">)</span><span class="token punctuation">)</span>
        <span class="token keyword">return</span> ans
</code></pre>
<p>唉 想不到啊</p>
<h2 id="动态规划">动态规划</h2>
<blockquote>
<p>当我们清楚所有 i&lt;n 时括号的可能生成排列后，对与 i=n 的情况，我们考虑整个括号排列中最左边的括号。<br>
它一定是一个左括号，那么它可以和它对应的右括号组成一组完整的括号 “( )”，我们认为这一组是相比 n-1 增加进来的括号。<br>
剩下的括号要么在这一组新增的括号内部，要么在这一组新增括号的外部（右侧）。<br>
既然知道了 i&lt;n 的情况，那我们就可以对所有情况进行遍历：<br>
“(” + 【i=p时所有括号的排列组合】 + “)” + 【i=q时所有括号的排列组合】其中 p + q = n-1，且 p q 均为非负整数。<br>
事实上，当上述 p 从 0 取到 n-1，q 从 n-1 取到 0 后，所有情况就遍历完了。<br>
注：上述遍历是没有重复情况出现的，即当 (p1,q1)≠(p2,q2) 时，按上述方式取的括号组合一定不同。</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">generateParenthesis</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> n<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span><span class="token builtin">str</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        <span class="token keyword">if</span> n <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        total_l <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        total_l<span class="token punctuation">.</span>append<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token boolean">None</span><span class="token punctuation">]</span><span class="token punctuation">)</span>    <span class="token comment"># 0组括号时记为None</span>
        total_l<span class="token punctuation">.</span>append<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token string">"()"</span><span class="token punctuation">]</span><span class="token punctuation">)</span>    <span class="token comment"># 1组括号只有一种情况</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">,</span>n<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>    <span class="token comment"># 开始计算i组括号时的括号组合</span>
            l <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>        
            <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>i<span class="token punctuation">)</span><span class="token punctuation">:</span>    <span class="token comment"># 开始遍历 p q ，其中p+q=i-1 , j 作为索引</span>
                now_list1 <span class="token operator">=</span> total_l<span class="token punctuation">[</span>j<span class="token punctuation">]</span>    <span class="token comment"># p = j 时的括号组合情况</span>
                now_list2 <span class="token operator">=</span> total_l<span class="token punctuation">[</span>i<span class="token number">-1</span><span class="token operator">-</span>j<span class="token punctuation">]</span>    <span class="token comment"># q = (i-1) - j 时的括号组合情况</span>
                <span class="token keyword">for</span> k1 <span class="token keyword">in</span> now_list1<span class="token punctuation">:</span>  
                    <span class="token keyword">for</span> k2 <span class="token keyword">in</span> now_list2<span class="token punctuation">:</span>
                        <span class="token keyword">if</span> k1 <span class="token operator">==</span> <span class="token boolean">None</span><span class="token punctuation">:</span>
                            k1 <span class="token operator">=</span> <span class="token string">""</span>
                        <span class="token keyword">if</span> k2 <span class="token operator">==</span> <span class="token boolean">None</span><span class="token punctuation">:</span>
                            k2 <span class="token operator">=</span> <span class="token string">""</span>
                        el <span class="token operator">=</span> <span class="token string">"("</span> <span class="token operator">+</span> k1 <span class="token operator">+</span> <span class="token string">")"</span> <span class="token operator">+</span> k2
                        l<span class="token punctuation">.</span>append<span class="token punctuation">(</span>el<span class="token punctuation">)</span>    <span class="token comment"># 把所有可能的情况添加到 l 中</span>
            total_l<span class="token punctuation">.</span>append<span class="token punctuation">(</span>l<span class="token punctuation">)</span>    <span class="token comment"># l这个list就是i组括号的所有情况，添加到total_l中，继续求解i=i+1的情况</span>
        <span class="token keyword">return</span> total_l<span class="token punctuation">[</span>n<span class="token punctuation">]</span>
</code></pre>

