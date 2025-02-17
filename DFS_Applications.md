DFS Application
---

Table of Contents
---
- [Topological sorting](#topological-sorting)
  - [Ieiunium explicandum (Quick explanation)](#ieiunium-explicandum-quick-explanation)
    - [Complexity](#complexity)
    - [Explanation x Pseudo Code](#explanation-x-pseudo-code)
  - [Pure pseudo code](#pure-pseudo-code)
  - [Pseudo code commented](#pseudo-code-commented)
- [SCC (Strongly connected components)](#scc-strongly-connected-components)
  - [Ieiunium explicandum (Quick explanation)](#ieiunium-explicandum-quick-explanation-1)
    - [Exemplum](#exemplum)
  - [Algorithmus](#algorithmus)
    - [Complexity](#complexity-1)
  - [Gif](#gif)

# Topological sorting
Find a dependency order in a graph, to do so we will have to use a timed DFS
## Ieiunium explicandum (Quick explanation)
### Complexity
```
Over all complexity for matrices -> O(|V|^3)
Over all complexity for lists -> O(|V|+|E|)
```
### Explanation x Pseudo Code
```
|RECURSIVE FUNCTION| params (L,v,G,s)
I- set the vertex [s] to true in the visited [v] list 
II- loop through all successors [t] of the vertex [s] in the graph [G]
    |- if the current vertex [t] is not visited
    	|- call the RECURSIVE FUNCTION again
III- add the the vertex [s] at the beginning of  the order list [L]    
|GLOBAL FUNCTION| (G)
I- from 0 to the number of vertices perpare a list called visited [v] and set all the values to false
II- prepare an empty list [L] (this will contain the order)
III- loop through all the vertices of the Graph [for s in vertices of G]
   |- if the current vertex is not visited 
      |- call the RECURSIVE FUNCTION
IV- return L 
```
## Pure pseudo code
```py
def TopoRec(L,v,G,s):
 v[s] = true
 for t successors of s in G:
   if !v[t]:
     TopoRec(L,v,G,t)
 add s to the beginning of L


def TopoWarpper(G):
  for s vertex in G:
   v[s]= false
  L = []
  for s vertex in G:
   if !v[s]:
    TopoRec(L,v,G,s) 
return L	

```

## Pseudo code commented
```py
def TopoRec(L,v,G,s):
 # set the vertex [s] to true in the visited [v] list 
 v[s] = true
 # loop through all successors [t] of the vertex [s] in the graph [G]
 for t successors of s in G:
   # if the current vertex [t] is not visited
   if !v[t]:
     TopoRec(L,v,G,t)
 # add the the vertex [s] at the beginning of  the order list [L]
 add s to the beginning of L


def TopoWarpper(G):
  #Initialisation
  # from 0 to the number of vertices perpare a list called visited [v] and set all the values to false
  for s vertex in G:
   v[s]= false
  # prepare an empty list [L] (this will contain the order)
  L = []
  
  # Program
  # loop through all the vertices of the Graph [for s in vertices of G]
  for s vertex in G:
   # if the current vertex is not visited
   if !v[s]:
    # Call TopoRec
    TopoRec(L,v,G,s) 
return L	
```

# SCC (Strongly connected components)
## Ieiunium explicandum (Quick explanation)
A strongly connected components is the set of vertices $Cs$ of a given vertex $s$ where there is a path from $s to t$  and from $s to t$.

### Exemplum 
![SCCExample1](/Images/DFS_Applications/SCC_example_1.png)</br>
In this example we have the following sets.</br>
$Ca = {A,D,B}$</br>
$Ce = {E}$</br>
$Cc = {C,F}$</br>
$Cb = {A,D,B}$</br>
$Cf = {C,F}$</br>

## Algorithmus

To find a SCC we will need to run the $Kosaraju’s$ $algorithmus$ or what the teacher like to call it the $Magical$ $algorithmus$ 
```
I- Run a timed-DFS and order the vertices by decreasing end of
treatment in a list [L]. By doing so, you obtains the topological order
II- Compute the transpose of the Graph [Gt]. 
III- Run a DFS on [Gt] by topological order and save the returned values into sublist in a big list 
Note : every time the dfs run some values will be computed and you will be saving thos value in a sublist 
when the dfs finishes you save that sub list in a big a list.
example -> [[A,D,B], [C,F], [E]]
```
### Complexity
For matrices : $O(|V^2|)$</br>
For lists : $O(|V| + |E|)$
## Gif
![SCCExample2](/Images/DFS_Applications/SCC_example_2.gif)
