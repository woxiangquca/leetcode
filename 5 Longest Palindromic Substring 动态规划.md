---


---

<blockquote>
<p>Given a string s, find the longest palindromic substring in s. You may<br>
assume that the maximum length of s is 1000.</p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/longest-palindromic-substring/">题目</a></p>
<h2 id="暴力解法">暴力解法</h2>
<blockquote>
<p>遍历所有可能的子串 找出其中的回文串并比较大小</p>
</blockquote>
<p>总共有<span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mfrac><mrow><mi>n</mi><mo stretchy="false">(</mo><mi>n</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo></mrow><mn>2</mn></mfrac></mrow><annotation encoding="application/x-tex">\frac{n(n-1)}{2}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1.355em; vertical-align: -0.345em;"></span><span class="mord"><span class="mopen nulldelimiter"></span><span class="mfrac"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.01em;"><span class="" style="top: -2.655em;"><span class="pstrut" style="height: 3em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">2</span></span></span></span><span class="" style="top: -3.23em;"><span class="pstrut" style="height: 3em;"></span><span class="frac-line" style="border-bottom-width: 0.04em;"></span></span><span class="" style="top: -3.485em;"><span class="pstrut" style="height: 3em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathdefault mtight">n</span><span class="mopen mtight">(</span><span class="mord mathdefault mtight">n</span><span class="mbin mtight">−</span><span class="mord mtight">1</span><span class="mclose mtight">)</span></span></span></span></span><span class="vlist-s">​</span></span><span class="vlist-r"><span class="vlist" style="height: 0.345em;"><span class=""></span></span></span></span></span><span class="mclose nulldelimiter"></span></span></span></span></span></span>个子串 对于每个子串从首尾开始验证 需要O(n)的复杂度<br>
一共是O(<span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><msup><mi>x</mi><mn>3</mn></msup></mrow><annotation encoding="application/x-tex">x^3</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.814108em; vertical-align: 0em;"></span><span class="mord"><span class="mord mathdefault">x</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.814108em;"><span class="" style="top: -3.063em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">3</span></span></span></span></span></span></span></span></span></span></span></span>)的复杂度</p>
<h2 id="最长公共子串法">最长公共子串法</h2>
<blockquote>
<p>反转 SS，使之变成 S’S′。找到 SS 和 S’S′ 之间最长的公共子串，这也必然是最长的回文子串。</p>
</blockquote>
<p>需要注意的是 <strong>找的的最长公共字串还需要满足对应字符索引之和为字符串长度</strong> 例如<br>
s = ‘abacdfgdcaba’<br>
s’ = ‘abacdgfdcaba’<br>
s与s’之间的最长公共子串为‘abacd’ 不是回文</p>
<p>所以这个方法本质上是在求两个字符串的<strong>最大公共子串</strong><br>
关于最大公共子串的求法见<strong>算法—&gt;最大公共子串和子序列</strong></p>
<h2 id="中心扩散法">中心扩散法</h2>
<blockquote>
<p>遍历每一个索引，以这个索引为中心，利用“回文串”中心对称的特点，往两边扩散，看最多能扩散多远。</p>
</blockquote>
<p>使用时要注意一个细节：<strong>回文串的长度可能是奇数，也可能是偶数</strong>。对于扩散函数我们应该设计以下两种情况：</p>
<ol>
<li>如果传入<strong>重合</strong>的索引编码，进行中心扩散，此时得到的最长回文子串的长度是奇数；</li>
<li>如果传入<strong>相邻</strong>的索引编码，进行中心扩散，此时得到的最长回文子串的长度是偶数。</li>
</ol>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">longestPalindrome</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">)</span><span class="token punctuation">:</span>
        size <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span>
        <span class="token keyword">if</span> size <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">:</span>
            <span class="token keyword">return</span> <span class="token string">''</span>

        <span class="token comment"># 至少是 1</span>
        max_length <span class="token operator">=</span> <span class="token number">1</span>
        p_str <span class="token operator">=</span> s<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span>

        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>size<span class="token punctuation">)</span><span class="token punctuation">:</span>
            p_odd<span class="token punctuation">,</span> odd_len <span class="token operator">=</span> self<span class="token punctuation">.</span>__center_spread<span class="token punctuation">(</span>s<span class="token punctuation">,</span> size<span class="token punctuation">,</span> i<span class="token punctuation">,</span> i<span class="token punctuation">)</span>
            p_even<span class="token punctuation">,</span> even_len <span class="token operator">=</span> self<span class="token punctuation">.</span>__center_spread<span class="token punctuation">(</span>s<span class="token punctuation">,</span> size<span class="token punctuation">,</span> i<span class="token punctuation">,</span> i <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span>

            <span class="token comment"># 当前找到的最长回文子串</span>
            cur_max_sub <span class="token operator">=</span> p_odd <span class="token keyword">if</span> odd_len <span class="token operator">&gt;=</span> even_len <span class="token keyword">else</span> p_even
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>cur_max_sub<span class="token punctuation">)</span> <span class="token operator">&gt;</span> max_length<span class="token punctuation">:</span>
                max_length <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>cur_max_sub<span class="token punctuation">)</span>
                p_str <span class="token operator">=</span> cur_max_sub

        <span class="token keyword">return</span> p_str

    <span class="token keyword">def</span> <span class="token function">__center_spread</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> s<span class="token punctuation">,</span> size<span class="token punctuation">,</span> left<span class="token punctuation">,</span> right<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token triple-quoted-string string">"""
        left = right 的时候，此时回文中心是一条线，回文串的长度是奇数
        right = left + 1 的时候，此时回文中心是任意一个字符，回文串的长度是偶数
        """</span>
        l <span class="token operator">=</span> left
        r <span class="token operator">=</span> right

        <span class="token keyword">while</span> l <span class="token operator">&gt;=</span> <span class="token number">0</span> <span class="token operator">and</span> r <span class="token operator">&lt;</span> size <span class="token operator">and</span> s<span class="token punctuation">[</span>l<span class="token punctuation">]</span> <span class="token operator">==</span> s<span class="token punctuation">[</span>r<span class="token punctuation">]</span><span class="token punctuation">:</span>
            l <span class="token operator">-=</span> <span class="token number">1</span>
            r <span class="token operator">+=</span> <span class="token number">1</span>
        <span class="token keyword">return</span> s<span class="token punctuation">[</span>l <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">:</span>r<span class="token punctuation">]</span><span class="token punctuation">,</span> r <span class="token operator">-</span> l <span class="token operator">-</span> <span class="token number">1</span>
</code></pre>
<h2 id="动态规划">动态规划</h2>
<p>dp[l][r]表示子串s[l:r]是否为回文串<br>
状态转移方程为：<br>
<span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>d</mi><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo><mo stretchy="false">[</mo><mi>r</mi><mo stretchy="false">]</mo><mo>=</mo><mrow><mo fence="true">{</mo><mtable rowspacing="0.3599999999999999em" columnalign="left left" columnspacing="1em"><mtr><mtd><mstyle scriptlevel="0" displaystyle="false"><mn>0</mn></mstyle></mtd><mtd><mstyle scriptlevel="0" displaystyle="false"><mrow><mi>s</mi><mo stretchy="false">[</mo><mi>l</mi><mo stretchy="false">]</mo><mo stretchy="false">!</mo><mo>=</mo><mi>s</mi><mo stretchy="false">[</mo><mi>r</mi><mo stretchy="false">]</mo></mrow></mstyle></mtd></mtr><mtr><mtd><mstyle scriptlevel="0" displaystyle="false"><mrow><mi>d</mi><mi>p</mi><mo stretchy="false">[</mo><mi>l</mi><mo>+</mo><mn>1</mn><mo stretchy="false">]</mo><mo stretchy="false">[</mo><mi>r</mi><mo>−</mo><mn>1</mn><mo stretchy="false">]</mo></mrow></mstyle></mtd><mtd><mstyle scriptlevel="0" displaystyle="false"><mrow><mi>s</mi><mo stretchy="false">[</mo><mi>i</mi><mo stretchy="false">]</mo><mo>=</mo><mo>=</mo><mi>s</mi><mo stretchy="false">[</mo><mi>j</mi><mo stretchy="false">]</mo><mi mathvariant="normal">∣</mi><mi mathvariant="normal">∣</mi><mi>r</mi><mo>−</mo><mi>l</mi><mo>&gt;</mo><mo>=</mo><mn>2</mn></mrow></mstyle></mtd></mtr></mtable></mrow></mrow><annotation encoding="application/x-tex">d[l][r] = \begin{cases}
0 &amp; s[l]!=s[r] \\
dp[l+1][r-1] &amp; s[i] == s[j] || r-l&gt;=2
\end{cases}</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathdefault">d</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.01968em;">l</span><span class="mclose">]</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.02778em;">r</span><span class="mclose">]</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 3.00003em; vertical-align: -1.25003em;"></span><span class="minner"><span class="mopen delimcenter" style="top: 0em;"><span class="delimsizing size4">{</span></span><span class="mord"><span class="mtable"><span class="col-align-l"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.69em;"><span class="" style="top: -3.69em;"><span class="pstrut" style="height: 3.008em;"></span><span class="mord"><span class="mord">0</span></span></span><span class="" style="top: -2.25em;"><span class="pstrut" style="height: 3.008em;"></span><span class="mord"><span class="mord mathdefault">d</span><span class="mord mathdefault">p</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.01968em;">l</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mord">1</span><span class="mclose">]</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.02778em;">r</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mord">1</span><span class="mclose">]</span></span></span></span><span class="vlist-s">​</span></span><span class="vlist-r"><span class="vlist" style="height: 1.19em;"><span class=""></span></span></span></span></span><span class="arraycolsep" style="width: 1em;"></span><span class="col-align-l"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.69em;"><span class="" style="top: -3.69em;"><span class="pstrut" style="height: 3.008em;"></span><span class="mord"><span class="mord mathdefault">s</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.01968em;">l</span><span class="mclose">]</span><span class="mclose">!</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mord mathdefault">s</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.02778em;">r</span><span class="mclose">]</span></span></span><span class="" style="top: -2.25em;"><span class="pstrut" style="height: 3.008em;"></span><span class="mord"><span class="mord mathdefault">s</span><span class="mopen">[</span><span class="mord mathdefault">i</span><span class="mclose">]</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mord mathdefault">s</span><span class="mopen">[</span><span class="mord mathdefault" style="margin-right: 0.05724em;">j</span><span class="mclose">]</span><span class="mord">∣</span><span class="mord">∣</span><span class="mord mathdefault" style="margin-right: 0.02778em;">r</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mord mathdefault" style="margin-right: 0.01968em;">l</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">&gt;</span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mord">2</span></span></span></span><span class="vlist-s">​</span></span><span class="vlist-r"><span class="vlist" style="height: 1.19em;"><span class=""></span></span></span></span></span></span></span><span class="mclose nulldelimiter"></span></span></span></span></span></span><br>
当r-l&lt;=2时 s[l+1,r-1]有0个或一个元素 这时s[l+1,r-1]一定为回文串</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">longestPalindrome</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span>s<span class="token punctuation">:</span><span class="token builtin">str</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
        n <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">;</span>
        res <span class="token operator">=</span> <span class="token string">""</span><span class="token punctuation">;</span>
        dp <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token boolean">False</span> <span class="token keyword">for</span> _ <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">]</span> <span class="token keyword">for</span> _ <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">]</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token number">-1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#需要从i+1推出i 所以倒叙</span>
            <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token number">-1</span><span class="token punctuation">,</span>i<span class="token number">-1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#倒叙顺序都一样</span>
                dp<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">=</span> s<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">==</span> s<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">and</span> <span class="token punctuation">(</span>j <span class="token operator">-</span> i <span class="token operator">&lt;</span> <span class="token number">2</span> <span class="token operator">or</span> dp<span class="token punctuation">[</span>i <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
                <span class="token keyword">if</span> <span class="token punctuation">(</span>dp<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">and</span> j <span class="token operator">-</span> i <span class="token operator">+</span> <span class="token number">1</span> <span class="token operator">&gt;</span> <span class="token builtin">len</span><span class="token punctuation">(</span>res<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    res <span class="token operator">=</span> s<span class="token punctuation">[</span>i<span class="token punctuation">:</span>j<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">]</span>
        <span class="token keyword">return</span> res
</code></pre>
<p>注意根据转换方程确定<strong>循环方向</strong><br>
动态规划法并没有中心扩散法快 但这是一种非常具有普适性的方法</p>
<h3 id="可以对空间复杂度进行优化">可以对空间复杂度进行优化</h3>
<p>因为dp[i][j] = dp[i+1][j-1]用到的数据都是在i+1层 所以可以1把i+1这个维度省去</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> String <span class="token function">longestPalindrome7</span><span class="token punctuation">(</span>String s<span class="token punctuation">)</span> <span class="token punctuation">{</span>
		<span class="token keyword">int</span> n <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		String res <span class="token operator">=</span> <span class="token string">""</span><span class="token punctuation">;</span>
		<span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span> P <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">boolean</span><span class="token punctuation">[</span>n<span class="token punctuation">]</span><span class="token punctuation">;</span>
		<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> n <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">;</span> i <span class="token operator">&gt;=</span> <span class="token number">0</span><span class="token punctuation">;</span> i<span class="token operator">--</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
			<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> j <span class="token operator">=</span> n <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">;</span> j <span class="token operator">&gt;=</span> i<span class="token punctuation">;</span> j<span class="token operator">--</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
				P<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">charAt</span><span class="token punctuation">(</span>i<span class="token punctuation">)</span> <span class="token operator">==</span> s<span class="token punctuation">.</span><span class="token function">charAt</span><span class="token punctuation">(</span>j<span class="token punctuation">)</span> <span class="token operator">&amp;&amp;</span> <span class="token punctuation">(</span>j <span class="token operator">-</span> i <span class="token operator">&lt;</span> <span class="token number">3</span> <span class="token operator">||</span> P<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
				<span class="token keyword">if</span> <span class="token punctuation">(</span>P<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">&amp;&amp;</span> j <span class="token operator">-</span> i <span class="token operator">+</span> <span class="token number">1</span> <span class="token operator">&gt;</span> res<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
					res <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">substring</span><span class="token punctuation">(</span>i<span class="token punctuation">,</span> j <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
				<span class="token punctuation">}</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>
		<span class="token keyword">return</span> res<span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
</code></pre>
<p>注意 这里j<strong>必须要倒叙</strong><br>
从递推式来看是要正序 但是如果正序的话相当于dp[i][j] = dp[i][j-1] 错误<br>
倒叙时更新dp[j]用到的dp[j-1]实际上是上一轮更新的dp[i+1][j-1]</p>
<h2 id="manacher法">Manacher法</h2>
<p><a href="https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zhong-xin-kuo-san-dong-tai-gui-hua-by-liweiwei1419/">Manacher算法</a>是专门用于寻找字符串中的最长回文子串的算法<br>
步骤</p>
<ol>
<li>加入分隔符（加入分隔符不会影响字符串的回文性）</li>
<li>根据情况计算p数组（记录回文半径）</li>
</ol>
<p>id代表当前p数组值最大的位置<br>
mx=id+p[i] 代表当前最大回文子串所到的位置</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">Solution</span> <span class="token punctuation">{</span>

    <span class="token comment">/**
     * 创建分隔符分割的字符串
     *
     * @param s      原始字符串
     * @param divide 分隔字符
     * @return 使用分隔字符处理以后得到的字符串
     */</span>
    <span class="token keyword">private</span> String <span class="token function">generateSDivided</span><span class="token punctuation">(</span>String s<span class="token punctuation">,</span> <span class="token keyword">char</span> divide<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">int</span> len <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>len <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token string">""</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>s<span class="token punctuation">.</span><span class="token function">indexOf</span><span class="token punctuation">(</span>divide<span class="token punctuation">)</span> <span class="token operator">!=</span> <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">IllegalArgumentException</span><span class="token punctuation">(</span><span class="token string">"参数错误，您传递的分割字符，在输入字符串中存在！"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        StringBuilder sBuilder <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">StringBuilder</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        sBuilder<span class="token punctuation">.</span><span class="token function">append</span><span class="token punctuation">(</span>divide<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> len<span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            sBuilder<span class="token punctuation">.</span><span class="token function">append</span><span class="token punctuation">(</span>s<span class="token punctuation">.</span><span class="token function">charAt</span><span class="token punctuation">(</span>i<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            sBuilder<span class="token punctuation">.</span><span class="token function">append</span><span class="token punctuation">(</span>divide<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> sBuilder<span class="token punctuation">.</span><span class="token function">toString</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>

    <span class="token keyword">public</span> String <span class="token function">longestPalindrome</span><span class="token punctuation">(</span>String s<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">int</span> len <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>len <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token string">""</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        String sDivided <span class="token operator">=</span> <span class="token function">generateSDivided</span><span class="token punctuation">(</span>s<span class="token punctuation">,</span> <span class="token string">'#'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">int</span> slen <span class="token operator">=</span> sDivided<span class="token punctuation">.</span><span class="token function">length</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> p <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">int</span><span class="token punctuation">[</span>slen<span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token keyword">int</span> mx <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
        <span class="token comment">// id 是由 mx 决定的，所以不用初始化，只要声明就可以了</span>
        <span class="token keyword">int</span> id <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
        <span class="token keyword">int</span> longestPalindrome <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
        String longestPalindromeStr <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">substring</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> slen<span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">if</span> <span class="token punctuation">(</span>i <span class="token operator">&lt;</span> mx<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token comment">//先算在mx之内的字符串 之后再看可不可以扩展</span>
                <span class="token comment">//前一个就是p[j]比较小 这时p[i]=p[j]</span>
                <span class="token comment">//后一种就是p[j]比较大 这时i肯定可以匹配到mx处 至于之后有没有就不知道了 先把i到mx这部分算上</span>
                p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> Integer<span class="token punctuation">.</span><span class="token function">min</span><span class="token punctuation">(</span>p<span class="token punctuation">[</span><span class="token number">2</span> <span class="token operator">*</span> id <span class="token operator">-</span> i<span class="token punctuation">]</span><span class="token punctuation">,</span> mx <span class="token operator">-</span> i<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
                <span class="token comment">// 走到这里，只可能是因为 i = mx</span>
                <span class="token keyword">if</span> <span class="token punctuation">(</span>i <span class="token operator">&gt;</span> mx<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                    <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">IllegalArgumentException</span><span class="token punctuation">(</span><span class="token string">"程序出错！"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span>
                p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
            <span class="token comment">// 老老实实去匹配，看新的字符</span>
            <span class="token keyword">while</span> <span class="token punctuation">(</span>i <span class="token operator">-</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">&gt;=</span> <span class="token number">0</span> <span class="token operator">&amp;&amp;</span> i <span class="token operator">+</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">&lt;</span> slen <span class="token operator">&amp;&amp;</span> sDivided<span class="token punctuation">.</span><span class="token function">charAt</span><span class="token punctuation">(</span>i <span class="token operator">-</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">==</span> sDivided<span class="token punctuation">.</span><span class="token function">charAt</span><span class="token punctuation">(</span>i <span class="token operator">+</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                p<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token operator">++</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
            <span class="token comment">//更新mx和id</span>
            <span class="token keyword">if</span> <span class="token punctuation">(</span>i <span class="token operator">+</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">&gt;</span> mx<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                mx <span class="token operator">=</span> i <span class="token operator">+</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">;</span>
                id <span class="token operator">=</span> i<span class="token punctuation">;</span>
            <span class="token punctuation">}</span>

            <span class="token keyword">if</span> <span class="token punctuation">(</span>p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token number">1</span> <span class="token operator">&gt;</span> longestPalindrome<span class="token punctuation">)</span> <span class="token punctuation">{</span>
                longestPalindrome <span class="token operator">=</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">;</span>
                longestPalindromeStr <span class="token operator">=</span> sDivided<span class="token punctuation">.</span><span class="token function">substring</span><span class="token punctuation">(</span>i <span class="token operator">-</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">,</span> i <span class="token operator">+</span> p<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">replace</span><span class="token punctuation">(</span><span class="token string">"#"</span><span class="token punctuation">,</span> <span class="token string">""</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> longestPalindromeStr<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>这种做法就是专门用于解决最长回文子串的 时间复杂度是O(n)</p>

