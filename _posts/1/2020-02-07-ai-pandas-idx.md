---
title: Pandas Index
date: 2020-02-07 10:50:00 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Index"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-02-07T18:50:00+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Index" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T18:50:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Index" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T18:50:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Index" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-07T18:50:00+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><h1 id="_1">Series</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="n">pd</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="n">seaborn</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="n">np</span>

<span class="c1">#Series()
</span><span class="n">s</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">np</span><span class="p">.</span><span class="n">nan</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">8</span><span class="p">])</span>
<span class="n">s</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
</code></pre></div></div>

<h1 id="_2">date_ranges</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#date_ranges()
</span><span class="n">dates</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'20130101'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">6</span><span class="p">)</span>
<span class="n">dates</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
</code></pre></div></div>

<h1 id="_3">DataFrame</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#DataFrame()
</span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">6</span><span class="p">,</span> <span class="mi">4</span><span class="p">),</span> <span class="n">index</span><span class="o">=</span><span class="n">dates</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="nb">list</span><span class="p">(</span><span class="s">'ABCD'</span><span class="p">))</span>
<span class="n">df</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.854440</td>
      <td>-0.574851</td>
      <td>-0.356466</td>
      <td>-1.595153</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.403468</td>
      <td>1.190093</td>
      <td>-1.347149</td>
      <td>0.189084</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df2</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'A'</span><span class="p">:</span> <span class="mf">1.</span><span class="p">,</span>
<span class="s">'B'</span><span class="p">:</span> <span class="n">pd</span><span class="p">.</span><span class="n">Timestamp</span><span class="p">(</span><span class="s">'20130102'</span><span class="p">),</span>
<span class="s">'C'</span><span class="p">:</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">index</span><span class="o">=</span><span class="nb">list</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)),</span> <span class="n">dtype</span><span class="o">=</span><span class="s">'float32'</span><span class="p">),</span>
<span class="s">'D'</span><span class="p">:</span> <span class="n">np</span><span class="p">.</span><span class="n">array</span><span class="p">([</span><span class="mi">3</span><span class="p">]</span> <span class="o">*</span> <span class="mi">4</span><span class="p">,</span> <span class="n">dtype</span><span class="o">=</span><span class="s">'int32'</span><span class="p">),</span>
<span class="s">'E'</span><span class="p">:</span> <span class="n">pd</span><span class="p">.</span><span class="n">Categorical</span><span class="p">([</span><span class="s">"test"</span><span class="p">,</span> <span class="s">"train"</span><span class="p">,</span> <span class="s">"test"</span><span class="p">,</span> <span class="s">"train"</span><span class="p">]),</span>
<span class="s">'F'</span><span class="p">:</span> <span class="s">'foo'</span><span class="p">})</span>
<span class="n">df2</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_4">dtypes</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#dtypes
</span><span class="n">df2</span><span class="p">.</span><span class="n">dtypes</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>A           float64
B    datetime64[ns]
C           float32
D             int32
E          category
F            object
dtype: object
</code></pre></div></div>

<p><a id="_5"></a></p>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#head()
</span><span class="n">df</span><span class="p">.</span><span class="n">head</span><span class="p">()</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.854440</td>
      <td>-0.574851</td>
      <td>-0.356466</td>
      <td>-1.595153</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_6">tail</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#tail()
</span><span class="n">df</span><span class="p">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">3</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.403468</td>
      <td>1.190093</td>
      <td>-1.347149</td>
      <td>0.189084</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_7">index</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#index
</span><span class="n">df</span><span class="p">.</span><span class="n">index</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
               '2013-01-05', '2013-01-06'],
              dtype='datetime64[ns]', freq='D')
</code></pre></div></div>

<h1 id="_8">columns</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#columns
</span><span class="n">df</span><span class="p">.</span><span class="n">columns</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>Index(['A', 'B', 'C', 'D'], dtype='object')
</code></pre></div></div>

