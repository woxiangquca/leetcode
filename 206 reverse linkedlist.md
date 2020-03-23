---


---

<blockquote>
<p>Reverse a singly linked list.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/reverse-linked-list/">题目</a><br>
<a href="https://blog.csdn.net/qq_42351880/article/details/88637387">解法</a></p>
<h2 id="非递归o1空间">非递归+O(1)空间</h2>
<h3 id="思路一">思路一</h3>
<blockquote>
<p>维护一个head，中间变量node和新的头指针newHead</p>
</blockquote>
<pre class=" language-c"><code class="prism  language-c"><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> <span class="token function">reverseList</span><span class="token punctuation">(</span><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> head<span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> newHead <span class="token operator">=</span> <span class="token constant">NULL</span><span class="token punctuation">;</span>
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> node<span class="token punctuation">;</span>
    
    <span class="token keyword">while</span> <span class="token punctuation">(</span>head<span class="token operator">!=</span><span class="token constant">NULL</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
	    <span class="token comment">//头删</span>
        node <span class="token operator">=</span> head<span class="token punctuation">;</span>
        head <span class="token operator">=</span> head<span class="token operator">-&gt;</span>next<span class="token punctuation">;</span>
        <span class="token comment">//头插    </span>
        node<span class="token operator">-&gt;</span>next <span class="token operator">=</span> newHead<span class="token punctuation">;</span>
        newHead <span class="token operator">=</span> node<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> newHead<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="思路二">思路二</h3>
<blockquote>
<p>跟思路一差不多，用front，cur和rear节点表示不同的节点</p>
</blockquote>
<pre class=" language-c"><code class="prism  language-c"><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> <span class="token function">reverseList</span><span class="token punctuation">(</span><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> head<span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> front<span class="token operator">=</span><span class="token constant">NULL</span><span class="token punctuation">;</span>
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> cur<span class="token punctuation">;</span>
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> rear<span class="token punctuation">;</span>
    
    <span class="token keyword">if</span><span class="token punctuation">(</span>head<span class="token operator">==</span><span class="token constant">NULL</span><span class="token punctuation">)</span> <span class="token keyword">return</span> head<span class="token punctuation">;</span>
    
    cur <span class="token operator">=</span> head<span class="token punctuation">;</span>
    rear <span class="token operator">=</span> head<span class="token operator">-&gt;</span>next<span class="token punctuation">;</span>
        
    <span class="token keyword">while</span><span class="token punctuation">(</span>head<span class="token operator">!=</span><span class="token constant">NULL</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
        head<span class="token operator">-&gt;</span>next <span class="token operator">=</span> front<span class="token punctuation">;</span>
        
        front <span class="token operator">=</span> head<span class="token punctuation">;</span>
        head <span class="token operator">=</span> rear<span class="token punctuation">;</span>
        <span class="token keyword">if</span><span class="token punctuation">(</span>rear<span class="token operator">!=</span><span class="token constant">NULL</span><span class="token punctuation">)</span> rear <span class="token operator">=</span> rear<span class="token operator">-&gt;</span>next<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">return</span> front<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="递归">递归</h2>
<blockquote>
<p>reverseList的功能是把以head为首的链表反转，并且返回反转后链表的头部</p>
</blockquote>
<pre class=" language-c"><code class="prism  language-c"><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> <span class="token function">reverseList</span><span class="token punctuation">(</span><span class="token keyword">struct</span> ListNode<span class="token operator">*</span> head<span class="token punctuation">)</span><span class="token punctuation">{</span>
    <span class="token keyword">if</span><span class="token punctuation">(</span>head <span class="token operator">==</span> <span class="token constant">NULL</span><span class="token operator">||</span>head<span class="token operator">-&gt;</span>next <span class="token operator">==</span><span class="token constant">NULL</span><span class="token punctuation">)</span> <span class="token keyword">return</span> head<span class="token punctuation">;</span>
    
    <span class="token keyword">struct</span> ListNode<span class="token operator">*</span> newHead<span class="token punctuation">;</span>
    
    newHead <span class="token operator">=</span> <span class="token function">reverseList</span><span class="token punctuation">(</span>head<span class="token operator">-&gt;</span>next<span class="token punctuation">)</span><span class="token punctuation">;</span>
    
    head<span class="token operator">-&gt;</span>next<span class="token operator">-&gt;</span>next <span class="token operator">=</span> head<span class="token punctuation">;</span>
    head<span class="token operator">-&gt;</span>next<span class="token operator">=</span><span class="token constant">NULL</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> newHead<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>

