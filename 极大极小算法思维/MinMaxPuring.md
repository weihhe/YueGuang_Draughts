### 极大极小算法(Min-Max)和负极大值(Negamax)剪枝(Pruning)

#### 极大极小（Min-Max）

伪代码：

MinMax(node)

 	if  node is  a terminal node 

​		return value of the node 

​	if node is a MAX

​		maxValue =  - ∞

​		for(all the child node)

​				bestValue = max(bestValue,MinMax(child node))

​	else node is a MIN

​		maxValue =  +∞

​		for(all the child node)

​				bestValue = min(bestValue,MinMax(child node))

return bestValue

#### Neg-max（负极大值）

伪代码：

NegMax(node)

 	if  node is  a terminal node 

​		return value of the node 

​		maxValue =  - ∞

​		for(all the child node)

​				bestValue = max(bestValue,-NegMax(child node))

#### pruning——假设我们是阿尔法（Max） 对手是(Min)

**Max 层维护 α ， Min 层维护 β** 

α：我们遍历我们的子节点，找到最大的值，保留下他的值（bestValue的值）

β：对手遍历该层的子节点  找到最小的子节点 保留下他的值（bestValue的值）

当 Max 寻找α的时候 如果发现 α>=β 则说明我们让对手获利（因为我们的下一层是Min，而这时候有β的较小值），这步并不合算，于是不再遍历此子树。

当Min 当 Max 寻找α的时候 如果发现 α>=β 则说明我们让对手获利（因为我们的下一层是Max，而这时候有α的较大值），这步并不合算，于是不再遍历此子树。

伪代码 

Func ABminmax(bestValue,a,b)

​	if(node is a terminal node)

​		return gameValue;

​	if node is a Max 

​		bestValue = -∞

​			for( chirld node)

​				gameValue = ABminmax(bestValue,a,b))

​				bestValue = max(bestValue,gameValue);

​				α = max(bestValue,α);

​				if（α>β）

​					break;

​	else

​		bestValue = -∞

​		for（chirld node）

​			gameValue = ABminmax(bestValue,a,b))

​			bestValue = min(bestValue,gameValue);

​			β = min(bestValue,β);

​			if（α>β）

​				break;

​	return bestValue;

#### Neg-puring——不完全

Func Negminmax(bestValue,a,b)

​	if(node is a terminal node)

​		return gameValue;

​		bestValue = -∞

​			for( chirld node)

​				gameValue =     Negminmax(bestValue,a,b))

​				bestValue = max(bestValue,gameValue);

​				α = max(bestValue,α);

​				if（α>β）

​					break;

​	return -bestValue;