<h1 id="_9">to_numpy</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#to_numpy
</span><span class="n">df</span><span class="p">.</span><span class="n">to_numpy</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[-0.85443982, -0.57485138, -0.35646587, -1.59515291],
       [-1.97446682,  0.94085528,  0.2395422 ,  1.65378816],
       [-0.59606223, -0.43563924, -0.26098173, -1.28942613],
       [-0.43825849, -0.65222304, -0.68351457, -0.76216213],
       [ 1.39737522, -0.22655392,  1.71780927, -1.43220544],
       [-0.40346849,  1.19009303, -1.34714893,  0.18908393]])
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df2</span><span class="p">.</span><span class="n">to_numpy</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>array([[1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
       [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo']],
      dtype=object)
</code></pre></div></div>

<h1 id="_10">describe</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#describe()
</span><span class="n">df</span><span class="p">.</span><span class="n">describe</span><span class="p">()</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.478220</td>
      <td>0.040280</td>
      <td>-0.115127</td>
      <td>-0.539346</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.088046</td>
      <td>0.811018</td>
      <td>1.039799</td>
      <td>1.254164</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-1.974467</td>
      <td>-0.652223</td>
      <td>-1.347149</td>
      <td>-1.595153</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.789845</td>
      <td>-0.540048</td>
      <td>-0.601752</td>
      <td>-1.396511</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.517160</td>
      <td>-0.331097</td>
      <td>-0.308724</td>
      <td>-1.025794</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-0.412166</td>
      <td>0.649003</td>
      <td>0.114411</td>
      <td>-0.048728</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.397375</td>
      <td>1.190093</td>
      <td>1.717809</td>
      <td>1.653788</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_11">T</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#T
</span><span class="n">df</span><span class="p">.</span><span class="n">T</span>
</code></pre></div></div>

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
      <th>2013-01-01</th>
      <th>2013-01-02</th>
      <th>2013-01-03</th>
      <th>2013-01-04</th>
      <th>2013-01-05</th>
      <th>2013-01-06</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-0.854440</td>
      <td>-1.974467</td>
      <td>-0.596062</td>
      <td>-0.438258</td>
      <td>1.397375</td>
      <td>-0.403468</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.574851</td>
      <td>0.940855</td>
      <td>-0.435639</td>
      <td>-0.652223</td>
      <td>-0.226554</td>
      <td>1.190093</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.356466</td>
      <td>0.239542</td>
      <td>-0.260982</td>
      <td>-0.683515</td>
      <td>1.717809</td>
      <td>-1.347149</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-1.595153</td>
      <td>1.653788</td>
      <td>-1.289426</td>
      <td>-0.762162</td>
      <td>-1.432205</td>
      <td>0.189084</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_12">sort_index</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#sort_index()
</span><span class="n">df</span><span class="p">.</span><span class="n">sort_index</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">ascending</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.595153</td>
      <td>-0.356466</td>
      <td>-0.574851</td>
      <td>-0.854440</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>1.653788</td>
      <td>0.239542</td>
      <td>0.940855</td>
      <td>-1.974467</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.289426</td>
      <td>-0.260982</td>
      <td>-0.435639</td>
      <td>-0.596062</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.762162</td>
      <td>-0.683515</td>
      <td>-0.652223</td>
      <td>-0.438258</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.432205</td>
      <td>1.717809</td>
      <td>-0.226554</td>
      <td>1.397375</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.189084</td>
      <td>-1.347149</td>
      <td>1.190093</td>
      <td>-0.403468</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_13">sort_values</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#sort_values()
</span><span class="n">df</span><span class="p">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s">'B'</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>-0.854440</td>
      <td>-0.574851</td>
      <td>-0.356466</td>
      <td>-1.595153</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.403468</td>
      <td>1.190093</td>
      <td>-1.347149</td>
      <td>0.189084</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">[</span><span class="s">'A'</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2013-01-01   -0.854440
2013-01-02   -1.974467
2013-01-03   -0.596062
2013-01-04   -0.438258
2013-01-05    1.397375
2013-01-06   -0.403468
Freq: D, Name: A, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">[</span><span class="mi">0</span><span class="p">:</span><span class="mi">3</span><span class="p">]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.854440</td>
      <td>-0.574851</td>
      <td>-0.356466</td>
      <td>-1.595153</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">[</span><span class="s">'20130102'</span><span class="p">:</span><span class="s">'20130104'</span><span class="p">]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_14">df.loc[]</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#df.loc[]
</span><span class="n">df</span><span class="p">.</span><span class="n">loc</span><span class="p">[</span><span class="s">'20130102'</span><span class="p">,</span> <span class="p">[</span><span class="s">'A'</span><span class="p">,</span> <span class="s">'B'</span><span class="p">]]</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>A   -1.974467
B    0.940855
Name: 2013-01-02 00:00:00, dtype: float64
</code></pre></div></div>

<h1 id="_15">df.iloc[]</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#df.iloc[]
</span><span class="n">df</span><span class="p">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">3</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>A   -0.438258
B   -0.652223
C   -0.683515
D   -0.762162
Name: 2013-01-04 00:00:00, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">3</span><span class="p">:</span><span class="mi">5</span><span class="p">,</span> <span class="mi">0</span><span class="p">:</span><span class="mi">2</span><span class="p">]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_16">BOOL_INDEX</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#BOOL_INDEX
</span><span class="n">df</span><span class="p">[</span><span class="n">df</span><span class="p">.</span><span class="n">A</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">[</span><span class="n">df</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>NaN</td>
      <td>1.717809</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>1.190093</td>
      <td>NaN</td>
      <td>0.189084</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_17">isin</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#isin()
</span><span class="n">df2</span> <span class="o">=</span> <span class="n">df</span><span class="p">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">df2</span><span class="p">[</span><span class="s">'E'</span><span class="p">]</span> <span class="o">=</span> <span class="p">[</span><span class="s">'one'</span><span class="p">,</span> <span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span> <span class="s">'three'</span><span class="p">,</span> <span class="s">'four'</span><span class="p">,</span> <span class="s">'three'</span><span class="p">]</span>
<span class="n">df2</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.854440</td>
      <td>-0.574851</td>
      <td>-0.356466</td>
      <td>-1.595153</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>1.653788</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>-0.762162</td>
      <td>three</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
      <td>four</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.403468</td>
      <td>1.190093</td>
      <td>-1.347149</td>
      <td>0.189084</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df2</span><span class="p">[</span><span class="n">df2</span><span class="p">[</span><span class="s">'E'</span><span class="p">].</span><span class="n">isin</span><span class="p">([</span><span class="s">'two'</span><span class="p">,</span> <span class="s">'four'</span><span class="p">])]</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>-1.289426</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.397375</td>
      <td>-0.226554</td>
      <td>1.717809</td>
      <td>-1.432205</td>
      <td>four</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_18">赋值</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#赋值
</span><span class="n">s1</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">],</span> <span class="n">index</span><span class="o">=</span><span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'20130102'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">6</span><span class="p">))</span>
<span class="n">s1</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2013-01-02    1
2013-01-03    2
2013-01-04    3
2013-01-05    4
2013-01-06    5
2013-01-07    6
Freq: D, dtype: int64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">at</span><span class="p">[</span><span class="n">dates</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="s">'A'</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">iat</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s">'D'</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="p">.</span><span class="n">array</span><span class="p">([</span><span class="mi">5</span><span class="p">]</span> <span class="o">*</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">))</span>
</code></pre></div></div>

