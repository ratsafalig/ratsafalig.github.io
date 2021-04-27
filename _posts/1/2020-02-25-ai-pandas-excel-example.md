---
title: Pandas Excel 示例
date: 2020-02-25 09:05:23 Z
tags:
- Misc
layout: article
---
<article itemscope itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Excel 示例"><meta itemprop="author" content="航"/><meta itemprop="datePublished" content="2020-02-25T17:05:23+08:00">
    <meta itemprop="keywords" content="Misc"><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Excel 示例" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-25T17:05:23+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><article itemscope="" itemtype="http://schema.org/Article"><meta itemprop="headline" content="Pandas Excel 示例" /><meta itemprop="author" content="航" /><meta itemprop="datePublished" content="2020-02-25T17:05:23+08:00" />
    <meta itemprop="keywords" content="Misc" /><div class="js-article-content"><div class="layout--article"><!-- start custom article top snippet -->

<!-- end custom article top snippet -->
<div class="article__content" itemprop="articleBody"><div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="n">pd</span>
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">contry</span> <span class="o">=</span> <span class="n">pd</span><span class="p">.</span><span class="n">read_excel</span><span class="p">(</span><span class="s">"contry.xlsx"</span><span class="p">,</span> <span class="n">sheet_name</span><span class="o">=</span><span class="s">'Sheet1'</span><span class="p">)</span>
<span class="n">contry</span>
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
      <th>Country</th>
      <th>Unnamed: 1</th>
      <th>Notes</th>
      <th>1949</th>
      <th>1950</th>
      <th>1951</th>
      <th>1952</th>
      <th>1953</th>
      <th>1954</th>
      <th>1955</th>
      <th>...</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>2018 Current</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Zimbabwe</td>
      <td>NaN</td>
      <td>26</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>105.292</td>
      <td>205.437</td>
      <td>317.68</td>
      <td>350.322</td>
      <td>362.287</td>
      <td>379.886</td>
      <td>366.86</td>
      <td>340.522</td>
      <td>404.72</td>
      <td>420.364</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Zambia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>257.786</td>
      <td>270.757</td>
      <td>301.395</td>
      <td>325.234</td>
      <td>400.163</td>
      <td>428.087</td>
      <td>348.908</td>
      <td>339.665</td>
      <td>386.445</td>
      <td>378.025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Yugoslavia</td>
      <td>NaN</td>
      <td>79</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Yemen, North</td>
      <td>NaN</td>
      <td>103</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Yemen</td>
      <td>NaN</td>
      <td>102</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>2846.84</td>
      <td>2581.37</td>
      <td>2364.83</td>
      <td>2175.91</td>
      <td>2093.45</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>180</th>
      <td>Argentina</td>
      <td>NaN</td>
      <td>35</td>
      <td>5456.8</td>
      <td>4325.49</td>
      <td>2932.01</td>
      <td>2986.04</td>
      <td>3893.56</td>
      <td>3709.81</td>
      <td>3746</td>
      <td>...</td>
      <td>4562.01</td>
      <td>4496.6</td>
      <td>4441.11</td>
      <td>4976.09</td>
      <td>5147.97</td>
      <td>5098.19</td>
      <td>4959.95</td>
      <td>5459.64</td>
      <td>5336.79</td>
      <td>4144.99</td>
    </tr>
    <tr>
      <th>181</th>
      <td>Angola</td>
      <td>NaN</td>
      <td>4</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>5444.59</td>
      <td>5097.94</td>
      <td>5350.36</td>
      <td>7307.67</td>
      <td>7798.18</td>
      <td>4551.91</td>
      <td>3590.5</td>
      <td>3062.87</td>
      <td>2507.85</td>
      <td>1983.61</td>
    </tr>
    <tr>
      <th>182</th>
      <td>Algeria</td>
      <td>NaN</td>
      <td>1</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>5410.7</td>
      <td>7743.62</td>
      <td>8148.56</td>
      <td>8801.77</td>
      <td>10136.7</td>
      <td>10604.9</td>
      <td>10636.6</td>
      <td>10073.4</td>
      <td>9458.56</td>
      <td>9583.72</td>
    </tr>
    <tr>
      <th>183</th>
      <td>Albania</td>
      <td>NaN</td>
      <td>§ ¶ 66</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>186.648</td>
      <td>185.628</td>
      <td>181.402</td>
      <td>170.809</td>
      <td>166.03</td>
      <td>144.561</td>
      <td>139.136</td>
      <td>144.383</td>
      <td>159.963</td>
      <td>180.489</td>
    </tr>
    <tr>
      <th>184</th>
      <td>Afghanistan</td>
      <td>Base year 1980 up to 1977</td>
      <td>52</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>296.45</td>
      <td>291.587</td>
      <td>218.517</td>
      <td>201.456</td>
      <td>245.718</td>
      <td>196.505</td>
      <td>194.666</td>
      <td>191.407</td>
      <td>204.243</td>
      <td>198.086</td>
    </tr>
  </tbody>
