# Binary Search

**Definitions:**  
lst = list, elt = element, left = left index, right = right index

**Requirements:**  
0 <= left <= right < size (lst)  

**Invariant:**  
If the element is found in the list, then it must also be found in the sub-lists 
[lst[left]], ...,[lst[right]]

Pseudocode for binarySearchHelper: 

    def binarySearchHelper (lst, elt, left, right) 
    if (left > right):
        return None 
        #the item does not exist because the left index has crossed the right index
    else:
        mid = (left + right) // 2 
        #use integer division to get a whole num

        if lst[mid] == elt:
            return mid 
            #best case, found the num at the index, return index
        elif lst[mid] < elt :
            return binarySearchHelper(lst. elt, mid+1, right)
            #recurse but change the left index to the mid index + 1
        elif lst[mid] > elt :
            return binarySearchHelper(lst, elt, left, mid-1)
            #recurse but change the right index to the mid index - 1

Pseudocode for binarySearch:

    def binarySearch(lst, elt)
        binarySearchHelper(lst, elt, 0, size(list)- 1)
        #0 is the left index, size(list) - 1 is the right index

Why is binary search correct?  
BSH (binarySearchHelper) has the following behaviors for lists sorted in **ascending order**:  
As stated above in the note on invariants, if the element is in the sub-list, then BSH will return the index of the element in the list.  
If the element does not belong to a sub-list, then it will return *None*.
	
When BSH is called, the invariant is always maintained. It **always** has this property:
- If I can find the element in the list, then I can find it in some iteration of the search (induction argument)
- Example: If 4 is found in [1,3,4,7,9], then it would also be found in [1,2,3,4,5,6,7,8,9]

## Run Time Analysis

Θ(log~2~n)  
*Upper bounded by log~2~n*

If n = 2^k^ and we go with k = 10, then n = 1024.
In binary search, in every iteration of the algo, the search gets halved.  
If the first iteration is the entire list, then the second iteration is either the left or right half. We keep going until the list is of size 1 for a worst-case scenario.

In the **worst** case, each iteration will half the list:
- 1^st^: n/2 = 2^k-1^
- 2^nd^: n/4 = 2^k-2^
- 3^rd^: n/8 = 2^k-3^
- ...
- K^th^: List of size 1 = 2^k-k^
  
Therefore, in a **worst case** scenario, binary search will take K+1 where K = log~2~n, or Θ(log~2~n)

**Examples:**  
If we have a list of 10^9^ (one billion) elements, which is approx. 2^20^ elements, it will take roughly 21 steps to get the search item in the worst case scenario or it won't exist. 
If we have a list of 10^12 (one trillion) elements, which is approx. 2^30^ elements. It will 