<h1 id="_19">缺失值</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#缺失值
#reindex()
</span><span class="n">df1</span> <span class="o">=</span> <span class="n">df</span><span class="p">.</span><span class="n">reindex</span><span class="p">(</span><span class="n">index</span><span class="o">=</span><span class="n">dates</span><span class="p">[</span><span class="mi">0</span><span class="p">:</span><span class="mi">4</span><span class="p">],</span> <span class="n">columns</span><span class="o">=</span><span class="nb">list</span><span class="p">(</span><span class="n">df</span><span class="p">.</span><span class="n">columns</span><span class="p">)</span> <span class="o">+</span> <span class="p">[</span><span class="s">'E'</span><span class="p">])</span>
<span class="n">df1</span><span class="p">.</span><span class="n">loc</span><span class="p">[</span><span class="n">dates</span><span class="p">[</span><span class="mi">0</span><span class="p">]:</span><span class="n">dates</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="s">'E'</span><span class="p">]</span> <span class="o">=</span> <span class="mi">1</span>
<span class="n">df1</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.356466</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_20">dropna</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#dropna()
</span><span class="n">df1</span><span class="p">.</span><span class="n">dropna</span><span class="p">(</span><span class="n">how</span><span class="o">=</span><span class="s">'any'</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.356466</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_21">fillna</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df1</span><span class="p">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">value</span><span class="o">=</span><span class="mi">5</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.356466</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>0.239542</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.596062</td>
      <td>-0.435639</td>
      <td>-0.260982</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.438258</td>
      <td>-0.652223</td>
      <td>-0.683515</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_22">isna</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pd</span><span class="p">.</span><span class="n">isna</span><span class="p">(</span><span class="n">df1</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_23">统计</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#统计
</span><span class="n">df</span><span class="p">.</span><span class="n">mean</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>A   -0.335813
B    0.136089
C   -0.115127
D    5.000000
dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">mean</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2013-01-01    1.160884
2013-01-02    1.051483
2013-01-03    0.926829
2013-01-04    0.806501
2013-01-05    1.972158
2013-01-06    1.109869
Freq: D, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">s</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">np</span><span class="p">.</span><span class="n">nan</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">8</span><span class="p">],</span> <span class="n">index</span><span class="o">=</span><span class="n">dates</span><span class="p">).</span><span class="n">shift</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
<span class="n">s</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2013-01-01    NaN
2013-01-02    NaN
2013-01-03    1.0
2013-01-04    3.0
2013-01-05    5.0
2013-01-06    NaN
Freq: D, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">sub</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="s">'index'</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.596062</td>
      <td>-1.435639</td>
      <td>-1.260982</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-3.438258</td>
      <td>-3.652223</td>
      <td>-3.683515</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-3.602625</td>
      <td>-5.226554</td>
      <td>-3.282191</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_24">apply</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#apply()
</span><span class="n">df</span><span class="p">.</span><span class="nb">apply</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">cumsum</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.356466</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.974467</td>
      <td>0.940855</td>
      <td>-0.116924</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.570529</td>
      <td>0.505216</td>
      <td>-0.377905</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-3.008788</td>
      <td>-0.147007</td>
      <td>-1.061420</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.611412</td>
      <td>-0.373561</td>
      <td>0.656389</td>
      <td>25</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-2.014881</td>
      <td>0.816532</td>
      <td>-0.690760</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="nb">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="p">.</span><span class="nb">max</span><span class="p">()</span> <span class="o">-</span> <span class="n">x</span><span class="p">.</span><span class="nb">min</span><span class="p">())</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>A    3.371842