</table>
<p>185 rows × 74 columns</p>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">contry</span><span class="p">.</span><span class="n">index</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>RangeIndex(start=0, stop=185, step=1)
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">contry</span><span class="p">.</span><span class="n">head</span><span class="p">()</span>
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
      <th>Country</th>
      <th>Unnamed: 1</th>
      <th>Notes</th>
      <th>1949</th>
      <th>1950</th>
      <th>1951</th>
      <th>1952</th>
      <th>1953</th>
      <th>1954</th>
      <th>1955</th>
      <th>...</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>2018 Current</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Zimbabwe</td>
      <td>NaN</td>
      <td>26</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>105.292</td>
      <td>205.437</td>
      <td>317.68</td>
      <td>350.322</td>
      <td>362.287</td>
      <td>379.886</td>
      <td>366.86</td>
      <td>340.522</td>
      <td>404.72</td>
      <td>420.364</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Zambia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>257.786</td>
      <td>270.757</td>
      <td>301.395</td>
      <td>325.234</td>
      <td>400.163</td>
      <td>428.087</td>
      <td>348.908</td>
      <td>339.665</td>
      <td>386.445</td>
      <td>378.025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Yugoslavia</td>
      <td>NaN</td>
      <td>79</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Yemen, North</td>
      <td>NaN</td>
      <td>103</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>...</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Yemen</td>
      <td>NaN</td>
      <td>102</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>xxx</td>
      <td>...</td>
      <td>2846.84</td>
      <td>2581.37</td>
      <td>2364.83</td>
      <td>2175.91</td>
      <td>2093.45</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
      <td>. .</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 74 columns</p>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">_1949_to_2018</span> <span class="o">=</span> <span class="n">contry</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,:]</span>
