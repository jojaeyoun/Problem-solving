<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome file</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h2 id="기본예제-bfs">기본예제 BFS</h2>
<h3 id="설명">1. 설명</h3>
<p>이 글은 동빈나님의 블로그(<a href="https://m.blog.naver.com/ndb796/221230944971">https://m.blog.naver.com/ndb796/221230944971</a>)를 참고하여 정리하였다. (추천!!)</p>
<p>BFS는 넓이 우선 탐색이라는 의미이며, 현재 노드에서 가장 가까운 노드를 먼저 탐색하기 때문에 DFS와 차이가 있다.</p>
<p>BFS알고리즘의 동작은 다음과 같다.</p>
<pre><code>1.큐에서 노드 하나를 꺼낸다.
2.해당 노드에 연결된 노드 중 방문하지 않는 노드를 방문처리하고,큐에 넣는다.
3.큐가 비어질때까지 반복한다.
</code></pre>
<p>BFS에서는 다음과 같은것들을 신경써줘야한다.</p>
<ul>
<li>방문한 노드는 방문처리를 해준다.</li>
<li>queue를 활용하여 구현한다.</li>
<li>노드의 연결관계를 잘 설정해주어야한다.</li>
</ul>
<p>BFS가 탐색하는 순서를 출력하는 알고리즘을 통해 BFS의 기초를 알아보자.</p>
<h3 id="구현">3. 구현</h3>
<pre class=" language-cpp"><code class="prism  language-cpp">
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;iostream&gt;</span></span>
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;vector&gt;</span></span>
<span class="token macro property">#<span class="token directive keyword">include</span> <span class="token string">&lt;queue&gt;</span></span>

<span class="token keyword">using</span> <span class="token keyword">namespace</span> std<span class="token punctuation">;</span>


<span class="token keyword">bool</span> visited<span class="token punctuation">[</span><span class="token number">8</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token punctuation">{</span> <span class="token number">0</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
vector<span class="token operator">&lt;</span><span class="token keyword">int</span><span class="token operator">&gt;</span> a<span class="token punctuation">[</span><span class="token number">8</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">void</span> <span class="token function">bfs</span><span class="token punctuation">(</span><span class="token keyword">int</span> x<span class="token punctuation">)</span>
<span class="token punctuation">{</span>
	queue<span class="token operator">&lt;</span><span class="token keyword">int</span><span class="token operator">&gt;</span> q<span class="token punctuation">;</span>
	q<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">;</span>
	visited<span class="token punctuation">[</span>x<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
	
	<span class="token keyword">while</span> <span class="token punctuation">(</span>q<span class="token punctuation">.</span><span class="token function">empty</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token boolean">false</span><span class="token punctuation">)</span>
	<span class="token punctuation">{</span>
		<span class="token keyword">int</span> index <span class="token operator">=</span> q<span class="token punctuation">.</span><span class="token function">front</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		q<span class="token punctuation">.</span><span class="token function">pop</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		cout <span class="token operator">&lt;&lt;</span> index<span class="token punctuation">;</span>

		<span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">;</span> i <span class="token operator">&lt;</span> a<span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">size</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> i<span class="token operator">++</span><span class="token punctuation">)</span>
		<span class="token punctuation">{</span>
			<span class="token keyword">if</span> <span class="token punctuation">(</span>visited<span class="token punctuation">[</span>a<span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">]</span> <span class="token operator">==</span> <span class="token boolean">false</span><span class="token punctuation">)</span>
			<span class="token punctuation">{</span>
				q<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>a<span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
				visited<span class="token punctuation">[</span>a<span class="token punctuation">[</span>index<span class="token punctuation">]</span><span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
			<span class="token punctuation">}</span>
		<span class="token punctuation">}</span>

	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">int</span> <span class="token function">main</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token punctuation">{</span>
	a<span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	a<span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

	a<span class="token punctuation">[</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	a<span class="token punctuation">[</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	a<span class="token punctuation">[</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">5</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

	a<span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	a<span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">6</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	a<span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">.</span><span class="token function">push_back</span><span class="token punctuation">(</span><span class="token number">7</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

	<span class="token function">bfs</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">return</span> <span class="token number">0</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="bfs-참고문제">4. BFS 참고문제</h3>
<p>다음 문제를 풀어보자!</p>
<ul>
<li>
<p>바이러스 : <a href="https://www.acmicpc.net/problem/2606">https://www.acmicpc.net/problem/2606</a></p>
</li>
<li>
<p>단지번호 붙이기 : <a href="https://www.acmicpc.net/problem/2667">https://www.acmicpc.net/problem/2667</a></p>
</li>
<li>
<p>보물섬 : <a href="https://www.acmicpc.net/problem/2589">https://www.acmicpc.net/problem/2589</a></p>
</li>
<li>
<p>토마토 : <a href="https://www.acmicpc.net/problem/7576">https://www.acmicpc.net/problem/7576</a></p>
</li>
<li>
<p>N-Queen : <a href="https://www.acmicpc.net/problem/9663">https://www.acmicpc.net/problem/9663</a></p>
</li>
</ul>
</div>
</body>

</html>