B    1.842316
C    3.064958
D    0.000000
dtype: float64
</code></pre></div></div>

<h1 id="_25">直方图</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#直方图
</span><span class="n">s</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="n">size</span><span class="o">=</span><span class="mi">10</span><span class="p">))</span>
<span class="n">s</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>0    3
1    0
2    1
3    1
4    0
5    6
6    1
7    4
8    4
9    3
dtype: int32
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">s</span><span class="p">.</span><span class="n">value_counts</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1    3
4    2
3    2
0    2
6    1
dtype: int64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">s</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">([</span><span class="s">'A'</span><span class="p">,</span> <span class="s">'B'</span><span class="p">,</span> <span class="s">'C'</span><span class="p">,</span> <span class="s">'Aaba'</span><span class="p">,</span> <span class="s">'Baca'</span><span class="p">,</span> <span class="n">np</span><span class="p">.</span><span class="n">nan</span><span class="p">,</span> <span class="s">'CABA'</span><span class="p">,</span> <span class="s">'dog'</span><span class="p">,</span> <span class="s">'cat'</span><span class="p">])</span>
<span class="n">s</span><span class="p">.</span><span class="nb">str</span><span class="p">.</span><span class="n">lower</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>0       a
1       b
2       c
3    aaba
4    baca
5     NaN
6    caba
7     dog
8     cat
dtype: object
</code></pre></div></div>

<h1 id="_26">合并</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#合并
</span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">4</span><span class="p">))</span>
<span class="n">df</span>
</code></pre></div></div>

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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.365895</td>
      <td>0.064669</td>
      <td>-1.399381</td>
      <td>-1.732080</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.306226</td>
      <td>1.049036</td>
      <td>-0.850992</td>
      <td>1.054144</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.237749</td>
      <td>-0.256360</td>
      <td>0.147857</td>
      <td>-0.994362</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.618422</td>
      <td>1.451188</td>
      <td>-2.276052</td>
      <td>0.599332</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.999072</td>
      <td>1.200498</td>
      <td>-0.407359</td>
      <td>-0.513325</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.312811</td>
      <td>-1.250918</td>
      <td>-0.839915</td>
      <td>0.734955</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.653820</td>
      <td>-2.026057</td>
      <td>-0.583408</td>
      <td>0.090834</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.162350</td>
      <td>-0.171216</td>
      <td>0.286236</td>
      <td>-0.109166</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.483130</td>
      <td>0.335461</td>
      <td>0.817618</td>
      <td>1.726531</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.012278</td>
      <td>0.737449</td>
      <td>-0.429658</td>
      <td>0.888149</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pieces</span> <span class="o">=</span> <span class="p">[</span><span class="n">df</span><span class="p">[:</span><span class="mi">3</span><span class="p">],</span> <span class="n">df</span><span class="p">[</span><span class="mi">3</span><span class="p">:</span><span class="mi">7</span><span class="p">],</span> <span class="n">df</span><span class="p">[</span><span class="mi">7</span><span class="p">:]]</span>
<span class="n">pd</span><span class="p">.</span><span class="n">concat</span><span class="p">(</span><span class="n">pieces</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.365895</td>
      <td>0.064669</td>
      <td>-1.399381</td>
      <td>-1.732080</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.306226</td>
      <td>1.049036</td>
      <td>-0.850992</td>
      <td>1.054144</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.237749</td>
      <td>-0.256360</td>
      <td>0.147857</td>
      <td>-0.994362</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.618422</td>
      <td>1.451188</td>
      <td>-2.276052</td>
      <td>0.599332</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.999072</td>
      <td>1.200498</td>
      <td>-0.407359</td>
      <td>-0.513325</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.312811</td>
      <td>-1.250918</td>
      <td>-0.839915</td>
      <td>0.734955</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.653820</td>
      <td>-2.026057</td>
      <td>-0.583408</td>
      <td>0.090834</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.162350</td>
      <td>-0.171216</td>
      <td>0.286236</td>
      <td>-0.109166</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.483130</td>
      <td>0.335461</td>
      <td>0.817618</td>
      <td>1.726531</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-0.012278</td>
      <td>0.737449</td>
      <td>-0.429658</td>
      <td>0.888149</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">left</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'key'</span><span class="p">:</span> <span class="p">[</span><span class="s">'foo'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">],</span> <span class="s">'lval'</span><span class="p">:</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">]})</span>
