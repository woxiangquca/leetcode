---


---

<blockquote>
<p>The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.<br>
<img src="https://assets.leetcode.com/uploads/2018/10/12/8-queens.png" alt="enter image description here"><br>
Given an integer <em>n</em>, return all distinct solutions to the <em>n</em>-queens puzzle.<br>
Each solution contains a distinct board configuration of the n-queens’ placement, where ‘Q’ and ‘.’ both indicate a queen and an empty space respectively.</p>
</blockquote>
<h2 id="回溯剪枝">回溯+剪枝</h2>
<blockquote>
<p>基础版的思路跟全排列一模一样</p>
</blockquote>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">class</span> <span class="token class-name">Solution</span><span class="token punctuation">:</span>
    <span class="token keyword">def</span> <span class="token function">solveNQueens</span><span class="token punctuation">(</span>self<span class="token punctuation">,</span> n<span class="token punctuation">:</span> <span class="token builtin">int</span><span class="token punctuation">)</span> <span class="token operator">-</span><span class="token operator">&gt;</span> List<span class="token punctuation">[</span>List<span class="token punctuation">[</span><span class="token builtin">str</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">:</span>
        
        <span class="token keyword">def</span> <span class="token function">one_dim2two_dim</span><span class="token punctuation">(</span>res<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>res<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">for</span> j <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>res<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                    col <span class="token operator">=</span> res<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">%</span> n
                    res<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">"."</span><span class="token operator">*</span>col <span class="token operator">+</span> <span class="token string">"Q"</span> <span class="token operator">+</span> <span class="token string">"."</span><span class="token operator">*</span><span class="token punctuation">(</span>n<span class="token operator">-</span>col<span class="token number">-1</span><span class="token punctuation">)</span>
            <span class="token keyword">return</span> res
        
        <span class="token keyword">def</span> <span class="token function">valid</span><span class="token punctuation">(</span>index<span class="token punctuation">,</span>path<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
                ele <span class="token operator">=</span> path<span class="token punctuation">[</span>i<span class="token punctuation">]</span>
                row <span class="token operator">=</span> ele <span class="token operator">//</span> n
                col <span class="token operator">=</span> ele <span class="token operator">%</span> n
                <span class="token keyword">if</span> index <span class="token operator">%</span> n <span class="token operator">==</span> col <span class="token operator">or</span> <span class="token builtin">abs</span><span class="token punctuation">(</span>index <span class="token operator">%</span> n <span class="token operator">-</span> col<span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token builtin">abs</span><span class="token punctuation">(</span>index <span class="token operator">//</span> n <span class="token operator">-</span> row<span class="token punctuation">)</span><span class="token punctuation">:</span> <span class="token keyword">return</span> <span class="token boolean">False</span>
            <span class="token keyword">return</span> <span class="token boolean">True</span>
        
        <span class="token keyword">def</span> <span class="token function">dfs</span><span class="token punctuation">(</span>path<span class="token punctuation">,</span>res<span class="token punctuation">,</span>row<span class="token punctuation">)</span><span class="token punctuation">:</span>
            <span class="token keyword">if</span> <span class="token builtin">len</span><span class="token punctuation">(</span>path<span class="token punctuation">)</span> <span class="token operator">==</span> n<span class="token punctuation">:</span>   
                res<span class="token punctuation">.</span>append<span class="token punctuation">(</span>path<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
                <span class="token keyword">return</span> <span class="token boolean">True</span>
            
            <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>n<span class="token punctuation">)</span><span class="token punctuation">:</span>
                <span class="token keyword">if</span> valid<span class="token punctuation">(</span>row<span class="token operator">*</span>n<span class="token operator">+</span>i<span class="token punctuation">,</span>path<span class="token punctuation">)</span> <span class="token operator">and</span> dfs<span class="token punctuation">(</span>path<span class="token operator">+</span><span class="token punctuation">[</span>row<span class="token operator">*</span>n<span class="token operator">+</span>i<span class="token punctuation">]</span><span class="token punctuation">,</span>res<span class="token punctuation">,</span>row<span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">:</span> <span class="token keyword">break</span>
            
            <span class="token keyword">return</span> <span class="token boolean">False</span>
                
        path <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        res <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
        dfs<span class="token punctuation">(</span>path<span class="token punctuation">,</span>res<span class="token punctuation">,</span><span class="token number">0</span><span class="token punctuation">)</span>
        <span class="token keyword">return</span> one_dim2two_dim<span class="token punctuation">(</span>res<span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>这样很繁琐，主要存在一个问题：这样做每次检查valid都需要O(n)的时间，因为需要遍历path看他是否会攻击到以前的每一个皇后。</p>
</blockquote>
<blockquote>
<p>我们可以在放置前面皇后的时候就用一些变量列出所有不允许的位置，在检查当前位置是否valid时就只用看这个位置是不是被禁止的位置即可。</p>
</blockquote>
<blockquote>
<p>对于所有的主对角线有 行号 + 列号 = 常数，对于所有的次对角线有 行号 - 列号 = 常数.<br>
可以让我们标记已经在攻击范围下的对角线并且检查一个方格 (行号, 列号) 是否处在攻击位置。<br>
用hills[i]第i条主对角线，dale[i]表示第j条次对角线，在hills[i]上的坐标满足x+y=i,在dale[i]上的坐标满足2n-(x-y)=i-1<img src="https://pic.leetcode-cn.com/332b878ebcd261a71f5f85cb4e23685d42b37685112f562e2844079748e63cd0-51_diagonals.png" alt="enter image description here"></p>
</blockquote>
<p>注意，如果这样写就必须设置placeQueen函数，置相应的行列对角线的数组值为1</p>
<p>N-Queens II 只用记录解的个数不用记录中间每一层的结果，直接对hill和dale数组进行修改即可（记录不可能的位置），所以位掩码比较简洁。</p>
<h2 id="bitmap位掩码">bitmap位掩码</h2>
<blockquote>
<p>用整数表示布尔数组和放置位置,详见<a href="https://leetcode-cn.com/problems/n-queens-ii/solution/dfs-wei-yun-suan-jian-zhi-by-makeex/">这里</a><br>
col表示由于之前行x位置放值导致下面行x位置无法放置的位置，ld表示由于之前行x位置放值导致下面行对角线位置无法放置的位置，rd表示由于之前行x位置放值导致下面行对焦位置无法放置的位置。这三个变量都是叠加而得的</p>
</blockquote>
<pre class=" language-cpp"><code class="prism  language-cpp"><span class="token keyword">class</span> <span class="token class-name">Solution</span> <span class="token punctuation">{</span>
<span class="token keyword">public</span><span class="token operator">:</span>
    <span class="token keyword">int</span> <span class="token function">totalNQueens</span><span class="token punctuation">(</span><span class="token keyword">int</span> n<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token function">dfs</span><span class="token punctuation">(</span>n<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        
        <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token operator">-</span><span class="token operator">&gt;</span>res<span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">void</span> <span class="token function">dfs</span><span class="token punctuation">(</span><span class="token keyword">int</span> n<span class="token punctuation">,</span> <span class="token keyword">int</span> row<span class="token punctuation">,</span> <span class="token keyword">int</span> col<span class="token punctuation">,</span> <span class="token keyword">int</span> ld<span class="token punctuation">,</span> <span class="token keyword">int</span> rd<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">if</span> <span class="token punctuation">(</span>row <span class="token operator">&gt;=</span> n<span class="token punctuation">)</span> <span class="token punctuation">{</span> res<span class="token operator">++</span><span class="token punctuation">;</span> <span class="token keyword">return</span><span class="token punctuation">;</span> <span class="token punctuation">}</span>#如果要记录结果，可以用一个整数，记录每一层结果，每次需要记录时就左移N位，然后位运算得出过程
        
        <span class="token comment">// 将所有能放置 Q 的位置由 0 变成 1，以便进行后续的位遍历</span>
        <span class="token keyword">int</span> bits <span class="token operator">=</span> <span class="token operator">~</span><span class="token punctuation">(</span>col <span class="token operator">|</span> ld <span class="token operator">|</span> rd<span class="token punctuation">)</span> <span class="token operator">&amp;</span> <span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">&lt;&lt;</span> n<span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">while</span> <span class="token punctuation">(</span>bits <span class="token operator">&gt;</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
            <span class="token keyword">int</span> pick <span class="token operator">=</span> bits <span class="token operator">&amp;</span> <span class="token operator">-</span>bits<span class="token punctuation">;</span> <span class="token comment">// 注: x &amp; -x</span>
            <span class="token function">dfs</span><span class="token punctuation">(</span>n<span class="token punctuation">,</span> row <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">,</span> col <span class="token operator">|</span> pick<span class="token punctuation">,</span> <span class="token punctuation">(</span>ld <span class="token operator">|</span> pick<span class="token punctuation">)</span> <span class="token operator">&lt;&lt;</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>rd <span class="token operator">|</span> pick<span class="token punctuation">)</span> <span class="token operator">&gt;&gt;</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            bits <span class="token operator">&amp;</span><span class="token operator">=</span> bits <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">;</span> <span class="token comment">// 注: x &amp; (x - 1)</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>

<span class="token keyword">private</span><span class="token operator">:</span>
    <span class="token keyword">int</span> res <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>明天任务：</p>
<ol>
<li>看数独题</li>
<li>看permutation位掩码</li>
</ol>

