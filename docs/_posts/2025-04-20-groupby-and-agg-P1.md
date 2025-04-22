---
layout: post
title: "Pandas: groupby and agg"
date: 2025-04-20
categories: [blog]
---
For some, `groupby()` and `agg()` can be a bit confusing in the beginning. The syntax may look strange, especially when they are chained together 
as `groupby().agg()`. But learning how to use them properly is very important. These are powerful functions in pandas that help you group data 
and then apply functions like `sum()`, `mean()`, or even custom functions to each group. Using this we can create new summarized DataFrames. 

The `agg()` function is commonly used alongside `groupby()` in pandas. When you group data using `groupby()`, you often need to perform one or more 
operations on each group. This is where `agg()` becomes useful. It allows you to compute summary statistics such as `totals`, `averages`, `counts`, or 
even apply `multiple functions` at the same time, making it a powerful tool for data analysis.

Let's discuss this concept in more detail using an example. I’ve created a dataset that tracks my monthly expenses from January 1, 2025, to April 15, 2025. 
Go through the Jupyter Notebook linked below for a step by step explanation.

  
  
  
  
  
  
  
  
  
  
  
  
  
  
</style>
<!-- End of mermaid configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">
<main><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs" id="cell-id=abf3ad6a-45b6-4da3-a001-73c69d169548">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="kn">import</span><span class="w"> </span><span class="nn">pandas</span><span class="w"> </span><span class="k">as</span><span class="w"> </span><span class="nn">pd</span>
</pre></div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=a38419a7-e6dc-4c00-b0eb-38a4743f424e">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">expenses</span><span class="o">=</span><span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">'realistic_expenses.csv'</span><span class="p">)</span>
<span class="n">expenses</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[8]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>date</th>
<th>category</th>
<th>payment_mode</th>
<th>amount</th>
<th>merchant</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>2025-01-01</td>
<td>groceries</td>
<td>upi</td>
<td>452</td>
<td>local shop</td>
</tr>
<tr>
<th>1</th>
<td>2025-01-01</td>
<td>subscriptions</td>
<td>credit card</td>
<td>199</td>
<td>netflix</td>
</tr>
<tr>
<th>2</th>
<td>2025-01-01</td>
<td>food</td>
<td>upi</td>
<td>497</td>
<td>swiggy</td>
</tr>
<tr>
<th>3</th>
<td>2025-01-02</td>
<td>subscriptions</td>
<td>upi</td>
<td>299</td>
<td>amazon prime</td>
</tr>
<tr>
<th>4</th>
<td>2025-01-02</td>
<td>groceries</td>
<td>credit card</td>
<td>699</td>
<td>big bazaar</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=dba6745f-187b-4644-af66-0861aa91fa60">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">expenses</span><span class="o">.</span><span class="n">info</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child">
<div class="jp-OutputPrompt jp-OutputArea-prompt"></div>
<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain" tabindex="0">
<pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 169 entries, 0 to 168
Data columns (total 5 columns):
 #   Column        Non-Null Count  Dtype 
---  ------        --------------  ----- 
 0   date          169 non-null    object
 1   category      169 non-null    object
 2   payment_mode  169 non-null    object
 3   amount        169 non-null    int64 
 4   merchant      169 non-null    object
dtypes: int64(1), object(4)
memory usage: 6.7+ KB
</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=9bb976a5-2e9b-4ae4-8d1c-da8c208292bb">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">expenses</span><span class="o">.</span><span class="n">shape</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[10]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>(169, 5)</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs" id="cell-id=3e270862-2d81-460f-a1cd-2bfbeef40737">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Structuring</span>
<span class="c1">#date as datetime</span>
<span class="n">expenses</span><span class="p">[</span><span class="s1">'date'</span><span class="p">]</span><span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">to_datetime</span><span class="p">(</span><span class="n">expenses</span><span class="p">[</span><span class="s1">'date'</span><span class="p">],</span><span class="nb">format</span><span class="o">=</span><span class="s1">'%Y-%m-</span><span class="si">%d</span><span class="s1">'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=468f273f-b2fe-4f0e-b1b8-f08b5bf4adce">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>Using <code>value_counts()</code> let's try to find the number of payments in each category.
Syntax:  <code>df['&lt;column name&gt;'].value_counts()</code></p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=545d7c40-6941-4890-8bf8-e116bbe43095">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">df</span><span class="p">[</span><span class="s1">'category'</span><span class="p">]</span><span class="o">.</span><span class="n">value_counts</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[15]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>category
groceries        42
food             36
travel           34
entertainment    25
utility          16
investment       10
subscriptions     6
Name: count, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=e0c455b4-e380-429f-9a9d-42b13512059b">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The table above shows the number of transactions made in each category. By default, <code>value_counts()</code> sorts the values in descending order.</p>
<p>However, the capability of <code>value_counts()</code> is limited to simply counting occurrences. It cannot apply functions like <code>sum()</code> or <code>mean()</code>, and it only works on a single column at a time.</p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=aba7b7b1-aec7-42df-90ba-1ec0a3d20855">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>In contrast, <code>groupby()</code> can handle multiple columns and allows you to apply a wide range of functions. This makes it much more powerful and flexible for performing complex data analysis. Let’s try to understand how <code>groupby()</code>works with a simple example. We’ll start by finding the total amount spent in each category.
Syntax: <code>df.groupby([&lt;columns seperated by coma &gt;]).&lt;function&gt;</code></p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=24419d83-34b5-4bf3-9df0-df8da5a91f9a">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [19]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Total expenditure per category</span>
<span class="n">expenses</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'category'</span><span class="p">])[</span><span class="s1">'amount'</span><span class="p">]</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[19]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>category
entertainment     8921
food              9210
groceries        19657
investment       34831
subscriptions     1876
travel           22294
utility           8398
Name: amount, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=3f2205f4-dbd6-4cc9-9ee7-cc81de3cbccb">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [23]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="c1">#Example with multiple columns </span>
<span class="c1">#Find total expenditure on each category and payment menthod</span>
<span class="n">expenses</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'category'</span><span class="p">,</span><span class="s1">'payment_mode'</span><span class="p">])[</span><span class="s1">'amount'</span><span class="p">]</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[23]:</div>
<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain" tabindex="0">
<pre>category       payment_mode
entertainment  cash             2213
               credit card       102
               debit card       2610
               upi              3996