<span class="n">right</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'key'</span><span class="p">:</span> <span class="p">[</span><span class="s">'foo'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">],</span> <span class="s">'rval'</span><span class="p">:</span> <span class="p">[</span><span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">]})</span>

<span class="n">left</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">right</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pd</span><span class="p">.</span><span class="n">merge</span><span class="p">(</span><span class="n">left</span><span class="p">,</span> <span class="n">right</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="s">'key'</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">left</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'key'</span><span class="p">:</span> <span class="p">[</span><span class="s">'foo'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">],</span> <span class="s">'lval'</span><span class="p">:</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">]})</span>
<span class="n">right</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'key'</span><span class="p">:</span> <span class="p">[</span><span class="s">'foo'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">],</span> <span class="s">'rval'</span><span class="p">:</span> <span class="p">[</span><span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">]})</span>

<span class="n">left</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">right</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">pd</span><span class="p">.</span><span class="n">merge</span><span class="p">(</span><span class="n">left</span><span class="p">,</span> <span class="n">right</span><span class="p">,</span> <span class="n">on</span><span class="o">=</span><span class="s">'key'</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_26">追加</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#追加
</span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">4</span><span class="p">),</span> <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s">'A'</span><span class="p">,</span> <span class="s">'B'</span><span class="p">,</span> <span class="s">'C'</span><span class="p">,</span> <span class="s">'D'</span><span class="p">])</span>
<span class="n">df</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.705208</td>
      <td>-0.229548</td>
      <td>0.501354</td>
      <td>-0.450969</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.340122</td>
      <td>0.714218</td>
      <td>-1.962493</td>
      <td>-0.657901</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.330998</td>
      <td>1.791533</td>
      <td>-0.849407</td>
      <td>-1.391748</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.264860</td>
      <td>0.127628</td>
      <td>0.565497</td>
      <td>-1.039815</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.058405</td>
      <td>-0.049585</td>
      <td>-0.490190</td>
      <td>-0.727434</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.944004</td>
      <td>0.487715</td>
      <td>0.141249</td>
      <td>1.485957</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-2.325875</td>
      <td>-0.681785</td>
      <td>-0.722487</td>
      <td>0.280039</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.753192</td>
      <td>1.985903</td>
      <td>0.620233</td>
      <td>0.354204</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">s</span> <span class="o">=</span> <span class="n">df</span><span class="p">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">3</span><span class="p">]</span>
