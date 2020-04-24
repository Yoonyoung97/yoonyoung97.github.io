## [ML] Search Algorithm::Uninformed Search - [1]

#### Uninformed Search 

  Uninformed Search는 목표 스테이트 까지 도착하는 데  어떤 노드부터 전개해야하는 지 우선순위를 알지 못한다. 그렇기에 탐색에 성공하였더라고하더라도 걸리는 시간이 일정하지 않고 들쭉날쭉하다.  대부분은 **FIFO/LIFO queue**를 이용하여 Search를 구현 한 경우가 이에 해당한다. 가장 기초적인 Uninformed Search를 밑에서 이야기 해 볼 예정이다.



**Frontier : 앞으로 전개할 노드들이 저장되어 있는 자료구조**

**Explored set : 중복을 피하기 위해 다녀간 노드를 저장하는 자료구조 **

**b :: the branching factor or maximum number of successors of any node **

**d ::  the depth of the shallowest goal node**

**m :: the maximum length of any path in the state space**



##### 1. Breadth-fisrt Search(BFS)

​	**Breadth-first Search**은 우리말로 '넓이 우선 탐색' 으로 가장 얕은 노드들을 전개하는 알고리즘으로 **Frontier는 FIFO queue**를 이용하여 구현한다. 

![BFS](C:\Users\USER\workspace\yoonyoung97.github.io\assets\img\BFS.png)

​	위의 그림에서 보듯이  A 노드를 확장하기전 목표 상태인지 검사 후 확장하여 확장한 노드들을 프론티어에 집어 넣는다 . 이걸 의사코드로 표현 하자면 

```pseudocode
function BFS(problem) return a solution, or failure
	PATH-COST = 0
	node = problem.INITIAL_STATE
	if problem.GOAL-TEST(node.STATE) then return SOULUTION(node)
	frontier = Queue.add(node)
	explored = Set()
	loop do 
		if EMPTY?(frontier) then return failure
		node = POP(frontier)
		add node.STATE to explored
		for each action in problem.ACTIONS(node.STATE) do
			child = CHILD_NODE(problem,node,action)
			if child.STATE is not in explored or froniter then
				if problem.GOAL_TEST(child.STATE) then return SOLUTION(child) // **
				frontier.add(child)
```

이런 식으로 표현 할 수 있다 . 여기서 가장 눈 여겨볼 점은 뒷부분 주석처리한 부분으로 프론티어에 넣기 전 검사하는 점이다. 이것은 자식노드에 목표상태가 있을 경우에 비효율적인 알고리즘으로 이를 보완한 XXX 알고리즘이 있다.

###### 평가 

1. Complete and Optimal

   Breadth-First-Search는 솔루션이 존재한다면 반드시 그 해답을 찾을 수 있고, 모든 비용이 같다고 했을 때 최적해를 반드시 찾을 수 있다.

2. Complexity

   복잡도는 SEARCH를 어떻게 구현하는게 따라 나뉜다. 	

   `TREE-SEARCH`으로 구현할  경우 공간 복잡도와 시간 복잡도 $$O(b^d)$$이다. 반면에 `GRAPH-SEARCH`기반으로 구현 할 경우 **공간복잡도**는 $$explored\;set$$의 사이즈인  $$O(b^d -1)$$ $$frontier$$ 의 사이즈 인 $$O(b^d)$$를 합친 것 으로 공간복잡도는  `TREE-SEARCH`기반 구현 보다 조금 불리하지만, **시간복잡도**에서는 다르다.

   ​	**시간 복잡도**에서 바라보면 `TREE-SERACH` 같은 경우 중복을 방지하는 $$explored\;set$$이 없기 때문에 중복해서 나오는 노드를 계산한다. 하지만 `GRAPH-SERACH` 같은 경우 중복을 방지하는 $$explored \;set$$이 존재하기 때문에 시간복잡도는 `TREE-SEARCH`기반보다 `GRAPH-SERACH` 는 우수하다. 



결국 복잡도가 지수적으로 커지기때문에 현실에서 쓰기엔 무리가 있다.



##### 2. Uniform-cost Search

​	Uniform-cost Search 는 Breadth-first Search에 step-cost 개념을 도입하여 나온 알고리즘이다. 중요한 것은 세가지이다.

1.  Step-cost를 사용하기 때문에 Priority Queue를 사용하여야한다.
2.  지나온 노드가 최저비용이 아닐수도 있기 때문에 Redundant Path를 허용할 방법이 필요하다.
3.  least-cost를 찾는 전제조건은 비용이 음수면 안된다.

  다른 Uninformed Search들과 다르게 Priority Queue를 이용하여 탐색하지만 전체 중에 가장 작은 비용를 찾는 것은 아니라 지나온 노드 중 가장 작은 비용을 찾는 것이기 때문에 Informed Search라곤 보기 어렵다.

#####  ![UCS](C:\Users\USER\workspace\yoonyoung97.github.io\assets\img\UCS.png)

위 그림은 Uniform-cost Search가 어떻게 작동하는지 보여주는 그림이다. 이 그림을 토대로 의사코드를 짜보면 

```pseudocode
function UNIFORM-COST-SEARCH(problem) return a solution, or failure
	PATH-COST = 0
	node = problem.INITIAL_STATE
	frontier = PriorityQueue.add(node)
	explored = Set()
	loop do 
		if EMPTY?(frontier) then return failure
		node = POP(frontier)
		if problem.GOAL-TEST(node.STATE) then return SOULUTION(node)
		add node.STATE to explored
		for each action in problem.ACTIONS(node.STATE) do
			child = CHILD_NODE(problem,node,action)
			if child.STATE is not in explored or froniter then
				frontier.add(child)
			else if child.STATE is in frontier with higher PATH-COST then
				replace that frontier node with child
```

위의 의사코드를 보면 GOAL-TEST가 Node를 전개하기 직전에 존재한다는 것을 알 수 있다. 그 이유는 목표상태에 도달한다고 해도 최저비용인지 모르기 때문에 다른것도 전개해봐야 알기 때문이다.



###### 평가

 1. Optimal and complete

    각 비용이 양수에 한해서 최적해를 찾을 수 있으며,  솔루션이 존재하면 반드시 찾을 수 있습니다.

	2. Complexity

    위의 BFS와 똑같이 최저비용이 아닌 노드의 중복을 피하기 위해서 explored set을 사용해야 효율이 좋다는 것어림짐작할 수 있습니다. 그리하여 `Graph-Search` 방식으로 구현하는게 더 효율적입니다.

    시간 & 공간 복잡도 : $$O(b^{1+[C^*/cost]})$$ [여기서 C*은 최적해의 코스트 비용입니다.]