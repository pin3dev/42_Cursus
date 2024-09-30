## Algorithm Applied <a id="apply"></a>

> Below is an explanation of the features for automating the algorithm,  
to see animations of how the code works, see next page.  

### 1. List Builder <a id="builder"></a>

> ℹ️ The following steps must be executed argument by argument in sequence. 

* **_Step 1:_**  
Using `ft_atoi`, it transforms the arguments (`char*` into `int`).   
* **_Step 2:_**  
Creates a node storing the integer value.
* **_Step 3:_**  
Finally, adds the node to the end of the linked list (stack A).  

> 🚨 Although it is not supposed to deal with inputs in single strings (like `"3 -1 2 10 0"`), implementing this was not a big challenge, you just need to add the initial steps of checking the number of args, and use `ft_split` to split into several arguments.  

> 🚨 Initially the second linked list (_stack B_) is composed only of the head that points to `NULL`, making it an empty stack.

### 2. Content Checkers <a id="checkers"></a>
> ℹ️ Once the linked list has been created, it is traversed node by node, checking that the values comply with certain rules 

* **_Step 1:_**  
Checks if there are any repeated integer values in stack A, using the _"ft_check_doubles"_.  
* **_Step 2:_**  
Checks if stack A is already sorted, using the _"ft_check_sorted"_.  

### 3. Sort Type Classifier <a id="classifier"></a>
> ℹ️ Checks the size of the stack to classify the best sorting type.  

| size | steps |
|:----:|:-----:|
| 2    | `sa`  |
| 3    | `sort_three_case` |
| 4    | `pb`+`sort_three_case` |
| >= 5 | `big_sort_case`+`sort_three_case` |  

> 🚨 The return algorithm from stack A to stack B is called at the end of the case classification 

### 4. Big Sort Algorithm Brain <a id="brain"></a>
> ℹ️ I used some features to store important data in the nodes that will automatically determine how the algorithm should run

* **_Feat 1: Index_**  
Ordered sequence of integers starting at `0` spaced one by one up to `N`, referring to the position of the node in the stack, with `0` being the top and `N` the bottom. Important for the next feats calculations.  

<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_1.jpg" width="300" height="300" />
</p>

* **_Feat 2: Mov_**  
Integer value that determines the smallest number of moves required to move the node to the top of its own stack.  

<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_2.jpg" width="300" height="300" />
</p>


> 🚨 Since the top has `index 0`, for nodes in the _first half_ of the stack the number of moves is their own index (to up moves), and for the rest, it will be the size of the stack minus its index (to down moves). 

* **_Feat 3: Mov_Orientation_**  
Binary value that determines the orientation of the moves required from this node to the top of the stack, with `0` being assigned for `up/rotation` moves, and `1` being assigned for `down/revrot` moves.  


<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_3.jpg" width="300" height="300" />
</p>

* **_Feat 4: Total_Mov_**  
It is the value in integer of moves required, in both stacks,  to the transfer and destination nodes to the top of their own stacks.  


<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_4_1.jpg" width="300" height="300" />

  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_4_2.jpg" width="300" height="300" />

  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/feat_4_3.jpg" width="300" height="300" />
</p>

> 🚨 In order to optimize the algorithm, the transfer and destination nodes are evaluated for having the same direction of movement, so that the stacks are moved together; if this is the case, the value of the `largest` is assigned as the "Total_Mov". Otherwise, the value assigned will be the `sum` of the individual movements of the two nodes.  


<!--
* **_Dest_Place_**  
It is a pointer to the node in another stack (stack B) which will be the intended destination of the current node (stack A), and is calculated following the rules of the [algorithm](https://github.com/pin3dev/42_Push_Swap/wiki/Algorithm). Although "dest_place" is not a feat, it is important for the future assignment of the "total_mov" feat.  

5.5. Best case
> Após todas atribuições anteriores, o best case percorre toda a stack a tentando encontrar o node com o total mov com menor valor, sendo esse o melhor caso -->

<p align="center">
 <a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/concepts.md"> Previous ⬅️ </a> •
<a href="#apply"> Top ⬆️ </a> •
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/extra.md">Next ➡️ </a>
</p>