<span class="n">df</span><span class="p">.</span><span class="n">append</span><span class="p">(</span><span class="n">s</span><span class="p">,</span> <span class="n">ignore_index</span><span class="o">=</span><span class="bp">True</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.705208</td>
      <td>-0.229548</td>
      <td>0.501354</td>
      <td>-0.450969</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.340122</td>
      <td>0.714218</td>
      <td>-1.962493</td>
      <td>-0.657901</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.330998</td>
      <td>1.791533</td>
      <td>-0.849407</td>
      <td>-1.391748</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.264860</td>
      <td>0.127628</td>
      <td>0.565497</td>
      <td>-1.039815</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.058405</td>
      <td>-0.049585</td>
      <td>-0.490190</td>
      <td>-0.727434</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.944004</td>
      <td>0.487715</td>
      <td>0.141249</td>
      <td>1.485957</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-2.325875</td>
      <td>-0.681785</td>
      <td>-0.722487</td>
      <td>0.280039</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-0.753192</td>
      <td>1.985903</td>
      <td>0.620233</td>
      <td>0.354204</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-1.264860</td>
      <td>0.127628</td>
      <td>0.565497</td>
      <td>-1.039815</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_27">分组</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#分组
</span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">'A'</span><span class="p">:</span> <span class="p">[</span><span class="s">'foo'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">,</span>
<span class="s">'foo'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">],</span>
<span class="s">'B'</span><span class="p">:</span> <span class="p">[</span><span class="s">'one'</span><span class="p">,</span> <span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span> <span class="s">'three'</span><span class="p">,</span>
<span class="s">'two'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span> <span class="s">'one'</span><span class="p">,</span> <span class="s">'three'</span><span class="p">],</span>
<span class="s">'C'</span><span class="p">:</span> <span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">8</span><span class="p">),</span>
<span class="s">'D'</span><span class="p">:</span> <span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">8</span><span class="p">)})</span>
<span class="n">df</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>1.519409</td>
      <td>1.097706</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>one</td>
      <td>-0.121282</td>
      <td>1.324063</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>-0.021356</td>
      <td>-1.335948</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>three</td>
      <td>-1.335837</td>
      <td>-0.440683</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foo</td>
      <td>two</td>
      <td>1.368770</td>
      <td>0.573272</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>two</td>
      <td>1.151514</td>
      <td>0.763971</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foo</td>
      <td>one</td>
      <td>-0.813546</td>
      <td>-1.895725</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foo</td>
      <td>three</td>
      <td>0.831471</td>
      <td>-1.298567</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">groupby</span><span class="p">(</span><span class="s">'A'</span><span class="p">).</span><span class="nb">sum</span><span class="p">()</span>
</code></pre></div></div>

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
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>-0.305605</td>
      <td>1.647351</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>2.884747</td>
      <td>-2.859262</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">groupby</span><span class="p">([</span><span class="s">'A'</span><span class="p">,</span> <span class="s">'B'</span><span class="p">]).</span><span class="nb">sum</span><span class="p">()</span>
</code></pre></div></div>

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
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">bar</th>
      <th>one</th>
      <td>-0.121282</td>
      <td>1.324063</td>
    </tr>
    <tr>
      <th>three</th>
      <td>-1.335837</td>
      <td>-0.440683</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.151514</td>
      <td>0.763971</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">foo</th>
      <th>one</th>
      <td>0.705863</td>
      <td>-0.798019</td>
    </tr>
    <tr>
      <th>three</th>
      <td>0.831471</td>
      <td>-1.298567</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.347414</td>
      <td>-0.762676</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_28">重塑</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#重塑
</span><span class="n">tuples</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="nb">zip</span><span class="p">(</span><span class="o">*</span><span class="p">[[</span><span class="s">'bar'</span><span class="p">,</span> <span class="s">'bar'</span><span class="p">,</span> <span class="s">'baz'</span><span class="p">,</span> <span class="s">'baz'</span><span class="p">,</span>
<span class="s">'foo'</span><span class="p">,</span> <span class="s">'foo'</span><span class="p">,</span> <span class="s">'qux'</span><span class="p">,</span> <span class="s">'qux'</span><span class="p">],</span>
<span class="p">[</span><span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span> <span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span>
<span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">,</span> <span class="s">'one'</span><span class="p">,</span> <span class="s">'two'</span><span class="p">]]))</span>
<span class="n">index</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">MultiIndex</span><span class="p">.</span><span class="n">from_tuples</span><span class="p">(</span><span class="n">tuples</span><span class="p">,</span> <span class="n">names</span><span class="o">=</span><span class="p">[</span><span class="s">'first'</span><span class="p">,</span> <span class="s">'second'</span><span class="p">])</span>
<span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">8</span><span class="p">,</span> <span class="mi">2</span><span class="p">),</span> <span class="n">index</span><span class="o">=</span><span class="n">index</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s">'A'</span><span class="p">,</span> <span class="s">'B'</span><span class="p">])</span>
<span class="n">df2</span> <span class="o">=</span> <span class="n">df</span><span class="p">[:</span><span class="mi">4</span><span class="p">]</span>
<span class="n">df2</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-1.011320</td>
      <td>0.094016</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.485568</td>
      <td>-1.141193</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>0.043433</td>
      <td>0.875106</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.540609</td>
      <td>-0.208505</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">stacked</span> <span class="o">=</span> <span class="n">df2</span><span class="p">.</span><span class="n">stack</span><span class="p">()</span>
<span class="n">stacked</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>first  second   
bar    one     A   -1.011320
               B    0.094016
       two     A    1.485568
               B   -1.141193
baz    one     A    0.043433
               B    0.875106
       two     A    0.540609
               B   -0.208505
dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">stacked</span><span class="p">.</span><span class="n">unstack</span><span class="p">()</span>
</code></pre></div></div>

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
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-1.011320</td>
      <td>0.094016</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.485568</td>
      <td>-1.141193</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>0.043433</td>
      <td>0.875106</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.540609</td>
      <td>-0.208505</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">stacked</span><span class="p">.</span><span class="n">unstack</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>-1.011320</td>
      <td>1.485568</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.094016</td>
      <td>-1.141193</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>0.043433</td>
      <td>0.540609</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.875106</td>
      <td>-0.208505</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">stacked</span><span class="p">.</span><span class="n">unstack</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>-1.011320</td>
      <td>0.043433</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.094016</td>
      <td>0.875106</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>1.485568</td>
      <td>0.540609</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.141193</td>
      <td>-0.208505</td>
    </tr>
  </tbody>
</table>
</div>

<h1 id="_28">时间序列</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#时间序列
</span><span class="n">rng</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'1/1/2012'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">freq</span><span class="o">=</span><span class="s">'S'</span><span class="p">)</span>
<span class="n">ts</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randint</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">500</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">rng</span><span class="p">)),</span> <span class="n">index</span><span class="o">=</span><span class="n">rng</span><span class="p">)</span>
<span class="n">ts</span><span class="p">.</span><span class="n">resample</span><span class="p">(</span><span class="s">'5Min'</span><span class="p">).</span><span class="nb">sum</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-01-01    24109
Freq: 5T, dtype: int32
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">rng</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'3/6/2012 00:00'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">freq</span><span class="o">=</span><span class="s">'D'</span><span class="p">)</span>
<span class="n">ts</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">rng</span><span class="p">)),</span> <span class="n">rng</span><span class="p">)</span>
<span class="n">ts</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-03-06    1.493093
2012-03-07    1.384363
2012-03-08    1.046803
2012-03-09    1.086955
2012-03-10   -1.564983
Freq: D, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ts_utc</span> <span class="o">=</span> <span class="n">ts</span><span class="p">.</span><span class="n">tz_localize</span><span class="p">(</span><span class="s">'UTC'</span><span class="p">)</span>
<span class="n">ts_utc</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-03-06 00:00:00+00:00    1.493093
2012-03-07 00:00:00+00:00    1.384363
2012-03-08 00:00:00+00:00    1.046803
2012-03-09 00:00:00+00:00    1.086955
2012-03-10 00:00:00+00:00   -1.564983
Freq: D, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ts_utc</span><span class="p">.</span><span class="n">tz_convert</span><span class="p">(</span><span class="s">'US/Eastern'</span><span class="p">)</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-03-05 19:00:00-05:00    1.493093
2012-03-06 19:00:00-05:00    1.384363
2012-03-07 19:00:00-05:00    1.046803
2012-03-08 19:00:00-05:00    1.086955
2012-03-09 19:00:00-05:00   -1.564983
Freq: D, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">rng</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'1/1/2012'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">freq</span><span class="o">=</span><span class="s">'M'</span><span class="p">)</span>
<span class="n">ts</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">rng</span><span class="p">)),</span> <span class="n">index</span><span class="o">=</span><span class="n">rng</span><span class="p">)</span>
<span class="n">ts</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-01-31    0.688941
2012-02-29    1.194007
2012-03-31    0.182798
2012-04-30    1.531025
2012-05-31    0.130136
Freq: M, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ps</span> <span class="o">=</span> <span class="n">ts</span><span class="p">.</span><span class="n">to_period</span><span class="p">()</span>
<span class="n">ps</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-01    0.688941
2012-02    1.194007
2012-03    0.182798
2012-04    1.531025
2012-05    0.130136
Freq: M, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">ps</span><span class="p">.</span><span class="n">to_timestamp</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>2012-01-01    0.688941
2012-02-01    1.194007
2012-03-01    0.182798
2012-04-01    1.531025
2012-05-01    0.130136
Freq: MS, dtype: float64
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">prng</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">period_range</span><span class="p">(</span><span class="s">'1990Q1'</span><span class="p">,</span> <span class="s">'2000Q4'</span><span class="p">,</span> <span class="n">freq</span><span class="o">=</span><span class="s">'Q-NOV'</span><span class="p">)</span>
<span class="n">ts</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">prng</span><span class="p">)),</span> <span class="n">prng</span><span class="p">)</span>
<span class="n">ts</span><span class="p">.</span><span class="n">index</span> <span class="o">=</span> <span class="p">(</span><span class="n">prng</span><span class="p">.</span><span class="n">asfreq</span><span class="p">(</span><span class="s">'M'</span><span class="p">,</span> <span class="s">'e'</span><span class="p">)</span> <span class="o">+</span> <span class="mi">1</span><span class="p">).</span><span class="n">asfreq</span><span class="p">(</span><span class="s">'H'</span><span class="p">,</span> <span class="s">'s'</span><span class="p">)</span> <span class="o">+</span> <span class="mi">9</span>
<span class="n">ts</span><span class="p">.</span><span class="n">head</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>1990-03-01 09:00   -0.880170
1990-06-01 09:00    0.048305
1990-09-01 09:00    1.597029
1990-12-01 09:00    0.348681
1991-03-01 09:00   -0.994927
Freq: H, dtype: float64
</code></pre></div></div>

