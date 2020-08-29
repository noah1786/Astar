# A*

##### *(Vers. 0.4)*

## What?

[A*](https://en.wikipedia.org/wiki/A*_search_algorithm) is a popular pathfinding algorithm, often used in games and the like. This is my implementation of it.

It has a pretty great O(x) computational time, (Though not so great memory-wise, and I can't promise my implementation is very efficient *yet*).

Its' use is with node networks, so while it'll work on a 2d grid, it can do much more.


## Why?

Well, it's a really simple procedure for what it's trying to get done, so I personally believe it'd be a shame if you don't try your hand at it.
I have a few times, but all my other attempts have relied on a 2d grid. That may mean less clock cycles, but at the expense of many use cases.

And some of those, I've been thinking of as a side-project.

For instance, I'd like to fit it to a web-crawler (Although, admittedly that might devolve into djikstra or a binary search if I can't get a good heuristic) to find the closest link between two people on facebook, or two pages on Wikipedia.

And if I'm going to have such a good time doing this, why not share it with the greater community?

## How?

##### *(Until version 1.0, this is subject to change.)*

Well, you can look at the code if you're interested in the specific mechanics, but the general idea is this:

`astar` is a function that takes a starting node, an ending node, a gscore function, and an hscore function.

The gscore and hscore functions, as expected, take two nodes and returns the hscore and gscore btween them.

There's this struct "node" that looks as so

```C
typedef struct node {
	void* data;
	astar_data a_data;
} node;
```

"data" would, in most cases, be position. In my use-case, I'm thinking of it being links.
Just whatever you want to associate the node with other than fscore, gscore, etc.
`a_data` is all for astar(It's defined in `astar.h` if you want to look at it), and for the most part can be zeroed out(So initializing with calloc is recommended).

in a_data, you can connect it to other nodes. `node.a_data.connected_nodes` should be a list of nodes, and `node.a_data.num_nodes` the length of that list.

Additionally, if you want any node to be entirely blocked off as a 'wall', you can initialize
`node.blocked` to 1.

`astar` returns nothing. Instead, the pointer `endnode.breadcrumb` will be another node(or NULL if the a* failed to get a path). Keep on dereferencing breacrumbs until you're back to the startnode, and that'll walk you through the optimal path.