food           cash             1790
               credit card      1600
               debit card       1782
               upi              4038
groceries      cash             4484
               credit card      3919
               debit card       3247
               upi              8007
investment     cash             6736
               credit card      7095
               debit card      14000
               upi              7000
subscriptions  credit card      1577
               upi               299
travel         cash             3084
               credit card      9880
               debit card       7365
               upi              1965
utility        cash             2057
               credit card      3684
               debit card        420
               upi              2237
Name: amount, dtype: int64</pre>
</div>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=90268380-0627-429d-be4f-498a385e5a75">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p>The <code>groupby()</code> is limited to use a single function. Now if you want to get both <code>sum()</code> and <code>mean()</code> in single table, use <code>agg()</code> along with <code>groupby()</code></p>
</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell" id="cell-id=4f24c2ca-3578-4dfa-b052-520cc345e5e4">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput" data-mime-type="text/markdown">
<p><code>agg()</code> takes input in the form of a dictionary : <code>df[].groupby().agg{&lt;column_name_1&gt;:&lt;function_1()&gt; , &lt;column_name_2&gt;:&lt;function_2()&gt; , &lt;column_name_2&gt;:&lt;function_2()&gt;)</code>.
Let's find out total expenditure in each category along with mean expenditure.</p>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=da3e9fd7-7014-4901-88b4-f0a31550e53c">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [24]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">expenses</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'category'</span><span class="p">])[</span><span class="s1">'amount'</span><span class="p">]</span><span class="o">.</span><span class="n">agg</span><span class="p">([</span><span class="s1">'sum'</span><span class="p">,</span> <span class="s1">'mean'</span><span class="p">])</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[24]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th>sum</th>
<th>mean</th>
</tr>
<tr>
<th>category</th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th>entertainment</th>
<td>8921</td>
<td>356.840000</td>
</tr>
<tr>
<th>food</th>
<td>9210</td>
<td>255.833333</td>
</tr>
<tr>
<th>groceries</th>
<td>19657</td>
<td>468.023810</td>
</tr>
<tr>
<th>investment</th>
<td>34831</td>
<td>3483.100000</td>
</tr>
<tr>
<th>subscriptions</th>
<td>1876</td>
<td>312.666667</td>
</tr>
<tr>
<th>travel</th>
<td>22294</td>
<td>655.705882</td>
</tr>
<tr>
<th>utility</th>
<td>8398</td>
<td>524.875000</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell" id="cell-id=084ab0a4-2020-4509-a14e-0e375b29a69f">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [32]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span><span class="n">expenses</span><span class="o">.</span><span class="n">groupby</span><span class="p">([</span><span class="s1">'category'</span><span class="p">,</span><span class="s1">'merchant'</span><span class="p">])[</span><span class="s1">'amount'</span><span class="p">]</span><span class="o">.</span><span class="n">agg</span><span class="p">(</span><span class="n">min_spent</span><span class="o">=</span><span class="s1">'min'</span><span class="p">,</span> <span class="n">avg_spent</span><span class="o">=</span><span class="s1">'mean'</span><span class="p">,</span> <span class="n">total_spent</span><span class="o">=</span><span class="s1">'sum'</span><span class="p">)</span>
</pre></div>
</div>
</div>
</div>
</div>
<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>
<div class="jp-OutputArea jp-Cell-outputArea">
<div class="jp-OutputArea-child jp-OutputArea-executeResult">
<div class="jp-OutputPrompt jp-OutputArea-prompt">Out[32]:</div>
<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html" tabindex="0">
<div>
<style scoped="">
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
<thead>
<tr style="text-align: right;">
<th></th>
<th></th>
<th>min_spent</th>
<th>avg_spent</th>
<th>total_spent</th>
</tr>
<tr>
<th>category</th>
<th>merchant</th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<th rowspan="6" valign="top">entertainment</th>
<th>inox</th>
<td>590</td>
<td>590.000000</td>
<td>590</td>
</tr>
<tr>
<th>local restaurant</th>
<td>278</td>
<td>278.000000</td>
<td>278</td>
</tr>
<tr>
<th>netflix</th>
<td>138</td>
<td>361.444444</td>
<td>3253</td>
</tr>
<tr>
<th>pvr</th>
<td>137</td>
<td>346.875000</td>
<td>2775</td>
</tr>
<tr>
<th>youtube premium</th>
<td>102</td>
<td>306.600000</td>
<td>1533</td>
</tr>
<tr>
<th>youtube subscription</th>
<td>492</td>
<td>492.000000</td>
<td>492</td>
</tr>
<tr>
<th rowspan="5" valign="top">food</th>
<th>local restaurant</th>
<td>103</td>
<td>237.000000</td>
<td>2133</td>
</tr>
<tr>
<th>local shop</th>
<td>95</td>
<td>118.500000</td>
<td>237</td>
</tr>
<tr>
<th>pvr</th>
<td>100</td>
<td>100.000000</td>
<td>100</td>
</tr>
<tr>
<th>swiggy</th>
<td>132</td>
<td>310.181818</td>
<td>3412</td>
</tr>
<tr>
<th>zomato</th>
<td>105</td>
<td>256.000000</td>
<td>3328</td>
</tr>
<tr>
<th rowspan="3" valign="top">groceries</th>
<th>big bazaar</th>
<td>225</td>
<td>513.000000</td>
<td>7182</td>
</tr>
<tr>
<th>local shop</th>
<td>18</td>
<td>375.105263</td>
<td>7127</td>
</tr>
<tr>
<th>reliance fresh</th>
<td>421</td>
<td>594.222222</td>
<td>5348</td>
</tr>
<tr>
<th rowspan="3" valign="top">investment</th>
<th>groww</th>
<td>2257</td>
<td>3128.500000</td>
<td>6257</td>
</tr>
<tr>
<th>nippon india</th>
<td>1000</td>
<td>1500.000000</td>
<td>3000</td>
</tr>
<tr>
<th>zerodha</th>
<td>2643</td>
<td>4262.333333</td>
<td>25574</td>
</tr>
<tr>
<th rowspan="4" valign="top">subscriptions</th>
<th>amazon prime</th>
<td>299</td>
<td>299.000000</td>
<td>299</td>
</tr>
<tr>
<th>google one</th>
<td>130</td>
<td>130.000000</td>
<td>260</td>
</tr>
<tr>
<th>netflix</th>
<td>199</td>
<td>599.000000</td>
<td>1198</td>
</tr>
<tr>
<th>spotify</th>
<td>119</td>
<td>119.000000</td>
<td>119</td>
</tr>
<tr>
<th rowspan="3" valign="top">travel</th>
<th>indian railway</th>
<td>25</td>
<td>611.666667</td>
<td>7340</td>
</tr>
<tr>
<th>petrol</th>
<td>166</td>
<td>764.384615</td>
<td>9937</td>
</tr>
<tr>
<th>uber</th>
<td>319</td>
<td>557.444444</td>
<td>5017</td>
</tr>
<tr>
<th rowspan="6" valign="top">utility</th>
<th>amazon</th>
<td>322</td>
<td>322.000000</td>
<td>322</td>
</tr>
<tr>
<th>bsnl</th>
<td>261</td>
<td>567.666667</td>
<td>5109</td>
</tr>
<tr>
<th>kerala electricity board</th>
<td>293</td>
<td>360.500000</td>
<td>721</td>
</tr>
<tr>
<th>local shop</th>
<td>55</td>
<td>55.000000</td>
<td>55</td>
</tr>
<tr>
<th>petrol</th>
<td>420</td>
<td>420.000000</td>
<td>420</td>
</tr>
<tr>
<th>water authority</th>
<td>817</td>
<td>885.500000</td>
<td>1771</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs" id="cell-id=5a1639b7-b2a5-44c1-ae0b-8295c184c872">
<div class="jp-Cell-inputWrapper" tabindex="0">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In [ ]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
<div class="cm-editor cm-s-jupyter">
<div class="highlight hl-ipython3"><pre><span></span> 
</pre></div>
</div>
</div>
</div>
</div>
</div>
</main>
</body>
</html>
