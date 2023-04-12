---
title: "Graph Traversal"
datePublished: Fri Dec 30 2022 10:53:42 GMT+0000 (Coordinated Universal Time)
cuid: clcaed4sv03i6ktnvfxd1edf5
slug: graph-traversal
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1672399248643/835bba8c-760b-477e-b9be-573fd6d77dcb.webp
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1672399313902/4e73e8e0-22f7-4cbc-a627-4b59e96d643c.jpeg
tags: data-structures, bfs, dfs, wemakedevs, graph-traversal

---

## Traversing

Let's imagine you have a puzzle🧩 with many pieces having arrows➡ on them that show you, where you can go next. To solve the puzzle, you have to visit every piece keeping in mind not to visit anyone twice. That's what ''Traversing'' the puzzle means.

## Graph Traversing

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672121934216/e028b82f-e11e-499d-87fc-7da31b103c36.png align="center")

Now consider the big puzzle as a `graph`, with different pieces as `nodes` and arrows as the `edges`. The process of visiting all the nodes in a graph(each node only once) is known as ***Graph Traversal***.

**There are two main types of graph traversal in data structures: *breadth-first search* (<mark>BFS</mark>)➡ and *depth-first search* (<mark>DFS</mark>)⤵️**

## Breadth-First Search -

Let's start with an example,

Breadth First Search for now just for the sake of explanation consider this as Big Festive Season (BFS)✨, don't give me a look👀 let me explain this.

Consider you are somewhere standing in-between and you have to visit all your loved ones for Christmas🎄, so the basic logic is, you have to go first to the closest house which is in your neighborhood then go ahead on and on.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385976252/de36ed56-e94f-41c4-850e-197e4dc1554f.jpeg align="center")

`0`\- **You**, `1,2,3,4,5`\- **Your loved ones💝** and `6` is **Your Home**🏡.

If you visit the 4th node first or the 5th node or start from somewhere in-between, Christmas eve will end and you might end up reaching your home soo late or maybe on the next day🥴.

But If you go with the <mark>bfs technique</mark> by visiting your neighbor first ie, `node 1` and `node 2` which is the nearest path say,(edge L0) from you, then go to the next street (Level1) `node 3`, `node 4` which is the neighbor of the previous node and then follows the path and so on. So you can reach your home (6) on time by visiting all the houses (nodes).

Also, take note📒 listed with all the names where you have to visit and tick them right✔️ after visiting each one. So that you shall not re-visit any of them even by mistake.

**\[Breadth First Search =&gt; Big Festive Season =&gt; Christmas🎅 =&gt; Visit Neighbours first\]**

Checklist✅ = you would keep track of which intersections you have already visited so that you don't accidentally go in a loophole.

\*You don't have to remember this, this is just for fun learning😜 So it just clicks on your mind🧠 what you have to do in bfs approach.

### **Algorithm:**

Consider the graph below:-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672222678573/fc83bad0-64fb-4e9c-8324-a01ef7b4a409.jpeg align="center")

Step 1- Create a queue and add the root `source` node (here we'll take `node0`) to it which is the current node.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672198141927/21196ecf-ab3f-4646-a009-5a86fe9c29e9.jpeg align="center")

F -&gt; `front` of the queue, R -&gt; `rear` of the queue.

Step 2 - Create an array list to track the visited nodes.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672198176350/83863912-657c-4f6a-939c-52f4a9cf0ce1.jpeg align="center")

Step 3 - Run the loop till the `queue` become empty

a. Remove the node from the queue and make it the `current` node

