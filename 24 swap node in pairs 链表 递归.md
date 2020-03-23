---


---

<blockquote>
<p>Given a linked list, swap every two adjacent nodes and return its<br>
head.</p>
<p>You may not modify the values in the list’s nodes, only nodes itself<br>
may be changed.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/swap-nodes-in-pairs/">题目</a></p>
<h2 id="初始解法（纯链表操作）">初始解法（纯链表操作）</h2>
<blockquote>
<p>记录当前pair的first和second 记录下一个pair的first 把first.next连到下一个的second即可</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># Definition for singly-linked list.</span>
<span class="token comment"># class ListNode:</span>
<span class="token comment">#     def __init__(self, x):</span>
<span class="token comment">#         self.val = x</span>
<span class="token comment">#         self.next = None</span>

<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">swapPairs</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> head<span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token boolean">None</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> head<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> head
        
        first <span class="token operator">=</span> head
        second <span class="token operator">=</span> first<span class="token punctuation">.</span><span class="token builtin">next</span>
        head <span class="token operator">=</span> head<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token comment">#从第一个pair的second开始</span>
        
        <span class="token keyword">while</span> first <span class="token operator">and</span> first<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            next_first <span class="token operator">=</span> second<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token comment">#下一个first节点</span>
            
            second<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> first<span class="token comment">#倒叙连接</span>
            
            <span class="token keyword">if</span> <span class="token operator">not</span> next_first<span class="token punctuation">:</span><span class="token comment">#说明没有下一个pair</span>
                first<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> <span class="token boolean">None</span>
                <span class="token keyword">break</span>
                
            <span class="token keyword">if</span> <span class="token operator">not</span> next_first<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span><span class="token comment">#说明下一个pair只有一个节点</span>
                first<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> next_first
                <span class="token keyword">break</span>
                
            first<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> next_first<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token comment">#first是当前pair的结束 连接到下一个pair的second节点 也就是下一个pair的开始</span>
            <span class="token comment">#更新first和second节点到下一个pair</span>
            first <span class="token operator">=</span> next_first
            second <span class="token operator">=</span> first<span class="token punctuation">.</span><span class="token builtin">next</span>
            
        <span class="token keyword">return</span> head
</code></pre>
<p>也可以使用一个<strong>哑节点</strong>来避免对特殊情况的判断</p>
<h2 id="递归">递归</h2>
<blockquote>
<p>递归终止条件：当前pair没有节点或者只有一个节点<br>
递归的工作：</p>
<ol>
<li>颠倒当前pair的链接顺序</li>
<li>给当前pair的first节点连接下一个pair</li>
<li>返回second节点供上一个pair连接</li>
</ol>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># Definition for singly-linked list.</span>
<span class="token comment"># class ListNode:</span>
<span class="token comment">#     def __init__(self, x):</span>
<span class="token comment">#         self.val = x</span>
<span class="token comment">#         self.next = None</span>

<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">swapPairs</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> head <span class="token operator">or</span> <span class="token operator">not</span> head<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> head
        
        second <span class="token operator">=</span> head<span class="token punctuation">.</span><span class="token builtin">next</span>
        head<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> self<span class="token punctuation">.</span>swapPairs<span class="token punctuation">(</span>second<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">)</span>
        second<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> head
        <span class="token keyword">return</span> second
</code></pre>