<span class="n">_1949_to_2018</span><span class="p">[(</span><span class="n">_1949_to_2018</span> <span class="o">==</span> <span class="s">'xxx'</span><span class="p">)</span> <span class="o">|</span> <span class="p">(</span><span class="n">_1949_to_2018</span> <span class="o">==</span> <span class="s">'. .'</span><span class="p">)]</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">_1949_to_2018</span>
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
      <th>Country</th>
      <th>Unnamed: 1</th>
      <th>Notes</th>
      <th>1949</th>
      <th>1950</th>
      <th>1951</th>
      <th>1952</th>
      <th>1953</th>
      <th>1954</th>
      <th>1955</th>
      <th>...</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
      <th>2018</th>
      <th>2018 Current</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Zimbabwe</td>
      <td>NaN</td>
      <td>26</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>105.292</td>
      <td>205.437</td>
      <td>317.68</td>
      <td>350.322</td>
      <td>362.287</td>
      <td>379.886</td>
      <td>366.86</td>
      <td>340.522</td>
      <td>404.72</td>
      <td>420.364</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Zambia</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>257.786</td>
      <td>270.757</td>
      <td>301.395</td>
      <td>325.234</td>
      <td>400.163</td>
      <td>428.087</td>
      <td>348.908</td>
      <td>339.665</td>
      <td>386.445</td>
      <td>378.025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Yugoslavia</td>
      <td>NaN</td>
      <td>79</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Yemen, North</td>
      <td>NaN</td>
      <td>103</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Yemen</td>
      <td>NaN</td>
      <td>102</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2846.84</td>
      <td>2581.37</td>
      <td>2364.83</td>
      <td>2175.91</td>
      <td>2093.45</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>180</th>
      <td>Argentina</td>
      <td>NaN</td>
      <td>35</td>
      <td>5456.8</td>
      <td>4325.49</td>
      <td>2932.01</td>
      <td>2986.04</td>
      <td>3893.56</td>
      <td>3709.81</td>
      <td>3746</td>
      <td>...</td>
      <td>4562.01</td>
      <td>4496.6</td>
      <td>4441.11</td>
      <td>4976.09</td>
      <td>5147.97</td>
      <td>5098.19</td>
      <td>4959.95</td>
      <td>5459.64</td>
      <td>5336.79</td>
      <td>4144.99</td>
    </tr>
    <tr>
      <th>181</th>
      <td>Angola</td>
      <td>NaN</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>5444.59</td>
      <td>5097.94</td>
      <td>5350.36</td>
      <td>7307.67</td>
      <td>7798.18</td>
      <td>4551.91</td>
      <td>3590.5</td>
      <td>3062.87</td>
      <td>2507.85</td>
      <td>1983.61</td>
    </tr>
    <tr>
      <th>182</th>
      <td>Algeria</td>
      <td>NaN</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>5410.7</td>
      <td>7743.62</td>
      <td>8148.56</td>
      <td>8801.77</td>
      <td>10136.7</td>
      <td>10604.9</td>
      <td>10636.6</td>
      <td>10073.4</td>
      <td>9458.56</td>
      <td>9583.72</td>
    </tr>
    <tr>
      <th>183</th>
      <td>Albania</td>
      <td>NaN</td>
      <td>§ ¶ 66</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>186.648</td>
      <td>185.628</td>
      <td>181.402</td>
      <td>170.809</td>
      <td>166.03</td>
      <td>144.561</td>
      <td>139.136</td>
      <td>144.383</td>
      <td>159.963</td>
      <td>180.489</td>
    </tr>
    <tr>
      <th>184</th>
      <td>Afghanistan</td>
      <td>Base year 1980 up to 1977</td>
      <td>52</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>296.45</td>
      <td>291.587</td>
      <td>218.517</td>
      <td>201.456</td>
      <td>245.718</td>
      <td>196.505</td>
      <td>194.666</td>
      <td>191.407</td>
      <td>204.243</td>
      <td>198.086</td>
    </tr>
  </tbody>
</table>
<p>185 rows × 74 columns</p>
</div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="n">_1949_to_2018</span> <span class="o">=</span> <span class="n">_1949_to_2018</span><span class="p">.</span><span class="n">drop</span><span class="p">([</span><span class="s">'Unnamed: 1'</span><span class="p">,</span><span class="s">'Notes'</span><span class="p">,</span><span class="s">'2018 Current'</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
<span class="n">_1949_to_2018</span> <span class="o">=</span> <span class="n">_1949_to_2018</span><span class="p">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">value</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>

</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
<span class="k">def</span> <span class="nf">top_ten</span><span class="p">(</span><span class="n">arr</span><span class="p">:</span> <span class="n">pd</span><span class="p">.</span><span class="n">DataFrame</span><span class="p">):</span>
    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1949</span><span class="p">,</span><span class="mi">2019</span><span class="p">):</span>
        <span class="n">temp1</span> <span class="o">=</span> <span class="n">arr</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,[</span><span class="n">i</span><span class="p">]].</span><span class="n">copy</span><span class="p">()</span>
        <span class="n">temp1</span><span class="p">.</span><span class="n">columns</span> <span class="o">=</span> <span class="p">[</span><span class="s">'_'</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">i</span><span class="p">)]</span>
        <span class="n">temp1</span> <span class="o">=</span> <span class="n">temp1</span><span class="p">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="s">'_'</span><span class="o">+</span><span class="nb">str</span><span class="p">(</span><span class="n">i</span><span class="p">),</span> <span class="n">ascending</span><span class="o">=</span><span class="bp">False</span><span class="p">)</span>
        <span class="n">temp1</span> <span class="o">=</span> <span class="n">temp1</span><span class="p">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">9</span><span class="p">]</span>
        <span class="n">temp1</span> <span class="o">=</span> <span class="n">temp1</span><span class="p">.</span><span class="n">to_numpy</span><span class="p">()[</span><span class="mi">0</span><span class="p">]</span>
        <span class="n">arr</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">=</span> <span class="n">arr</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="p">[</span><span class="n">i</span><span class="p">]][</span><span class="n">arr</span><span class="p">.</span><span class="n">loc</span><span class="p">[:,[</span><span class="n">i</span><span class="p">]]</span> <span class="o">&gt;=</span> <span class="n">temp1</span><span class="p">].</span><span class="n">fillna</span><span class="p">(</span><span class="n">value</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="k">return</span> <span class="n">arr</span>

