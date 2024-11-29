<header>

# hw seven

Andrew Chang-DeWitt \
CS 430, Fall 2024 \
Nov. 30, 2024

</header>
<section>

## question one

:::{.reply}

> _(6 points) NASA wants to link n stations spread over the country using
> communication channels. Each pair of stations has a different bandwidth
> available, which is known a priori. NASA wants to select n-1 channels (the
> minimum possible) in such a way that all the stations are linked by the
> channels and the total bandwidth (defined as the sum of the individual
> bandwidths of the channels) is maximum. Give an efficient algorithm for this
> problem and determine its worst-case time complexity._

:::

<section>

### algorithm

Using <i>Kruskal's algorithm</i>, representing the stations & their
channels as a graph, `G`:

<pre>
<strong>MINIMUM-CHANNELS</strong> is
  <u>inputs</u>:  G <- (V, E), where
             V is all stations & |V| = n
             E is all channels, with weights w
           w <- list of weights for ∀ e ∈ E
  <u>outputs</u>: MST of G

  M <- ∅                          <span class="comment">// init an empty set to hold the MST</span>

  for each v ∈ G.V:               <span class="comment">// build a disjoint set forest</span>
    MAKE-SET(v)

  E <- list of edges in G.E       <span class="comment">// sort edges by weight</span>
  SORT(E, increasing by w(e))

  for each u, v in E do           <span class="comment">// loop over all edges</span>
    if FIND-SET(u) != FIND-SET(v) <span class="comment">// if vertex @ each end of the edge</span>
                                  <span class="comment">// is not in MST</span>
      M <- M ∪ {(u,v)}            <span class="comment">// then add edge to MST</span>
      UNION(u,v)                  <span class="comment">// and mark all v<sup>o</sup> ∈ V connected to u</span>
                                  <span class="comment">// as connected to all v<sup>o</sup> ∈ V connected</span>
                                  <span class="comment">// to v</span>
  return M
</pre>

</section>
<section>

### time complexity

Time complexity can be derived from Kruskal's algorithm as well, which has a
complexity of O(E lg V) in the worst case:

<pre>
∵ |V| === n,                      <span class="comment">// V is set of n stations</span>
  |E| === n(n - 1),               <span class="comment">// assuming each station is connected</span>
                                  <span class="comment">// to every other station</span>
  T(n) ∈ O(E lg V)                <span class="comment">// from CLRS</span>

  T(n) ∈ O((n(n - 1)) lg n)
       < O(n<sup>2</sup> lg n)

∴ T(n) ∈ O(n<sup>2</sup> lg n)
</pre>
</section>
</section>
<section>

## question two

:::blockquote{.reply}

_(6 points) Alternative minimum-spanning-tree algorithms: In this problem, we
give pseudo-code for three different algorithms. Each one takes a graph as
input and returns a set of edges T. For each algorithm, you must either prove
that T is a minimum spanning tree or prove that T is not a minimum spanning
tree. Also, describe the most efficient implementation of each algorithm,
whether or not it computes a minimum spanning tree._

:::

<section>

### algorithm a

:::blockquote{.reply}

<pre>
  <strong>MAYBE-MST-A(G, w)</strong>
<span class="ln">1</span>   sort the edges into nonincreasing order of edge weights w
<span class="ln">2</span>   T = E
<span class="ln">3</span>   for each edge e, taken in nonincreasing order by weight
<span class="ln">4</span>   do if T - {e} is a connected graph
<span class="ln">5</span>   then T = T – {e}
<span class="ln">6</span>   return T
</pre>

:::

</section>
<section>

### algorithm b

:::blockquote{.reply}

<pre>
  <strong>MAYBE-MST-B(G, w)</strong>
<span class="ln">1</span>   T = Ø
<span class="ln">2</span>   for each edge e, taken in arbitrary order
<span class="ln">3</span>   do if T + {e} has no cycles
<span class="ln">4</span>   then T = T + {e}
<span class="ln">5</span>   return T
</pre>

:::

</section>
<section>

### algorithm c

:::blockquote{.reply}

<pre>
  <strong>MAYBE-MST-C(G, w)</strong>
<span class="ln">1</span>   T = Ø
<span class="ln">2</span>   for each edge e, taken in arbitrary order
<span class="ln">3</span>   do T = T + {e}
<span class="ln">4</span>   if T has a cycle c
<span class="ln">5</span>   then let e' be the maximum-weight edge on c
<span class="ln">6</span>   T = T - {e'}
<span class="ln">7</span>   return T
</pre>

:::

</section>
</section>
<section>

## question three

:::{.reply}

> _(6 points) Suppose we are given a graph G = (V, E) and a source vertex s in
> V. If Dijkstra's Algorithm is to properly find the shortest path from start
> to goal, we must guarantee that all edge weights in E are nonegative. In
> detail explain why is this a necessary condition? Just showing an example is
> not sufficient._

:::

</section>
<section>

## question four

:::{.reply}

> _(10 points) Compute D(1), D(2), D(3), D(4) and D(5) using Floyd-Warshall
> algorithm to compute minimum weight paths between all vertices in the below
> graph. Also keep track of the predecessor vertices (last vertex in the
> shortest paths)._

:::

</section>
<section>

## question five

:::{.reply}

> _(6 points) How can the output of the Floyd-Warshall algorithm be used to
> detect the presence of a negativweight cycle? Explain in detail._

:::

</section>
<section>

## question six

:::{.reply}

> _(6 points) Let a directed acyclic graph G = (V, E) and vertices start, goal
> in V be given. Assuming all edges in E are of non-negative weight, describe an
> efficient algorithm for finding the longest (heaviest weight) path from start
> to goal._

:::

</section>
