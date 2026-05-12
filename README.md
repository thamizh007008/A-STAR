<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: THAMIZHARASI J</h3>
<h3>Register Number: 212224060279       </h3>
<H3>Aim:</H3>
<p>To Implement A* Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
    ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
      successor.f = successor.g + successor.h

     iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor
     iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
end (for loop)
  
    e) push q on the closed list
    end (while loop)

# Program
```
import heapq

# -------------------------
# A* Search Function
# -------------------------
def a_star(graph, heuristics, start, goal):
    open_list = []
    heapq.heappush(open_list, (0, start))  # (f, node)

    parent = {start: None}
    g_cost = {start: 0}
    closed_list = set()

    while open_list:
        f, current = heapq.heappop(open_list)

        if current == goal:
            # Build final path
            path = []
            while current is not None:
                path.append(current)
                current = parent[current]
            return path[::-1]

        closed_list.add(current)

        for neighbor, cost in graph[current]:
            temp_g = g_cost[current] + cost
            temp_f = temp_g + heuristics[neighbor]

            # If neighbor already in closed with better f -> skip
            if neighbor in closed_list and temp_f >= g_cost.get(neighbor, float('inf')):
                continue

            # If better path found -> update
            if temp_f < g_cost.get(neighbor, float('inf')):
                parent[neighbor] = current
                g_cost[neighbor] = temp_g
                heapq.heappush(open_list, (temp_f, neighbor))

    return None



# -------------------------
# MAIN PROGRAM
# -------------------------

# Read number of nodes and edges
n, e = map(int, input().split())

graph = {}

# Read edges
for _ in range(e):
    line = input().strip()
    while line == "":      # Skip empty lines
        line = input().strip()

    u, v, w = line.split()
    w = int(w)

    if u not in graph:
        graph[u] = []
    if v not in graph:
        graph[v] = []

    # Undirected graph
    graph[u].append((v, w))
    graph[v].append((u, w))

# Read heuristics
heuristics = {}
start_node = None
goal_node = None

for idx in range(n):
    line = input().strip()
    while line == "":      # Skip empty lines
        line = input().strip()

    node, h = line.split()
    h = int(h)

    heuristics[node] = h

    if idx == 0:
        start_node = node  # First node is start

    if h == 0:
        goal_node = node   # Node with heuristic 0 is goal


# Run A* Search
path = a_star(graph, heuristics, start_node, goal_node)

print("Path found:", path)

```
<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'E', 'D', 'G']
<hr>
<h2>Output:</h2>
<hr>
<img width="869" height="481" alt="image" src="https://github.com/user-attachments/assets/e7ad8f42-243f-40d5-80bc-ceed18433d4f" />


<hr>
<h2>Result:</h2>
<hr>
  A* Search algorithm for a Graph using Python 3 is implemented.
