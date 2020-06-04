<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome file</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h2 id="백준-7568번">백준 7568번</h2>
<h3 id="문제설명">1. 문제설명</h3>
<p>지민이는 자신의 저택에서 MN개의 단위 정사각형으로 나누어져 있는 M<em>N 크기의 보드를 찾았다. 어떤 정사각형은 검은색으로 칠해져 있고, 나머지는 흰색으로 칠해져 있다. 지민이는 이 보드를 잘라서 8</em>8 크기의 체스판으로 만들려고 한다.</p>
<p>체스판은 검은색과 흰색이 번갈아서 칠해져 있어야 한다. 구체적으로, 각 칸이 검은색과 흰색 중 하나로 색칠되어 있고, 변을 공유하는 두 개의 사각형은 다른 색으로 칠해져 있어야 한다. 따라서 이 정의를 따르면 체스판을 색칠하는 경우는 두 가지뿐이다. 하나는 맨 왼쪽 위 칸이 흰색인 경우, 하나는 검은색인 경우이다.</p>
<p>보드가 체스판처럼 칠해져 있다는 보장이 없어서, 지민이는 8<em>8 크기의 체스판으로 잘라낸 후에 몇 개의 정사각형을 다시 칠해야겠다고 생각했다. 당연히 8</em>8 크기는 아무데서나 골라도 된다. 지민이가 다시 칠해야 하는 정사각형의 최소 개수를 구하는 프로그램을 작성하시오.</p>
<h3 id="입출력">2. 입출력</h3>

<table>
<thead>
<tr>
<th>입력</th>
<th>출력</th>
</tr>
</thead>
<tbody>
<tr>
<td>N M</td>
<td>다시 칠해야 하는 정사각형 개수의 최솟값</td>
</tr>
</tbody>
</table><h3 id="구현">3. 구현</h3>
<p>브루트포스이기 때문에 모든 경우의 수를 탐색하려면 어떻게 해야될지 생각했다.</p>
<p>비교의 편의를 위해 미리 블랙, 화이트를 만들어 놓고, 두가지 경우의 수 모두 탐색했을 때의 최소값을 찾았다.</p>
<pre class=" language-cpp"><code class="prism  language-cpp">
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;iostream&gt;</span></span>
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;string&gt;</span></span>
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;vector&gt;</span></span>
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;algorithm&gt;</span></span>

<span class="token keyword">using</span> <span class="token keyword">namespace</span> std<span class="token punctuation">;</span>

string white<span class="token punctuation">[</span><span class="token number">8</span><span class="token punctuation">]</span> <span class="token operator">=</span>
<span class="token punctuation">{</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

string black<span class="token punctuation">[</span><span class="token number">8</span><span class="token punctuation">]</span> <span class="token operator">=</span>
<span class="token punctuation">{</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span><span class="token punctuation">,</span>
	<span class="token string">"BWBWBWBW"</span><span class="token punctuation">,</span>
	<span class="token string">"WBWBWBWB"</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>


<span class="token keyword">int</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">{</span>
	<span class="token keyword">int</span> n<span class="token punctuation">,</span> m<span class="token punctuation">;</span>
	cin <span class="token operator">&gt;&gt;</span> m <span class="token operator">&gt;&gt;</span> n<span class="token punctuation">;</span>
	vector<span class="token operator">&lt;</span>string<span class="token operator">&gt;</span> array<span class="token punctuation">;</span>
	vector<span class="token operator">&lt;</span><span class="token keyword">int</span><span class="token operator">&gt;</span> answer<span class="token punctuation">;</span>

	<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> m<span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span>
	<span class="token punctuation">{</span>
		string temp<span class="token punctuation">;</span>
		cin <span class="token operator">&gt;&gt;</span> temp<span class="token punctuation">;</span>
		array<span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span>temp<span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>

	<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;=</span> m <span class="token operator">-</span> <span class="token number">8</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span>
	<span class="token punctuation">{</span>
		<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> j <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> j <span class="token operator">&lt;=</span> n <span class="token operator">-</span> <span class="token number">8</span><span class="token punctuation">;</span> j<span class="token operator">++</span><span class="token punctuation">)</span>
		<span class="token punctuation">{</span>
			<span class="token keyword">int</span> count <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
			<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> y <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> y <span class="token operator">&lt;</span> <span class="token number">8</span><span class="token punctuation">;</span> y<span class="token operator">++</span><span class="token punctuation">)</span>
			<span class="token punctuation">{</span>
				<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> x <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> x <span class="token operator">&lt;</span> <span class="token number">8</span><span class="token punctuation">;</span> x<span class="token operator">++</span><span class="token punctuation">)</span>
				<span class="token punctuation">{</span>
					<span class="token keyword">if</span> <span class="token punctuation">(</span>array<span class="token punctuation">[</span>i <span class="token operator">+</span> y<span class="token punctuation">]</span><span class="token punctuation">[</span>j <span class="token operator">+</span> x<span class="token punctuation">]</span> <span class="token operator">!=</span> white<span class="token punctuation">[</span>y<span class="token punctuation">]</span><span class="token punctuation">[</span>x<span class="token punctuation">]</span><span class="token punctuation">)</span>
						count<span class="token operator">++</span><span class="token punctuation">;</span>
				<span class="token punctuation">}</span>
			<span class="token punctuation">}</span>
			answer<span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span>count<span class="token punctuation">)</span><span class="token punctuation">;</span>

			count <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span>
			<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> y <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> y <span class="token operator">&lt;</span> <span class="token number">8</span><span class="token punctuation">;</span> y<span class="token operator">++</span><span class="token punctuation">)</span>
			<span class="token punctuation">{</span>
				<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> x <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> x <span class="token operator">&lt;</span> <span class="token number">8</span><span class="token punctuation">;</span> x<span class="token operator">++</span><span class="token punctuation">)</span>
				<span class="token punctuation">{</span>
					<span class="token keyword">if</span> <span class="token punctuation">(</span>array<span class="token punctuation">[</span>i <span class="token operator">+</span> y<span class="token punctuation">]</span><span class="token punctuation">[</span>j <span class="token operator">+</span> x<span class="token punctuation">]</span> <span class="token operator">!=</span> black<span class="token punctuation">[</span>y<span class="token punctuation">]</span><span class="token punctuation">[</span>x<span class="token punctuation">]</span><span class="token punctuation">)</span>
						count<span class="token operator">++</span><span class="token punctuation">;</span>
				<span class="token punctuation">}</span>
			<span class="token punctuation">}</span>
			answer<span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span>count<span class="token punctuation">)</span><span class="token punctuation">;</span>

		<span class="token punctuation">}</span>
	<span class="token punctuation">}</span>

	cout <span class="token operator">&lt;&lt;</span> <span class="token operator">*</span><span class="token function">min_element</span><span class="token punctuation">(</span>answer<span class="token punctuation">.</span><span class="token function">begin</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">,</span> answer<span class="token punctuation">.</span><span class="token function">end</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>


</code></pre>
</div>
</body>

</html>