<span class="n">top_ten</span><span class="p">(</span><span class="n">_1949_to_2018</span><span class="p">).</span><span class="n">T</span><span class="p">.</span><span class="n">to_excel</span><span class="p">(</span><span class="s">'dst.xlsx'</span><span class="p">,</span><span class="n">sheet_name</span><span class="o">=</span><span class="s">'Sheet1'</span><span class="p">)</span>

</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="s">'''
temp1 = _1949_to_2018.loc[:,[1950]].copy()
temp1.columns = ['_1950']
temp1 = temp1.sort_values(by='_1950', ascending=False)
temp1 = temp1.iloc[9]
temp1 = temp1.to_numpy()[0]
_1949_to_2018.loc[:, [1950]] = _1949_to_2018.loc[:, [1950]][_1949_to_2018.loc[:,[1950]] &gt;= temp1].fillna(value=0)

_1949_to_2018.to_excel("dst.xlsx",sheet_name='Sheet1')
'''</span>
</code></pre></div></div>

<div class="language-plaintext highlighter-rouge"><div class="highlight"><pre class="highlight"><code>'\ntemp1 = _1949_to_2018.loc[:,[1950]].copy()\ntemp1.columns = [\'_1950\']\ntemp1 = temp1.sort_values(by=\'_1950\', ascending=False)\ntemp1 = temp1.iloc[9]\ntemp1 = temp1.to_numpy()[0]\n_1949_to_2018.loc[:, [1950]] = _1949_to_2018.loc[:, [1950]][_1949_to_2018.loc[:,[1950]] &gt;= temp1].fillna(value=0)\n\n_1949_to_2018.to_excel("dst.xlsx",sheet_name=\'Sheet1\')\n'
</code></pre></div></div>

<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code>
</code></pre></div></div>
</div><section class="article__sharing d-print-none"></section><div class="d-print-none"><footer class="article__footer"><meta itemprop="dateModified" content="2020-02-25T17:05:23+08:00" /><!-- start custom article footer snippet -->

<!-- end custom article footer snippet -->
<div class="article__subscribe"><div class="subscribe"><i class="fas fa-rss"></i> <a type="application/rss+xml" href="/feed.xml">订阅</a></div>
</div><div class="article__license"><div class="license">
    <p>本文遵守 <a itemprop="license" rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">Attribution-NonCommercial 4.0 International</a> 许可协议。
      <a rel="license" href="https://creativecommons.org/licenses/by-nc/4.0/">
        <img alt="Attribution-NonCommercial 4.0 International" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
      </a>
    </p>
  </div></div></footer>
<div class="article__section-navigator clearfix"><div class="previous"><span>上篇</span><a href="/2020/02/11/ai-neural-network.html">V1 Neural Network 神经网络</a></div><div class="next"><span>下篇</span><a href="/2020/05/29/mysql-explain-extra.html">Mysql Explain 操作的 Extra列信息</a></div></div></div>

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