b. If the node is un-visited ie, `false` (by default) then, mark the current as visited ie,`true` and `print it.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672388023754/cc793784-a80f-4e46-9561-77ea69909e44.jpeg align="center")

c. Now, add all the neighbors of the current node `node 0` to the queue.

`Dry Run:`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386156185/012cf0a3-4ddc-4f13-af0e-df30f17861ac.jpeg align="center")

adding all the neighbors of `node 0` ie, `node 1` and `node 2` into the queue⬆.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386247214/dd61390d-f54e-45fc-a7fe-27c3f192fb5b.jpeg align="center")

when `node 0` is removed, the next node ie `node 1` becomes the current node of the queue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386385016/e17446e9-f764-4e02-a970-f8b9143ef2b3.jpeg align="center")

now, here the current node is `node 2` ⬇,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386462667/5eca5c8e-2943-4459-805c-c01874f804ae.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386578290/7b6688bf-db7a-46b1-a52d-c6c3f2ff2b24.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672204926274/5322eb3a-85f4-4072-abef-6d977764a18f.jpeg align="center")

now the current node is `node 3` ⬇

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386655100/53e306d2-0b60-455d-b74f-93286d8d9f80.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386819009/06cb5a3c-d944-4275-b008-cf29c52533ff.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672386931177/e644af0e-5889-4f92-9008-a480a7e28159.jpeg align="center")

here the current node will be `node 4`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672387016799/3328908e-fbfe-454f-a188-7dc81ea176ab.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672387063513/fffb6c34-a6db-44be-832d-4539810bf8cd.jpeg align="center")

current node = `node 5`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672387153773/db50e31a-829b-4981-a3a1-a9324a51fb19.jpeg align="center")

now, `q.remove()` the curr node ie `2`, node `3`, node `5`, node `3`, node `4` and node `6`

and do nothing as it is visited nodes.

now `q.remove()` the curr node ie `6`

mark it `vis[curr]` - true. and `print`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672387236335/e8720149-48f1-471a-8b2f-eed853301e1c.jpeg align="center")

by adding the neighbor of `node 6`, `node 5` added to the queue

Simply do `q.remove()` for `curr node 5` and as it is already `visited`, do nothing.

Step 4 - When the queue becomes empty, bfs is done!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672218229071/2a1dace7-85b3-4a3e-bcd8-86cd588f9914.jpeg align="center")

the final `queue` will look like this -

<mark>output</mark>:- `0 1 2 3 4 5 6`

---

## Depth-First Search -

Let's dive into an example as we did above

Consider DFS as Digging Floor, I know I know! please bear with me for a while😅.

Imagine you just got to know about a treasure🎁 that is 30ft below where you're standing right now😵. Now you just start digging and digging, and digging until you get it. Then you turn around (backtrack) and follow another path until you reach the end again.

That's basically what DFS is all about. It's like following the branches of a tree🌴 and going as up as you can to get a good view😁 of your neighborhood. Then you turn around and follow another branch (path) until you reach the end. You keep doing this until you finally reach the very top of the tree.

%[https://twitter.com/i/status/744529115827609600] 

And don't forget to keep the track of your visited path (nodes) to avoid the loophole.

### Algorithm:

Step 1- Here we do `recursion` that uses `stack` implicitly.

Step 2 - Create an `array list` to track the `visited` nodes.

Step 3 - If the `node` is un-visited ie, `false` (by default)

a. Print the node: `print`

b. Mark it visited `vis[curr]` = `true`

Step 4 - Check for all the neighbors

`if` the node is un-visited -&gt; `print` and `vis[curr]` - `true`

`else` -&gt; do nothing

Step 5 - If all the neighbors are visited then backtrack.

`return`

Considering the same graph of bfs here also, so that we can differentiate better:-

`Dry run` :-

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672369451366/8572b19f-adcd-4b96-b944-b6c10b543837.jpeg align="center")

Let's take `node 0` as our `source node`

As we're using recursion and the node is not visited, it will go inside the `stack s,`

`Print` the current `node 0` and mark it as `visited` ie, `true`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672378139601/2c5e0b61-3fe8-4386-852f-bc9163c78a09.jpeg align="center")

Now, visit all the 0's neighbors ie, `node 1` and `node 2`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672378327465/03e3d717-189b-4775-a828-37f5f83413f3.jpeg align="center")

The recursion call goes for `node 1` and it will be added to the stack

`Print` the current `node 1` and mark it as visited `true`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672378697770/56e24444-593a-4e32-8a89-89cef3100369.jpeg align="center")

As we're on node 1, it will look for its neighbors ie, `node 0` and `node 3`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385192025/3f0b20b6-5197-42b5-b322-db7d20dbb95e.jpeg align="center")

here, `node 0` is already visited so it will not go inside the stack again and won't be printed twice. The next <mark>neighbor</mark> of `node 1` is `node 3`, so it will call `node 3` .

`Print` the current `node 3` and mark it as visited `true`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672378987694/434f6858-3ec4-4a40-9bd2-68f1506250c6.jpeg align="center")

Now, we're on `node 3`, so it will visit all the neighbors ie, `node 1`, `node 4` and `node 5`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385490985/2f344ebc-7e5a-4de2-9800-13331337b668.jpeg align="center")

As `node 1` is already <mark>visited</mark>, the <mark>call</mark> will go for the node that is `node 4`.

`Print` the current `node 4` and mark it as visited `true`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672379449719/322ddd96-c73b-4c99-84ef-e84334852a41.jpeg align="center")

Now, we're on `node 4`, it will visit the neighbors ie, `node 2`, `node 3` and `node 5`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385436975/2c782c10-2ca4-4a76-b3e7-398c6beb09a3.jpeg align="center")

The call will go for `node 2` so it will be added to the stack

`Print` the current `node 2` and mark it as visited `true`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672379748495/1672d596-f0fa-4256-b080-0526aa25f4e6.jpeg align="center")

As we're on `node 2`, it will check for all the un-visited neighbors

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385591060/f8857587-e4b5-476a-9998-1bb014d373c7.jpeg align="center")

here, all the neighbors are visited ie, `node 0` and `node 4`.

So `backtrack` occurs and `node 2` will be removed from the stack

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672380038535/b594cc43-51dc-4260-9b49-69d66dc0e6cd.jpeg align="center")

Now, `node 4` will check for its leftover neighbor ie, `node 3` which is already <mark>visited</mark>.

So the next call it will make is for `node 5` .

`Print` the current `node 5` and mark it as visited `true`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672380365356/d420117b-07c6-47a0-8f60-68e430156271.jpeg align="center")

As of now, we're on `node 5`, it will check for the neighbors ie, `node 3`, `node 4` and `node6`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385665307/5c71241d-348a-4172-85dd-342fa05d332a.jpeg align="center")

here, `node 3` and `node 4` both are <mark>visited</mark> already so it will call for `node 6` .

`Print` the current `node 6` and mark it as visited `true`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672380676816/333bd5f9-6d10-45c9-a306-a7b93d4ad9c8.jpeg align="center")

Now, we're on `node 6`, it will check all the neighbors of itself.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672385758564/50de90b3-4eb5-47cd-8097-c4af74efbd00.jpeg align="center")

the neighbor of `node 6` is `node 5` which is already <mark>visited</mark>.

So it will simply `return` from the stack.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672381185906/cb4099de-2cae-4e8f-8e72-e1d83a32a6e2.jpeg align="center")

Now, `node 5` will check for its un-visited node.

In this case, there is no node left out to visit. So it will be <mark>removed</mark> from the stack.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672381485710/2a4520c3-c7be-42a2-b9ea-e01db583bd35.jpeg align="center")

Now `node 4`, there is nothing left to visit, so `return`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672381887651/5d900d3a-3c84-47f2-b045-a2339d85f212.jpeg align="center")

Also for now `node 3`, simply `return` from the stack as no neighbor left <mark>un-visited</mark>

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672381913654/941d90a3-74d2-4742-9d12-1c282c2d6a10.jpeg align="center")

The same procedure follows for `node 1` and it will be removed from the stack

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672381947918/abdb1eea-ba94-407c-8c7a-eea159010666.jpeg align="center")

Now the last node in the stack here is `node 0`, check for an un-visited neighbor, and if nothing is left then simply `return` from it.

So, `stack s` will become empty.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1672382100376/b97434fb-369b-41ee-8b3c-7e290cbada35.jpeg align="center")

So, our final <mark>output</mark> will `print` -&gt; `0 1 3 4 2 5 6`.

---

### Pseudocode BFS:

```plaintext
function bfs( graph, node )
  stack = new Queue()
  queue.enqueue( node )

  while (queue.notEmpty())
    currentNode = queue.dequeue()

    if (!currentNode.visited)
      currentNode.visited = true

      while ( child = graph.nextUnvisitedChildOf( node ) )
        queue.enqueue( child )
