---


---

<blockquote>
<p>Given a linked list, reverse the nodes of a linked list k at a time<br>
and return its modified list.<br>
k is a positive integer and is less than or equal to the length of the<br>
linked list. If the number of nodes is not a multiple of k then<br>
left-out nodes in the end should remain as it is.</p>
<p><strong>Example:</strong><br>
Given this linked list: 1-&gt;2-&gt;3-&gt;4-&gt;5<br>
For k = 2, you should return: 2-&gt;1-&gt;4-&gt;3-&gt;5<br>
For k = 3, you should return: 3-&gt;2-&gt;1-&gt;4-&gt;5</p>
<p><strong>Note:</strong></p>
<ul>
<li>Only constant extra memory is allowed. You may not alter the values<br>
in</li>
<li>the list’s nodes, only nodes itself may be changed.</li>
</ul>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/reverse-nodes-in-k-group/">题目</a></p>
<p><strong>思路</strong></p>
<blockquote>
<p>其实跟24题的框架一样 只不过上次的步长是2 这次的步长是k<br>
所以这个问题应该被拆成两个子问题：</p>
<ol>
<li>把长度为k的链表反转（可以用栈）</li>
<li>把1中被反转的链表连起来（这个问题在24中已经解决过了）</li>
</ol>
</blockquote>
<h2 id="双递归">双递归</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">reverseKGroup</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">,</span> k<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>
        <span class="token keyword">def</span> <span class="token function">reverseKNodes</span><span class="token punctuation">(</span>head<span class="token punctuation">,</span>cnt<span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#利用递归把长度为k的链表反转</span>
            <span class="token keyword">if</span> cnt <span class="token operator">==</span> k<span class="token punctuation">:</span>
                <span class="token keyword">return</span> head
            c <span class="token operator">=</span> reverseKNodes<span class="token punctuation">(</span>head<span class="token punctuation">.</span><span class="token builtin">next</span><span class="token punctuation">,</span>cnt<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span>
            c<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> head
            <span class="token keyword">return</span> head
            
        t <span class="token operator">=</span> head
        <span class="token comment">#作用有两点 第一找到当前步长为k的组中的最后一个元素 第二判断递归的终止条件 即本组元素不足k个</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>k<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token operator">not</span> t<span class="token punctuation">:</span>
                <span class="token keyword">return</span> head
            <span class="token keyword">if</span> i <span class="token operator">==</span> k<span class="token number">-1</span><span class="token punctuation">:</span>
            	last <span class="token operator">=</span> t
            t <span class="token operator">=</span> t<span class="token punctuation">.</span><span class="token builtin">next</span>
		<span class="token comment">#把以head为首 长度为k的组反转</span>
        reverseKNodes<span class="token punctuation">(</span>head<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span>
	    <span class="token comment">#反转后 head是当前组的最后一个节点 给他连上下一个组</span>
        head<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> self<span class="token punctuation">.</span>reverseKGroup<span class="token punctuation">(</span>t<span class="token punctuation">,</span>k<span class="token punctuation">)</span>
        <span class="token comment">#返回当前的组的最后一个节点供上一个组的head连接</span>
        <span class="token keyword">return</span> last
</code></pre>
<h2 id="非递归">非递归</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token comment"># Definition for singly-linked list.</span>
<span class="token comment"># class ListNode:</span>
<span class="token comment">#     def __init__(self, x):</span>
<span class="token comment">#         self.val = x</span>
<span class="token comment">#         self.next = None</span>

<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">reverseKGroup</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> head<span class="token punctuation">:</span> ListNode<span class="token punctuation">,</span> k<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> ListNode<span class="token punctuation">:</span>

        <span class="token keyword">def</span> <span class="token function">reverseKNodes</span><span class="token punctuation">(</span>head<span class="token punctuation">,</span>tail<span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#每两个前后节点改变他们连接的方向</span>
            first <span class="token operator">=</span> head
            second <span class="token operator">=</span> head<span class="token punctuation">.</span><span class="token builtin">next</span>
            first<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> <span class="token boolean">None</span>
            <span class="token keyword">while</span> <span class="token operator">not</span> <span class="token punctuation">(</span>first <span class="token keyword">is</span> tail<span class="token punctuation">)</span><span class="token punctuation">:</span>
                next_second <span class="token operator">=</span> second<span class="token punctuation">.</span><span class="token builtin">next</span>
                second<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> first
                first <span class="token operator">=</span> second
                second <span class="token operator">=</span> next_second

        dummy <span class="token operator">=</span> ListNode<span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">)</span>
        dummy<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> head
        tail <span class="token operator">=</span> head
        pre_head <span class="token operator">=</span> dummy
        <span class="token keyword">while</span> tail<span class="token punctuation">:</span><span class="token comment">#这里的结束条件针对链表长度刚好能被k整除的情况</span>
	        <span class="token comment">#2 把tail指向待翻转区的末尾</span>
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>k<span class="token number">-1</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                tail <span class="token operator">=</span> tail<span class="token punctuation">.</span><span class="token builtin">next</span> 
                <span class="token keyword">if</span> <span class="token operator">not</span> tail<span class="token punctuation">:</span><span class="token comment">#这里的结束条件针对链表长度不能被k整除的情况</span>
                    <span class="token keyword">return</span> dummy<span class="token punctuation">.</span><span class="token builtin">next</span>

			<span class="token comment">#3 置pre和next</span>
            pre_head<span class="token punctuation">.</span><span class="token builtin">next</span> <span class="token operator">=</span> tail
            next_head <span class="token operator">=</span> tail<span class="token punctuation">.</span><span class="token builtin">next</span>

			<span class="token comment">#4 翻转group</span>
            reverseKNodes<span class="token punctuation">(</span>head<span class="token punctuation">,</span>tail<span class="token punctuation">)</span>
            
            <span class="token comment">#5 翻转后连接 head和tail指向下一个group的头</span>
            pre_head <span class="token operator">=</span> head
            tail <span class="token operator">=</span> next_head
            head <span class="token operator">=</span> tail 

        <span class="token keyword">return</span> dummy<span class="token punctuation">.</span><span class="token builtin">next</span>
</code></pre>
<p><img src="https://pic.leetcode-cn.com/866b404c6b0b52fa02385e301ee907fc015742c3766c80c02e24ef3a8613e5ad-k%E4%B8%AA%E4%B8%80%E7%BB%84%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.png" alt="enter image description here"><br>
问题的关键是记录好每一个区域的指针 有条不紊 不然容易搞混</p>