<h1 id="_29">Categoricals</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#Categoricals
</span><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s">"id"</span><span class="p">:</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">],</span>
<span class="s">"raw_grade"</span><span class="p">:</span> <span class="p">[</span><span class="s">'a'</span><span class="p">,</span> <span class="s">'b'</span><span class="p">,</span> <span class="s">'b'</span><span class="p">,</span> <span class="s">'a'</span><span class="p">,</span> <span class="s">'a'</span><span class="p">,</span> <span class="s">'e'</span><span class="p">]})</span>
<span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">"raw_grade"</span><span class="p">].</span><span class="n">astype</span><span class="p">(</span><span class="s">"category"</span><span class="p">)</span>
<span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>0    a
1    b
2    b
3    a
4    a
5    e
Name: grade, dtype: category
Categories (3, object): [a, b, e]
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">].</span><span class="n">cat</span><span class="p">.</span><span class="n">categories</span> <span class="o">=</span> <span class="p">[</span><span class="s">"very good"</span><span class="p">,</span> <span class="s">"good"</span><span class="p">,</span> <span class="s">"very bad"</span><span class="p">]</span>
<span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">].</span><span class="n">cat</span><span class="p">.</span><span class="n">set_categories</span><span class="p">([</span><span class="s">"very bad"</span><span class="p">,</span> <span class="s">"bad"</span><span class="p">,</span> <span class="s">"medium"</span><span class="p">,</span>
<span class="s">"good"</span><span class="p">,</span> <span class="s">"very good"</span><span class="p">])</span>
<span class="n">df</span><span class="p">[</span><span class="s">"grade"</span><span class="p">]</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>0    very good
1         good
2         good
3    very good
4    very good
5     very bad
Name: grade, dtype: category
Categories (5, object): [very bad, bad, medium, good, very good]
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s">"grade"</span><span class="p">)</span>
</code></pre></div></div>

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
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">df</span><span class="p">.</span><span class="n">groupby</span><span class="p">(</span><span class="s">"grade"</span><span class="p">).</span><span class="n">size</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>grade
very bad     1
bad          0
medium       0
good         2
very good    3
dtype: int64
</code></pre></div></div>