```

### Java Code:

```java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.List;

public class BFS {

    public void search(List<List<Integer>> graph, boolean[] visited, int start) {
        Deque<Integer> queue = new ArrayDeque<>();
        visited[start] = true;
        queue.add(start);

        while (!queue.isEmpty()) {
            int vertex = queue.poll();
            for (int neighbor : graph.get(vertex)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }
}
```

---

### Pseudocode DFS:

```plaintext
function dfs( graph, node )
  stack = new Stack()
  search(node)

  function search( node )
    if ( !node )
      return

    if ( !node.visited )
      stack.push( node )
      node.visited = true

    if ( graph.nodeHasUnvisitedChildren( node ) )
      search( graph.nextUnvisitedChildOf( node ) )
    else
      search( stack.pop() )
```

### Java Code:

```java
import java.util.List;

public class DFS {

    public void search(List<List<Integer>> graph, boolean[] visited, int vertex) {
        visited[vertex] = true;
        for (int neighbor : graph.get(vertex)) {
            if (!visited[neighbor]) {
                search(graph, visited, neighbor);
            }
        }
    }
}
```

(Source: [Visual-Graph-Algorithm](https://workshape.github.io/visual-graph-algorithms/))

---

## Interesting Facts💡:

### **BFS** -

* BFS was first described by E.F. Moore in a paper published🧾 in 1959, where it was used to find the shortest path between two vertices in a graph.
    
* In fact, the famous mathematician Leonhard Euler used a similar technique in the 18th century to solve the famous Seven Bridges of Königsberg problem, which asked whether it was possible to walk through the city of Königsberg⛳ (now Kaliningrad) and cross each of its seven bridges exactly once.
    
* Euler's solution involved representing the city as a graph and using a breadth-first search to determine whether a solution was possible.
    

**<mark>Use Cases:</mark>**

* BFS is often used to solve puzzles🧩 that involve searching for a particular state, such as finding a solution to a maze or solving a word ladder🔢.
    
* It can be used in networking🌐 to find all the reachable nodes in a network or to find the shortest path between two nodes in a network.
    
* It can be used to test whether a graph📈 is bipartite or not. A graph is bipartite if it can be divided into two sets of vertices such that every edge connects a vertex in one set with a vertex in the other set.
    

### **DFS -**

* DFS has been used in the field of psychology🧠 to study how people process and organize information.
    
* In one study, researchers used DFS to investigate how people👨‍👨‍👧‍👧 categorize words based on their meaning. They found that people tend to organize words into categories based on their common properties, rather than their characteristics and that this process follows a DFS pattern.
    
* This suggests that DFS may be a fundamental cognitive process that is used to understand and organize the world🌎 around us.
    

**<mark>Use Cases:</mark>**

* Tarjan used DFS to develop a linear-time↗ algorithm for finding the strongly connected⛓ components of a directed graph.
    
* It can be used to perform a [topological sort](https://iq.opengenus.org/topological-sorting-dfs/) on a directed acyclic graph (DAG).
    
* It is used in compiler design to find strongly connected components in a graph.
    
    ---
    

This blog was submitted for the "Data Structures" track-4 of the Hashnode and WeMakeDevs/CommunityClassroom December blogging challenge. Thanks to them for giving this opportunity. More blogs are coming your way of this series.

Thanks for clicking!❤️