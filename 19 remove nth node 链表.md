---


---

<blockquote>
<p>Given a linked list, remove the n-th node from the end of list and return its head.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/">题目</a></p>
<h2 id="双指针法">双指针法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># Definition for singly-linked list.</span>
<span class="token comment"># class ListNode:</span>
<span class="token comment">#     def __init__(self, x):</span>
<span class="token comment">#         self.val = x</span>
<span class="token comment">#         self.next = None</span>

<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">removeNthFromEnd</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">,</span> n<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        l <span class="token operator">=</span> head
        r <span class="token operator">=</span> head
        i <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token number">-1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            r <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token builtin">next</span>
            
        <span class="token keyword">while</span> r<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            q <span class="token operator">=</span> l<span class="token comment">#记录前驱节点</span>
            l <span class="token operator">=</span> l<span class="token punctuation">.</span><span class="token builtin">next</span>
            r <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token builtin">next</span>
        
        <span class="token keyword">if</span> l <span class="token operator">==</span> head<span class="token punctuation">:</span>
            <span class="token keyword">return</span> head<span class="token punctuation">.</span><span class="token builtin">next</span>
        
        q<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> l<span class="token punctuation">.</span><span class="token builtin">next</span>
        l<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> <span class="token boolean">None</span>
        
        <span class="token keyword">return</span> head
</code></pre>
<p>为省去记录前驱节点 可以让最后的l指针停在要删去的节点的前面 这样的话之前移动r指针就要多移一格:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># Definition for singly-linked list.</span>
<span class="token comment"># class ListNode:</span>
<span class="token comment">#     def __init__(self, x):</span>
<span class="token comment">#         self.val = x</span>
<span class="token comment">#         self.next = None</span>

<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">removeNthFromEnd</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">,</span> n<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        <span class="token keyword">if</span> <span class="token operator">not</span> head <span class="token operator">or</span> <span class="token operator">not</span> head<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token boolean">None</span>
        l <span class="token operator">=</span> head
        r <span class="token operator">=</span> head
        i <span class="token operator">=</span> <span class="token number">0</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span>
            r <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token builtin">next</span>
        
        <span class="token keyword">if</span> <span class="token operator">not</span> r<span class="token punctuation">:</span>
            <span class="token keyword">return</span> head<span class="token punctuation">.</span><span class="token builtin">next</span>
        
        <span class="token keyword">while</span> r<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">:</span>
            l <span class="token operator">=</span> l<span class="token punctuation">.</span><span class="token builtin">next</span>
            r <span class="token operator">=</span> r<span class="token punctuation">.</span><span class="token builtin">next</span>
        
        l<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span>  l<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">.</span><span class="token builtin">next</span>
        
        <span class="token keyword">return</span> head           
</code></pre>
<p>就是要注意边界情况<br>
或者设置哑节点dummy,预防链表为空的情况：</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">removeNthFromEnd</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">,</span> n<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        dummy <span class="token operator">=</span> ListNode<span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">)</span>
        dummy<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> head
        fast<span class="token punctuation">,</span>slow <span class="token operator">=</span> dummy<span class="token punctuation">,</span>dummy
        <span class="token keyword">for</span>  i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            fast <span class="token operator">=</span> fast<span class="token punctuation">.</span><span class="token builtin">next</span>
        <span class="token keyword">while</span> fast <span class="token keyword">is</span> <span class="token operator">not</span> <span class="token boolean">None</span><span class="token punctuation">:</span> 
            fast <span class="token operator">=</span> fast<span class="token punctuation">.</span><span class="token builtin">next</span>
            slow <span class="token operator">=</span> slow<span class="token punctuation">.</span><span class="token builtin">next</span>
        slow<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> slow<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">.</span><span class="token builtin">next</span>
        <span class="token keyword">return</span> dummy<span class="token punctuation">.</span><span class="token builtin">next</span>
</code></pre>

