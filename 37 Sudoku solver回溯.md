---


---

<blockquote>
<p>Write a program to solve a Sudoku puzzle by filling the empty cells.<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" alt="enter image description here"><br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png" alt="enter image description here"></p>
</blockquote>
<p><a href="https://leetcode-cn.com/problems/sudoku-solver/">题目</a></p>
<h2 id="回溯法（一定掌握）">回溯法（一定掌握）</h2>
<blockquote>
<p>从左上角往右下角挨个填写1-9 不行的话会remove这个元素</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">from</span> collections <span class="token keyword">import</span> defaultdict
<span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">solveSudoku</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> board<span class="token punctuation">)</span><span class="token punctuation">:</span>
        <span class="token triple-quoted-string string">"""
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """</span>
        <span class="token keyword">def</span> <span class="token function">could_place</span><span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token triple-quoted-string string">"""
            Check if one could place a number d in (row, col) cell
            """</span>
            <span class="token keyword">return</span> <span class="token operator">not</span> <span class="token punctuation">(</span>d <span class="token keyword">in</span> rows<span class="token punctuation">[</span>row<span class="token punctuation">]</span> <span class="token operator">or</span> d <span class="token keyword">in</span> columns<span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">or</span> \
                    d <span class="token keyword">in</span> boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
        
        <span class="token keyword">def</span> <span class="token function">place_number</span><span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token triple-quoted-string string">"""
            Place a number d in (row, col) cell
            """</span>
            rows<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span> <span class="token operator">+=</span> <span class="token number">1</span>
            columns<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span> <span class="token operator">+=</span> <span class="token number">1</span>
            boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span> <span class="token operator">+=</span> <span class="token number">1</span>
            board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token builtin">str</span><span class="token punctuation">(</span>d<span class="token punctuation">)</span>
            
        <span class="token keyword">def</span> <span class="token function">remove_number</span><span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token triple-quoted-string string">"""
            Remove a number which didn't lead 
            to a solution
            """</span>
            <span class="token keyword">del</span> rows<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span>
            <span class="token keyword">del</span> columns<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span>
            <span class="token keyword">del</span> boxes<span class="token punctuation">[</span>box_index<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">]</span><span class="token punctuation">[</span>d<span class="token punctuation">]</span>
            board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">'.'</span>    
            
        <span class="token keyword">def</span> <span class="token function">place_next_numbers</span><span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">:</span><span class="token comment">#进入下一个数的backtrack</span>
            <span class="token triple-quoted-string string">"""
            Call backtrack function in recursion
            to continue to place numbers
            till the moment we have a solution
            """</span>
            <span class="token comment"># if we're in the last cell</span>
            <span class="token comment"># that means we have the solution</span>
            <span class="token keyword">if</span> col <span class="token operator">==</span> N <span class="token operator">-</span> <span class="token number">1</span> <span class="token operator">and</span> row <span class="token operator">==</span> N <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">:</span>
                <span class="token keyword">nonlocal</span> sudoku_solved
                sudoku_solved <span class="token operator">=</span> <span class="token boolean">True</span>
            <span class="token comment">#if not yet    </span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                <span class="token comment"># if we're in the end of the row</span>
                <span class="token comment"># go to the next row</span>
                <span class="token keyword">if</span> col <span class="token operator">==</span> N <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">:</span>
                    backtrack<span class="token punctuation">(</span>row <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span>
                <span class="token comment"># go to the next column</span>
                <span class="token keyword">else</span><span class="token punctuation">:</span>
                    backtrack<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span>
                
                
        <span class="token keyword">def</span> <span class="token function">backtrack</span><span class="token punctuation">(</span>row <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span> col <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token triple-quoted-string string">"""
            Backtracking
            """</span>
            <span class="token comment"># if the cell is empty</span>
            <span class="token keyword">if</span> board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">==</span> <span class="token string">'.'</span><span class="token punctuation">:</span>
                <span class="token comment"># iterate over all numbers from 1 to 9</span>
                <span class="token keyword">for</span> d <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">10</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    <span class="token keyword">if</span> could_place<span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span><span class="token punctuation">:</span>
                        place_number<span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span>
                        place_next_numbers<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span>
                        <span class="token comment"># if sudoku is solved, there is no need to backtrack</span>
                        <span class="token comment"># since the single unique solution is promised</span>
                        <span class="token keyword">if</span> <span class="token operator">not</span> sudoku_solved<span class="token punctuation">:</span>
                            remove_number<span class="token punctuation">(</span>d<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col<span class="token punctuation">)</span>
            <span class="token keyword">else</span><span class="token punctuation">:</span>
                place_next_numbers<span class="token punctuation">(</span>row<span class="token punctuation">,</span> col<span class="token punctuation">)</span>
                    
        <span class="token comment"># box size</span>
        n <span class="token operator">=</span> <span class="token number">3</span>
        <span class="token comment"># row size</span>
        N <span class="token operator">=</span> n <span class="token operator">*</span> n
        <span class="token comment"># lambda function to compute box index</span>
        box_index <span class="token operator">=</span> <span class="token keyword">lambda</span> row<span class="token punctuation">,</span> col<span class="token punctuation">:</span> <span class="token punctuation">(</span>row <span class="token operator">//</span> n <span class="token punctuation">)</span> <span class="token operator">*</span> n <span class="token operator">+</span> col <span class="token operator">//</span> n
        
        <span class="token comment"># init rows, columns and boxes</span>
        rows <span class="token operator">=</span> <span class="token punctuation">[</span>defaultdict<span class="token punctuation">(</span><span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">]</span>
        columns <span class="token operator">=</span> <span class="token punctuation">[</span>defaultdict<span class="token punctuation">(</span><span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">]</span>
        boxes <span class="token operator">=</span> <span class="token punctuation">[</span>defaultdict<span class="token punctuation">(</span><span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">]</span>
        <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>N<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> board<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">!=</span> <span class="token string">'.'</span><span class="token punctuation">:</span> 
                    d <span class="token operator">=</span> <span class="token builtin">int</span><span class="token punctuation">(</span>board<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">)</span>
                    place_number<span class="token punctuation">(</span>d<span class="token punctuation">,</span> i<span class="token punctuation">,</span> j<span class="token punctuation">)</span>
        
        sudoku_solved <span class="token operator">=</span> <span class="token boolean">False</span>
        backtrack<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">class</span> <span class="token class-name">Solution</span> <span class="token punctuation">{</span>
    <span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">solveSudoku</span><span class="token punctuation">(</span><span class="token keyword">char</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span> board<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token comment">// 三个布尔数组 表明 行, 列, 还有 3*3 的方格的数字是否被使用过</span>
        <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span> rowUsed <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">boolean</span><span class="token punctuation">[</span><span class="token number">9</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token number">10</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span> colUsed <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">boolean</span><span class="token punctuation">[</span><span class="token number">9</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token number">10</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span> boxUsed <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">boolean</span><span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token number">10</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        <span class="token comment">// 初始化</span>
        <span class="token keyword">for</span><span class="token punctuation">(</span><span class="token keyword">int</span> row <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> row <span class="token operator">&lt;</span> board<span class="token punctuation">.</span>length<span class="token punctuation">;</span> row<span class="token operator">++</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
            <span class="token keyword">for</span><span class="token punctuation">(</span><span class="token keyword">int</span> col <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> col <span class="token operator">&lt;</span> board<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>length<span class="token punctuation">;</span> col<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
                <span class="token keyword">int</span> num <span class="token operator">=</span> board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">-</span> <span class="token string">'0'</span><span class="token punctuation">;</span>
                <span class="token keyword">if</span><span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">&lt;=</span> num <span class="token operator">&amp;&amp;</span> num <span class="token operator">&lt;=</span> <span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
                    rowUsed<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    colUsed<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    boxUsed<span class="token punctuation">[</span>row<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
        <span class="token comment">// 递归尝试填充数组 </span>
        <span class="token function">recusiveSolveSudoku</span><span class="token punctuation">(</span>board<span class="token punctuation">,</span> rowUsed<span class="token punctuation">,</span> colUsed<span class="token punctuation">,</span> boxUsed<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">private</span> <span class="token keyword">boolean</span> <span class="token function">recusiveSolveSudoku</span><span class="token punctuation">(</span><span class="token keyword">char</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span>board<span class="token punctuation">,</span> <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span>rowUsed<span class="token punctuation">,</span> <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span>colUsed<span class="token punctuation">,</span> <span class="token keyword">boolean</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token punctuation">]</span>boxUsed<span class="token punctuation">,</span> <span class="token keyword">int</span> row<span class="token punctuation">,</span> <span class="token keyword">int</span> col<span class="token punctuation">)</span><span class="token punctuation">{</span>
        <span class="token comment">// 边界校验, 如果已经填充完成, 返回true, 表示一切结束</span>
        <span class="token keyword">if</span><span class="token punctuation">(</span>col <span class="token operator">==</span> board<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>length<span class="token punctuation">)</span><span class="token punctuation">{</span>
            col <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
            row<span class="token operator">++</span><span class="token punctuation">;</span>
            <span class="token keyword">if</span><span class="token punctuation">(</span>row <span class="token operator">==</span> board<span class="token punctuation">.</span>length<span class="token punctuation">)</span><span class="token punctuation">{</span>
                <span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span>
        <span class="token comment">// 是空则尝试填充, 否则跳过继续尝试填充下一个位置</span>
        <span class="token keyword">if</span><span class="token punctuation">(</span>board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">==</span> <span class="token string">'.'</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token comment">// 尝试填充1~9</span>
            <span class="token keyword">for</span><span class="token punctuation">(</span><span class="token keyword">int</span> num <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span> num <span class="token operator">&lt;=</span> <span class="token number">9</span><span class="token punctuation">;</span> num<span class="token operator">++</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
                <span class="token keyword">boolean</span> canUsed <span class="token operator">=</span> <span class="token operator">!</span><span class="token punctuation">(</span>rowUsed<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">||</span> colUsed<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">||</span> boxUsed<span class="token punctuation">[</span>row<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token keyword">if</span><span class="token punctuation">(</span>canUsed<span class="token punctuation">)</span><span class="token punctuation">{</span>
                    rowUsed<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    colUsed<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    boxUsed<span class="token punctuation">[</span>row<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    
                    board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token keyword">char</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token string">'0'</span> <span class="token operator">+</span> num<span class="token punctuation">)</span><span class="token punctuation">;</span>
                    <span class="token keyword">if</span><span class="token punctuation">(</span><span class="token function">recusiveSolveSudoku</span><span class="token punctuation">(</span>board<span class="token punctuation">,</span> rowUsed<span class="token punctuation">,</span> colUsed<span class="token punctuation">,</span> boxUsed<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">{</span>
                        <span class="token keyword">return</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
                    <span class="token punctuation">}</span>
                    board<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">'.'</span><span class="token punctuation">;</span>
                    
                    rowUsed<span class="token punctuation">[</span>row<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
                    colUsed<span class="token punctuation">[</span>col<span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
                    boxUsed<span class="token punctuation">[</span>row<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>col<span class="token operator">/</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">[</span>num<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
            <span class="token keyword">return</span> <span class="token function">recusiveSolveSudoku</span><span class="token punctuation">(</span>board<span class="token punctuation">,</span> rowUsed<span class="token punctuation">,</span> colUsed<span class="token punctuation">,</span> boxUsed<span class="token punctuation">,</span> row<span class="token punctuation">,</span> col <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token punctuation">}</span>
        <span class="token keyword">return</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>

