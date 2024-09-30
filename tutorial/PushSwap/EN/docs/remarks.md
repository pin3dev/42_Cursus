## 🔎 Remarks <a id="remarks"></a>

### 📃 Subject

Based on [version 6 subject](https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Rdm/Push_Swap_subject.en.pdf) (updated in 2023) of [École 42's common core](https://42.fr/en/the-program/software-engineer-degree/) project,  
PushSwap's construction parameters and objectives are as follows:

1. Receive a list of integers that fills stack A, according to the order in which they were entered into stdin  

2. Sort all elements in stack A in ascending order, using as few moves as possible and stack B, if necessary.  
  
3. The program must print out a list of instructions for the moves required for sorting,  
the list being made up of the abbreviations of the moves followed always by a new line.

4. The program must check for input errors, such as non-integers or empty inputs.

5. At the end of the program, all memory dynamically allocated must be freed, avoiding memory leaks.

### Stack Filling Order

> 🚨 Note that the head of the first linked list (stack A), i.e. its top, is configured to point to the first value passed through the input.  
It's a strange approach, but one requested by the subject.  

Input example:
```bash
$~ ./push_swap 3 1 6 0
```  
Linked list order:
|HEAD| 1º | 2º | 3º | 4º | Nº |
|----|----|----|----|----|----|
| ➡️  |`3` |`1` |`6` |`0` |`...`|


> 🚨 Also, when moving nodes from the first list (stack A) to the second list (stack B),  
the linked lists should be considered as stacks, only removing and adding from the top (head).

Stack display:

|HEAD| ⤵️ |
|----|----|
|_top_|`3` |
|    |`1` |
|    |`6` |
|_base_|`0` |

### Moviments and Stacks

> 🚨 Only two stacks are allowed to use, the original stack A and stack supporting sort B.   
> 🚨 Only internal rotational movements in the stacks and the transfer of nodes from the top between the stacks are permitted. 

<!--
|STACK| swap↕️ | reverse-rotate↗️ | rotate↘️ | push➡️ |
|-----|------|----------------|--------|------|
|     |<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_swap.gif" width="250" height="250" />|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_reverserotate.gif" width="250" height="250" /> |<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_rotate.gif" width="250" height="250" />|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_push.gif" width="250" height="250" />  |
|  A  |`sa` |`rra` |`ra` |`pa` |
|  B  |`sb` |`rrb` |`rb` |`pb` |
| A&B |`ss` |`rrr` |`rr` | _none_ |  
-->

|MOVIMENTS| STACK A | STACK B | STACK A&B |  
|:-------:|:-------:|:-------:|:---------:|    
|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_swap.gif" width="250" height="250" /> | `sa` | `sb`| `ss` |  
|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_reverserotate.gif" width="250" height="250" /> | `rra` | `rrb`| `rrr` |  
|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_rotate.gif" width="250" height="250" /> | `ra` | `rb` | `rr` |  
|<img src="https://github.com/pin3dev/42_Cursus/blob/a708c0de6d3fdc729bb720318b5d35bdaa9551c0/assets/PushSwap/Tutorial/general_push.gif" width="250" height="250" /> | `pa` | `pb`| _none_ |  

<p align="center">
 <a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/home.md"> Previous ⬅️ </a> •
<a href="#remarks"> Top ⬆️ </a> • 
<a href="https://github.com/pin3dev/42_Cursus/blob/main/tutorial/PushSwap/EN/docs/concepts.md">Next ➡️ </a>
</p>
