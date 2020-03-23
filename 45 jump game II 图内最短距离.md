---


---

<blockquote>
<p>Given an array of non-negative integers, you are initially positioned at the first index of the array.<br>
Each element in the array represents your maximum jump length at that position.<br>
Your goal is to reach the last index in the minimum number of jumps.<br>
<a href="https://leetcode-cn.com/problems/jump-game-ii/">题目</a></p>
</blockquote>
<h2 id="贪心算法">贪心算法</h2>
<blockquote>
<p>我们每次在<strong>可跳范围</strong>内选择可以使得跳的更远的位置。由于题目说明了一定能跳到最后，所以不用从后往前 从前往后即可</p>
</blockquote>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">int</span> <span class="token function">jump</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> nums<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">int</span> end <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
    <span class="token keyword">int</span> maxPosition <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> 
    <span class="token keyword">int</span> steps <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
    <span class="token keyword">for</span><span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> nums<span class="token punctuation">.</span>length <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
        <span class="token comment">//找能跳的最远的</span>
        maxPosition <span class="token operator">=</span> Math<span class="token punctuation">.</span><span class="token function">max</span><span class="token punctuation">(</span>maxPosition<span class="token punctuation">,</span> nums<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> i<span class="token punctuation">)</span><span class="token punctuation">;</span> 
        <span class="token keyword">if</span><span class="token punctuation">(</span> i <span class="token operator">==</span> end<span class="token punctuation">)</span><span class="token punctuation">{</span> <span class="token comment">//遇到边界，就更新边界，并且步数加一</span>
            end <span class="token operator">=</span> maxPosition<span class="token punctuation">;</span>
            steps<span class="token operator">++</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> steps<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p><a href="https://leetcode-cn.com/problems/jump-game-ii/solution/45-by-ikaruga/">贪心解法详细</a><br>
这种写法是一边走一边更新比较简洁 也可以使用双层循环，先确定范围，在范围里选，然后更改cur_position</p>
<h2 id="动态规划">动态规划</h2>
<blockquote>
<p>注意两点：</p>
<ol>
<li>从前往后进行动态规划，dp数组记录跳到当前格的最少步数</li>
<li>一定要剪枝</li>
</ol>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/jump-game-ii/solution/dong-tai-gui-hua-yong-shi-ji-bai-99nei-cun-ji-bai-/">动态规划</a></p>

