## 🔃 Algorithm <a id="algo"></a>

### Theory

The Turkish Algorithm has a simple goal:
> ℹ️ To organize the numbers in stack A, push it in descending order into stack B (`pb`) and then bring them back to stack A, leaving it in ascending order (`pa`).  
 
<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/dec.gif" width="300" height="300" />
</p>


### Sorting Types

   #### 1. Sort Three

> ℹ️ For ordering up to 3 nodes it is not necessary to use stack B, with only internal rotation and swap movements being effective in all cases.

| case 1 | case 2 | case 3 | case 4 | case 5 |
|:------:|:------:|:------:|:------:|:------:|
|  `acb` |  `bac` |  `bca` |  `cab` |  `cba` |
| `1`,`3`,`2` | `2`,`1`,`3` | `2`,`3`,`1` | `3`,`1`,`2` | `3`,`2`,`1` |
| `swap`+`rot` | `swap` | `revrot` | `rot` | `swap`+`revrot` |


   #### 2. Big Sort
   > ℹ️ Sorting method for sorting a stack with more than 3 nodes. Here's the steps how the big sort works:

<!---
* **_Step 1:_**  
It starts by checking if stack A has more than 3 nodes (because for stacks with only 3 nodes or less, there is an optimized ordering of internal movements).  
--->

* **_Step 1:_**  
It pushes the first 2 nodes to stack B, one after the other, using the `pb` move.  

* **_Step 2:_**  
With the 2 new nodes in stack B, it determines which node has the `highest` and `lowest` integer _values_, marking them as the "new maximum value" and "new minimum value" in stack B.  

* **_Step 3:_**  
Next, the algorithm goes into a loop, searching only for the `best case` to move, found by each round, until only 3 nodes remain in stack A.   
 
> 🚨 The _"best case"_ It evaluates by considering which node in stack A have the lowest `Total_Mov`


<p align="center">
  <img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/fst_pbs.gif" width="300" height="300" />
</p>



   #### 2.1. Rules
> ℹ️ Some features have been added for the algorithm to run, and will be explained in the future, but these features depend on the concept of sorting the stack B, which follows two possible rules to determine the destination (`Dest_Position`) of the node to be transferred (stack A) into stack B.  

The "Dest_Position" rules:  
 * **_Rule 1:_**  
If the value of the node to be transferred (stack A) is less than the minimum value (`node < min`) or greater than the current maximum value in stack B (`node > max`), it is placed on `top` of the node with the `highest` value in stack B so far.  
 * **_Rule 2:_**  
If the value of the node does _not follow the previous rule_, it is placed on `top` of the node with the value `immediately lower` than it in stack B.  

### 3. Returning Ordination 

> ℹ️ To return from stack B to stack A (`pa`), it’s just moving the number from the `top` of stack B to its `Dest_Position` on stack A.    
It is important to mention that the entire `Dest_Position` logic is inverted, with the number always positioned at the top of the number `immediately greater` than it.  

> 🚨 Checking the “best case”, are dispensed with in this part of the algorithm.  

> ℹ️ Once all the nodes are back in stack A, find the min value, and according to the settings of the features (`Mov` and `Mov_Orientation`) rotate stack A until the node with this value is at the top.  

<p align="center">
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/remarks.md"> Previous ⬅️ </a> • 
<a href="#algo"> Top ⬆️ </a> • 
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/roadmap.md">Next ➡️ </a>
</p>
