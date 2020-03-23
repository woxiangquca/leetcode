---


---

<blockquote>
<p>Given a string containing just the characters ‘(’, ‘)’, ‘{’, ‘}’, ‘[’<br>
and ‘]’, determine if the input string is valid.</p>
<p>An input string is valid if:</p>
<p>Open brackets must be closed by the same type of brackets. Open<br>
brackets must be closed in the correct order. Note that an empty<br>
string is also considered valid.</p>
</blockquote>
<h2 id="栈">栈</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">isValid</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">:</span> <span class="token builtin">str</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">bool</span><span class="token punctuation">:</span>
        stack <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dic <span class="token operator">=</span> <span class="token punctuation">{</span><span class="token string">')'</span><span class="token punctuation">:</span><span class="token string">'('</span> <span class="token punctuation">,</span> <span class="token string">']'</span><span class="token punctuation">:</span><span class="token string">'['</span> <span class="token punctuation">,</span> <span class="token string">'}'</span><span class="token punctuation">:</span><span class="token string">'{'</span><span class="token punctuation">}</span>
        
        <span class="token keyword">for</span> a <span class="token keyword">in</span> s<span class="token punctuation">:</span>
            <span class="token keyword">if</span> a <span class="token keyword">in</span> <span class="token punctuation">[</span><span class="token string">'('</span><span class="token punctuation">,</span><span class="token string">'{'</span><span class="token punctuation">,</span><span class="token string">'['</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
                stack<span class="token punctuation">.</span>append<span class="token punctuation">(</span>a<span class="token punctuation">)</span>
            
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>stack<span class="token punctuation">)</span> <span class="token operator">and</span> stack<span class="token punctuation">[</span><span class="token builtin">len</span><span class="token punctuation">(</span>stack<span class="token punctuation">)</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">==</span> dic<span class="token punctuation">[</span>a<span class="token punctuation">]</span><span class="token punctuation">:</span>
                    stack<span class="token punctuation">.</span>pop<span class="token punctuation">(</span><span class="token punctuation">)</span>
                <span class="token keyword">else</span><span class="token punctuation">:</span>
                    <span class="token keyword">return</span> <span class="token boolean">False</span>
        
        <span class="token keyword">return</span> <span class="token operator">not</span> stack
</code></pre>
<p>就是括号匹配的问题</p>
<h2 id="赖皮法">赖皮法</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">isValid</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token keyword">while</span> <span class="token string">'{}'</span> <span class="token keyword">in</span> s <span class="token operator">or</span> <span class="token string">'()'</span> <span class="token keyword">in</span> s <span class="token operator">or</span> <span class="token string">'[]'</span> <span class="token keyword">in</span> s<span class="token punctuation">:</span>
            s <span class="token operator">=</span> s<span class="token punctuation">.</span>replace<span class="token punctuation">(</span><span class="token string">'{}'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">)</span>
            s <span class="token operator">=</span> s<span class="token punctuation">.</span>replace<span class="token punctuation">(</span><span class="token string">'[]'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">)</span>
            s <span class="token operator">=</span> s<span class="token punctuation">.</span>replace<span class="token punctuation">(</span><span class="token string">'()'</span><span class="token punctuation">,</span> <span class="token string">''</span><span class="token punctuation">)</span>
        <span class="token keyword">return</span> s <span class="token operator">==</span> <span class="token string">''</span>
</code></pre>

