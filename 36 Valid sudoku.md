---


---

<blockquote>
<p>Determine if a 9x9 Sudoku board is valid. Only the filled cells need<br>
to be validated according to the following rules:</p>
<ol>
<li>Each row must contain the digits 1-9 without repetition.</li>
<li>Each column must contain the digits 1-9 without repetition.</li>
<li>Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.</li>
</ol>
<p><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" alt="enter image descriptionhere"></p>
<p><strong>Note:</strong></p>
<ol>
<li><strong>A Sudoku board (partially filled) could be valid but is not necessarily solvable.</strong></li>
<li>Only the filled cells need to be validated according to the mentioned rules.</li>
<li>The given board contain only digits 1-9 and the character ‘.’.</li>
<li>The given board size is always 9x9.</li>
</ol>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/valid-sudoku/">题目</a></p>
<h2 id="一次遍历">一次遍历</h2>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">isValidSudoku</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> board<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token triple-quoted-string string">"""
        :type board: List[List[str]]
        :rtype: bool
        """</span>
        <span class="token comment"># init data</span>
        rows <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">{</span><span class="token punctuation">}</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
        columns <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">{</span><span class="token punctuation">}</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
        boxes <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">{</span><span class="token punctuation">}</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>

        <span class="token comment"># validate a board</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                num <span class="token operator">=</span> board<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span>
                <span class="token keyword">if</span> num <span class="token operator">!=</span> <span class="token string">'.'</span><span class="token punctuation">:</span>
                    num <span class="token operator">=</span> <span class="token builtin">int</span><span class="token punctuation">(</span>num<span class="token punctuation">)</span>
                    box_index <span class="token operator">=</span> <span class="token punctuation">(</span>i <span class="token operator">//</span> <span class="token number">3</span> <span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token number">3</span> <span class="token operator">+</span> j <span class="token operator">//</span> <span class="token number">3</span>
                    
                    <span class="token comment"># keep the current cell value</span>
                    rows<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> rows<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">.</span>get<span class="token punctuation">(</span>num<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span>
                    columns<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> columns<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">.</span>get<span class="token punctuation">(</span>num<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span>
                    boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">]</span><span class="token punctuation">.</span>get<span class="token punctuation">(</span>num<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span>
                    
                    <span class="token comment"># check if this value has been already seen before</span>
                    <span class="token keyword">if</span> rows<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">&gt;</span> <span class="token number">1</span> <span class="token operator">or</span> columns<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">&gt;</span> <span class="token number">1</span> <span class="token operator">or</span> boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">&gt;</span> <span class="token number">1</span><span class="token punctuation">:</span>
                        <span class="token keyword">return</span> <span class="token boolean">False</span>         
        <span class="token keyword">return</span> <span class="token boolean">True</span>
</code></pre>
<p>rows[i][num]记录第i行num出现的次数<br>
get(num,0)返回num出现的次数<br>
这里也可以用set()存储 和字典一样 它的查找速率也是O(1)</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">isValidSudoku</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> board<span class="token punctuation">:</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">str</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token builtin">bool</span><span class="token punctuation">:</span>
        matrix_line <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token builtin">set</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
        matrix_column <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token builtin">set</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
        matrix_area <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token builtin">set</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">]</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                item <span class="token operator">=</span> board<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span>
                pos <span class="token operator">=</span> <span class="token punctuation">(</span>i<span class="token operator">//</span><span class="token number">3</span><span class="token punctuation">)</span><span class="token operator">*</span><span class="token number">3</span> <span class="token operator">+</span> j <span class="token operator">//</span><span class="token number">3</span><span class="token comment">#获得块编号</span>
                <span class="token keyword">if</span> item <span class="token operator">!=</span> <span class="token string">'.'</span><span class="token punctuation">:</span>
                    <span class="token keyword">if</span> item <span class="token operator">not</span> <span class="token keyword">in</span> matrix_line<span class="token punctuation">[</span>i<span class="token punctuation">]</span> <span class="token operator">and</span> item <span class="token operator">not</span> <span class="token keyword">in</span> matrix_column<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">and</span> item <span class="token operator">not</span> <span class="token keyword">in</span> matrix_area<span class="token punctuation">[</span>pos<span class="token punctuation">]</span><span class="token punctuation">:</span>
                        matrix_line<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">.</span>add<span class="token punctuation">(</span>item<span class="token punctuation">)</span>
                        matrix_column<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">.</span>add<span class="token punctuation">(</span>item<span class="token punctuation">)</span>
                        matrix_area<span class="token punctuation">[</span>pos<span class="token punctuation">]</span><span class="token punctuation">.</span>add<span class="token punctuation">(</span>item<span class="token punctuation">)</span>
                    <span class="token keyword">else</span><span class="token punctuation">:</span>
                        <span class="token keyword">return</span> <span class="token boolean">False</span>
        <span class="token keyword">return</span> <span class="token boolean">True</span>
</code></pre>

