---


---

<blockquote>
<p>Given an array of non-negative integers, you are initially positioned at the first index of the array.<br>
Each element in the array represents your maximum jump length at that position.<br>
Determine if you are able to reach the last index.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/jump-game/">题目</a></p>
<h2 id="贪心算法">贪心算法</h2>
<blockquote>
<p>与45 Jump game II算法同理<br>
只不过要搞清楚怎么样会到不了终点，只有出现nums[i]==0的情况才会有到不了终点的可能，maxPosition永远大于等于i，大于的时候说明之前的位置能够跳过i，不会在i这里被卡住。如果等于的话就说明之前所有的j(j&lt;i)能跳到的最大距离就是i，这时候肯定会在i这里卡住。</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">canJump</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">bool</span><span class="token punctuation">:</span>
        end <span class="token operator">=</span> <span class="token number">0</span>
        maxPosition <span class="token operator">=</span> <span class="token number">0</span> 
        steps <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">==</span> <span class="token number">0</span> <span class="token operator">and</span> maxPosition <span class="token operator">==</span> i<span class="token punctuation">:</span> <span class="token keyword">return</span> <span class="token boolean">False</span>
            maxPosition <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>maxPosition<span class="token punctuation">,</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> i<span class="token punctuation">)</span>
            <span class="token keyword">if</span> i <span class="token operator">==</span> end<span class="token punctuation">:</span> end <span class="token operator">=</span> maxPosition
        <span class="token keyword">return</span> <span class="token boolean">True</span>
</code></pre>
<p>优化一下,当跳不过去时，i还在前进，所以一旦i大于maxPosition，就肯定跳不过去</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">canJump</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> nums<span class="token punctuation">:</span> List<span class="token punctuation">[</span><span class="token builtin">int</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">bool</span><span class="token punctuation">:</span>
        end <span class="token operator">=</span> <span class="token number">0</span>
        maxPosition <span class="token operator">=</span> <span class="token number">0</span> 
        steps <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>nums<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> i<span class="token operator">&gt;</span>maxPosition<span class="token punctuation">:</span> <span class="token keyword">return</span> <span class="token boolean">False</span><span class="token comment">#表示左边有一堵墙，左边任意节点，都不能跳到当前节点</span>
            maxPosition <span class="token operator">=</span> <span class="token builtin">max</span><span class="token punctuation">(</span>maxPosition<span class="token punctuation">,</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> i<span class="token punctuation">)</span>
        <span class="token keyword">return</span> <span class="token boolean">True</span>
</code></pre>

