---


---

<h1 id="dijkstras-shortest-path-first-algorithm">Dijkstra’s Shortest Path First Algorithm</h1>
<p>Consider that , you want to go to your friend’s house who lives in a different town and  you have number of different path to go  his house. Now if you want to go his house as soon as possible then obviously want to go via shortest path only. Now how to find shortest path? - Well you may think of calculating it manually but sometimes finding the shortest path may not be so easy that you can find it manually . In this article we are going to present a powerful technique to find out the shortest path.</p>
<h2 id="problem">Problem</h2>
<blockquote>
<p>Given a <strong>weighted  graph</strong> (where all edge weight is <strong>non negative</strong>) and a <strong>source vertex</strong> find shortest path from source to <strong>all other vertex</strong> in the graph.</p>
</blockquote>
<h2 id="example">Example</h2>
<p>For example consider the following graph —</p>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-9tZlTL4wvupLYRqF" width="100%" style="max-width: 379.86663818359375px;" viewBox="0 0 379.86663818359375 147.7916488647461"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M62.68845061924884,72.78254879852402L96.21665954589844,50.03749465942383L125.71665954589844,50.03749465942383" marker-end="url(#arrowhead2554)" style="fill:none"></path><defs><marker id="arrowhead2554" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M59.92536523636181,102.36230267563671L96.21665954589844,138.43331909179688L149.07498931884766,138.43331909179688L201.93331909179688,138.43331909179688L232.51598524261186,128.78312141077794" marker-end="url(#arrowhead2555)" style="fill:none"></path><defs><marker id="arrowhead2555" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M171.3506529409819,43.008527453968156L201.93331909179688,33.35832977294922L254.7916488647461,33.35832977294922L307.6499786376953,33.35832977294922L343.94127294723194,69.42934618910938" marker-end="url(#arrowhead2556)" style="fill:none"></path><defs><marker id="arrowhead2556" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M278.1499786376953,121.75415420532227L307.6499786376953,121.75415420532227L341.1781875643449,99.00910006622208" marker-end="url(#arrowhead2557)" style="fill:none"></path><defs><marker id="arrowhead2557" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M168.40511016514728,63.15077029327286L201.93331909179688,85.89582443237305L235.46152801844647,108.64087857147324" marker-end="url(#arrowhead2558)" style="fill:none"></path><defs><marker id="arrowhead2558" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" style="opacity: 1;" transform="translate(96.21665954589844,50.03749465942383)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">5</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(149.07498931884766,138.43331909179688)"><g transform="translate(-9,-13.358329772949219)" class="label"><foreignObject width="18" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">10</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(254.7916488647461,33.35832977294922)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">6</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(307.6499786376953,121.75415420532227)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">4</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(201.93331909179688,85.89582443237305)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">2</span></div></foreignObject></g></g></g><g class="nodes"><g class="node" style="opacity: 1;" id="A" transform="translate(43.35832977294922,85.89582443237305)"><circle x="-15.5" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5.5,-13.358329772949219)"><foreignObject width="11" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">A</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="B" transform="translate(149.07498931884766,50.03749465942383)"><circle x="-15" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5,-13.358329772949219)"><foreignObject width="10" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">B</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="C" transform="translate(254.7916488647461,121.75415420532227)"><circle x="-15.5" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5.5,-13.358329772949219)"><foreignObject width="11" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">C</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="D" transform="translate(360.50830841064453,85.89582443237305)"><circle x="-16" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-6,-13.358329772949219)"><foreignObject width="12" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">D</div></foreignObject></g></g></g></g></g></g></svg></div>
<p>In the above graph  let’s consider source vertex is <strong>A</strong> .<br>
Now,</p>
<ul>
<li>shortest path distance  from A to B is 5  and route is A-&gt;B</li>
<li>shortest path distance from A to C is 7 and route is A-&gt;B-&gt;C</li>
<li>shortest path distance from A to D is 11 and route is either A-&gt;B-&gt;D or A-&gt;B-&gt;C-&gt;D</li>
</ul>
<h2 id="simple-solution">Simple Solution</h2>
<p>Now let’s think how to solve it? Well, the obvious solution that first comes into mind that why don’t we consider all path from source to a vertex and find minimum among them and repeat this step for all vertex except the source vertex.<br>
<strong>Algorithm</strong>:</p>
<blockquote>
<p>for all vertex except the source<br>
find cost of all path from source to this vertex using DFS<br>
then find minimum among the cost</p>
</blockquote>
<p>Now let’s think of time complexity of this naive approach. For a single vertex we are applying DFS to find cost of all alternative path from source to it and then finding minimum among all the cost .Now the time complexity of DFS is O(V+E) where V is the number of vertex and E is the number of edges. So the overall time complexity is O(V*(V+E))  or  <span class="katex--display"><span class="katex-display"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><mi>V</mi><mo>∗</mo><mo stretchy="false">(</mo><mi>V</mi><mo>+</mo><msup><mi>V</mi><mn>2</mn></msup><mo stretchy="false">)</mo><mo stretchy="false">)</mo></mrow><annotation encoding="application/x-tex">O(V*(V+ V^{2}))</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span style="margin-right: 0.02778em;" class="mord mathdefault">O</span><span class="mopen">(</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">∗</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mopen">(</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1.11411em; vertical-align: -0.25em;"></span><span class="mord"><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.864108em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">2</span></span></span></span></span></span></span></span></span><span class="mclose">)</span><span class="mclose">)</span></span></span></span></span></span> as is dense graph |E| is order of V square.Now It  is very huge. It will eventually fail when you have a test case where |V| &gt;= 1000 .</p>
<h2 id="optimized-solution">Optimized Solution</h2>
<p>Now  lets think of some optimization. As we know in  <strong>Unweighted Graph</strong> we  can use simple BFS to find shortest path from source to all other vertex. Now can we think of some modification to simple BFS–</p>
<ul>
<li>First modification we can easily think of that in BFS we do dis[v]=dis[u]+1 for an edge e(u,v) but here we have to do <strong>dis[v]=dis[u]+weight(u,v)</strong></li>
<li>Now second thing is in BFS we maintained a queue and a  visited array to keep track of which vertex is visited before .If any vertex is visited before there we did not push the same vertex again but here scenario is different. Consider the following graph–</li>
</ul>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-ZdI6AXliOCvZJRqC" width="100%" style="max-width: 274.1499786376953px;" viewBox="0 0 274.1499786376953 124.43331909179688"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M62.68845061924884,82.32993517974747L96.21665954589844,105.07498931884766L125.71665954589844,105.07498931884766" marker-end="url(#arrowhead2576)" style="fill:none"></path><defs><marker id="arrowhead2576" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M62.68845061924884,56.1033839120494L96.21665954589844,33.35832977294922L149.07498931884766,33.35832977294922L201.93331909179688,33.35832977294922L235.46152801844647,56.1033839120494" marker-end="url(#arrowhead2577)" style="fill:none"></path><defs><marker id="arrowhead2577" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M172.43331909179688,105.07498931884766L201.93331909179688,105.07498931884766L235.46152801844647,82.32993517974747" marker-end="url(#arrowhead2578)" style="fill:none"></path><defs><marker id="arrowhead2578" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1px; stroke-dasharray: 1px, 0px;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" style="opacity: 1;" transform="translate(96.21665954589844,105.07498931884766)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">5</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(149.07498931884766,33.35832977294922)"><g transform="translate(-9,-13.358329772949219)" class="label"><foreignObject width="18" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">10</span></div></foreignObject></g></g><g class="edgeLabel" style="opacity: 1;" transform="translate(201.93331909179688,105.07498931884766)"><g transform="translate(-4.5,-13.358329772949219)" class="label"><foreignObject width="9" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">2</span></div></foreignObject></g></g></g><g class="nodes"><g class="node" style="opacity: 1;" id="A" transform="translate(43.35832977294922,69.21665954589844)"><circle x="-15.5" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5.5,-13.358329772949219)"><foreignObject width="11" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">A</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="B" transform="translate(149.07498931884766,105.07498931884766)"><circle x="-15" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5,-13.358329772949219)"><foreignObject width="10" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">B</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="C" transform="translate(254.7916488647461,69.21665954589844)"><circle x="-15.5" y="-23.35832977294922" r="23.35832977294922"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-5.5,-13.358329772949219)"><foreignObject width="11" height="26.716659545898438"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">C</div></foreignObject></g></g></g></g></g></g></svg></div>
<p>consider that A is source.Here if we maintain a queue and visited array then the problem is at step 1  - B,C will be pushed to queue and they will be marked as visited but so we can’t visit B again ,So final path from A to C will be of distance 10 . But If we visit B we get a better path that is of distance 7. So here visited array  is of no use and we also don’t require the queue as while a vertex is within the queue it distance can be updated.<br>
<strong>Now let’s think of a better solution–</strong><br>
let’s divide the vertices in two sets –</p>
<ul>
<li>one is set of all vertices whose shortest path is already decided (green vertex) and,</li>
<li>other is set of all vertices whose shortest path is not decided  (black vertex).</li>
<li>Now consider the below graph –<img src="https://i.imgur.com/556Gsm5.png" alt=""><br>
here you can see that there are edge possible between the green and black node (red edge) and edge possible between two black node(black edge).<br>
Now at each step we want to add one black node to green vertices  set. So in order to grow the green vertices set how to add new vertex to it? Well, we can consider only the red edge and try to find out the black  vertex which has minimum distance from green vertices  and add it to green vertices set. Why? — Because we know as the green vertices shortest path distance is already found out so if we now add a black vertex which is closet to some green vertex  then the added vertex’s shortest path distance can never  decrement in future , as  all the edge weight is positive so if we again come to this vertex again then it’s distance should be more than previous. So the <strong>Algorithm</strong> is:</li>
</ul>
<pre><code>Single Source Shortest Path(G, s)
begin
	S={}
	for all vertices v do
		d(v) = infinity; 
		p(v) = NIL;
	end-for
	d(s) = 0;
	V={all vertex}
	for |V| iterations do
		v=the vertex with least d() value among V \ S (black vertex)
		Add v to S
		for each neighbor w of v in V \ S do
			d(w) = min { d(w), d(v) + W(v,w) }
                end-for
        end-for
</code></pre>
<p>Now here at every step we are finding the least weight vertex from set V \ S so is there any data structure that support this need? Yes – <strong>Min Heap</strong>,<br>
in min heap we can extract minimum element in O(log n) time and after that we have to decrease the d() value of all the neighbor we can do it in O(log n) using decrease key method of min heap.<br>
So final <strong>Algorithm</strong> after incorporating heap is-</p>
<pre><code>DIJKSTRA(G,w,s)
S={}
for all vertices v do
	d[v] = infinity; 
	p[v] = NIL;
end-for
d[s] = 0;

Q&lt;-V[G] // push all vertex to Q

while(!Q.empty()) 

do 
	u=EXTRACT-MIN(Q)

	S=SU{u}

	 for each vertex v  Adj[u]
	 do
		  if d[v] &gt; d[u] + w(u,v)
		   then d[v] = d[u] + w(u,v)
			p[v]=u
         end for
end while

</code></pre>
<h2 id="code">Code</h2>
<p>For implementation purpose we can use STL multiset to implement dijsktra  as it is a ordered balanced binary tree (i.e the minimum element will be always on the front) so we can extract min in O(log n) (due to reordering of multiset’s tree).So here is the code . The code assumes that source vertex is vertex 1.</p>
<pre><code>/*Program for Dijsktra Single Source Shortest Path
  Written by : Ankush Mitra
  Date: 28.10.19 Time: 3.00 P.M */
#include&lt;bits/stdc++.h&gt;
using namespace std;
typedef long long int ll;
typedef pair&lt;ll,ll&gt; Des_Weight_Pair;
typedef pair&lt;ll,ll&gt; relaxedVal_node_Pair;//For relaxing ,   intially source  is already relaxed to 0

vector&lt;Des_Weight_Pair&gt;graph[100009];
ll vis[100009];
ll dis[100009];

void init()
{
	for(int i=0;i&lt;100009;i++)
	{
		graph[i].clear();
		vis[i]=0;
		dis[i]=INT_MAX;
	}
}
int main()
{
	ll no_of_test_case;
	cin&gt;&gt;no_of_test_case;
	while(no_of_test_case--)
	{
		ll no_of_node,no_of_edges;
		cin&gt;&gt;no_of_node&gt;&gt;no_of_edges;
		init();
		for(ll i=0;i&lt;no_of_edges;i++)
		{
			ll Source,Des,Weight;
			cin&gt;&gt;Source&gt;&gt;Des&gt;&gt;Weight;
			graph[Source].push_back({Des,Weight});//Making the Adjacency List
			//for undirected graph push two time
		}
	    multiset&lt;relaxedVal_node_Pair&gt;DijsktraHeap;
	    DijsktraHeap.insert({0,1});  //Asumming the statring node is 1
	    dis[1]=0;
	    while(!DijsktraHeap.empty())
	    {
	    	Des_Weight_Pair tem=*DijsktraHeap.begin();
	    	DijsktraHeap.erase(DijsktraHeap.begin());// O(log n) as set tree reorders 
	    	
	    	ll tem_node=tem.second;
	    	if(vis[tem_node]==1)
	    		continue;
	    	vis[tem_node]=1;
	    	for(int i=0;i&lt;graph[tem_node].size();i++)
	    	{
	    		Des_Weight_Pair new_node_pair=graph[tem_node][i];
	    		ll new_node=new_node_pair.first;
	    		ll w=new_node_pair.second;
	    		if(dis[new_node]&gt;dis[tem_node]+w)
	    		{
	    			dis[new_node]=dis[tem_node]+w;
	    			DijsktraHeap.insert({dis[new_node],new_node});
	    		}
                
	    	}

    	}
    	ll final_des;
    	cin&gt;&gt;final_des;
    	cout&lt;&lt;dis[final_des]&lt;&lt;endl;

	}
	
}
</code></pre>
<h2 id="time-complexity">Time Complexity</h2>
<p>Now lets analyze  the time complexity of Dijsktra  Algorithm :<br>
Now the initialization takes O(V). Now in each step we are doing extract-min (O(log v) using min-heap) and there are O(V) such operation  . We are also doing  decrease key operation (relax operation- O(log v) using min-heap)) and there will be total O(E) such operation . Hence the over all time complexity is –<br>
<span class="katex--display"><span class="katex-display"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi>O</mi><mo stretchy="false">(</mo><msup><mi>V</mi><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><mi>V</mi><mi>l</mi><mi>o</mi><mi>g</mi><mi>V</mi><mo>+</mo><mi>E</mi><mi>l</mi><mi>o</mi><mi>g</mi><mi>V</mi><mo stretchy="false">)</mo><mo stretchy="false">)</mo><mo>=</mo><mi>O</mi><mo stretchy="false">(</mo><mi>V</mi><mo>+</mo><mi>E</mi><mo stretchy="false">)</mo><mi>l</mi><mi>o</mi><mi>g</mi><mi>V</mi></mrow><annotation encoding="application/x-tex">
O(V^{2} + (V log V+ E log V))=O(V+E) log V
</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1.11411em; vertical-align: -0.25em;"></span><span style="margin-right: 0.02778em;" class="mord mathdefault">O</span><span class="mopen">(</span><span class="mord"><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.864108em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">2</span></span></span></span></span></span></span></span></span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mopen">(</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span style="margin-right: 0.01968em;" class="mord mathdefault">l</span><span class="mord mathdefault">o</span><span style="margin-right: 0.03588em;" class="mord mathdefault">g</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span style="margin-right: 0.05764em;" class="mord mathdefault">E</span><span style="margin-right: 0.01968em;" class="mord mathdefault">l</span><span class="mord mathdefault">o</span><span style="margin-right: 0.03588em;" class="mord mathdefault">g</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="mclose">)</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span style="margin-right: 0.02778em;" class="mord mathdefault">O</span><span class="mopen">(</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">+</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span style="margin-right: 0.05764em;" class="mord mathdefault">E</span><span class="mclose">)</span><span style="margin-right: 0.01968em;" class="mord mathdefault">l</span><span class="mord mathdefault">o</span><span style="margin-right: 0.03588em;" class="mord mathdefault">g</span><span style="margin-right: 0.22222em;" class="mord mathdefault">V</span></span></span></span></span></span></p>
<h2 id="remarks">Remarks</h2>
<p>Here In this post we have seen Dijsktra’s Single Source Path Algorithm.<br>
Here We have implemented it using multi set so the overall time complexity is O(V+E) log V but if we use fibbonacci heap which has decrease_key complexity as O(1) then the overall time complexity will be O(Vlog V+ E) which we will discuss in a separate post. Dijsktra Single Source Shortest Path Algorithm is useful in many practical scenario as in real life generally all edges of the graph will be positive.</p>