<h1 id="_30">可视化</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#可视化
</span><span class="n">ts</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">Series</span><span class="p">(</span><span class="n">np</span><span class="p">.</span><span class="n">random</span><span class="p">.</span><span class="n">randn</span><span class="p">(</span><span class="mi">1000</span><span class="p">),</span>
<span class="n">index</span><span class="o">=</span><span class="n">pd</span><span class="p">.</span><span class="n">date_range</span><span class="p">(</span><span class="s">'1/1/2000'</span><span class="p">,</span> <span class="n">periods</span><span class="o">=</span><span class="mi">1000</span><span class="p">))</span>
<span class="n">ts</span> <span class="o">=</span> <span class="n">ts</span><span class="p">.</span><span class="n">cumsum</span><span class="p">()</span>
<span class="n">ts</span><span class="p">.</span><span class="n">plot</span><span class="p">()</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>&lt;matplotlib.axes._subplots.AxesSubplot at 0x1ee150ac6d8&gt;
</code></pre></div></div>

<p><img src="pandas_index_files/pandas_index_72_1.svg" alt="svg" /></p>

<h1 id="_31">IO</h1>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">#IO
</span><span class="n">df</span><span class="p">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s">'foo.csv'</span><span class="p">)</span>
<span class="n">pd</span><span class="p">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">'foo.csv'</span><span class="p">)</span>
<span class="n">df</span><span class="p">.</span><span class="n">to_hdf</span><span class="p">(</span><span class="s">'foo.h5'</span><span class="p">,</span> <span class="s">'df'</span><span class="p">)</span>
<span class="n">pd</span><span class="p">.</span><span class="n">read_hdf</span><span class="p">(</span><span class="s">'foo.h5'</span><span class="p">,</span> <span class="s">'df'</span><span class="p">)</span>
<span class="n">df</span><span class="p">.</span><span class="n">to_excel</span><span class="p">(</span><span class="s">'foo.xlsx'</span><span class="p">,</span> <span class="n">sheet_name</span><span class="o">=</span><span class="s">'Sheet1'</span><span class="p">)</span>
<span class="n">pd</span><span class="p">.</span><span class="n">read_excel</span><span class="p">(</span><span class="s">'foo.xlsx'</span><span class="p">,</span> <span class="s">'Sheet1'</span><span class="p">,</span> <span class="n">index_col</span><span class="o">=</span><span class="bp">None</span><span class="p">,</span> <span class="n">na_values</span><span class="o">=</span><span class="p">[</span><span class="s">'NA'</span><span class="p">])</span>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-02-07T18:50:00+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/02/07/ai-pca.html">PCA 主成分分析</a></div><div class="next"><span>下篇</span><a href="/2020/02/07/ai-numpy-amin-and-amax.html">Numpy AMin Amax</a></div></div></div>

</div>

<script>(function() {
  var SOURCES = window.TEXT_VARIABLES.sources;
  window.Lazyload.js(SOURCES.jquery, function() {
    $(function() {
      var $this ,$scroll;
      var $articleContent = $('.js-article-content');
      var hasSidebar = $('.js-page-root').hasClass('layout--page--sidebar');
      var scroll = hasSidebar ? '.js-page-main' : 'html, body';
      $scroll = $(scroll);

      $articleContent.find('.highlight').each(function() {
        $this = $(this);
        $this.attr('data-lang', $this.find('code').attr('data-lang'));
      });
      $articleContent.find('h1[id], h2[id], h3[id], h4[id], h5[id], h6[id]').each(function() {
        $this = $(this);
        $this.append($('<a class="anchor d-print-none" aria-hidden="true"></a>').html('<i class="fas fa-anchor"></i>'));
      });
      $articleContent.on('click', '.anchor', function() {
        $scroll.scrollToAnchor('#' + $(this).parent().attr('id'), 400);
      });
    });
  });
})();
</script>
</div></article>