# 主題:LeetCode 237. Delete Node in a Linked List
---
###### tags: `leetcode` `easy`
##### 類型:`Linked List`


---
## 題目大要:
Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

( 刪除給定Node 除了trail )

Example 1:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220512154507280.png)

```
Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
```
Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.

Example 2:
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220512154522879.png)
```
Input: head = [4,5,1,9], node = 1
Output: [4,5,9]
```
Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.


Constraints:

The number of the nodes in the given list is in the range [2, 1000].
-1000 <= Node.val <= 1000
The value of each node in the list is unique.
The node to be deleted is in the list and is not a tail node




---
## 解法(演算法):
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-2022051300144278.png)
---
## 程式碼(C++)
```C++
void deleteNode(ListNode *node) {
	//刪除相應傳入的這個Node
	printf("刪除val=%d的Node\n", node->val);
	if (node == NULL || node->next == NULL)	//若node為空或node為Trail
		return;

	ListNode* delete_node = node->next;
	node->val = node->next->val;			//該Node值改為原本下一個Node的值，將刪除Node作為下個Node
	node->next = node->next->next;			//該Node改為指向原本下下一個Node，如同刪除
	delete delete_node;						//真正刪掉下個Node (需要?)
}
```
---

# 主題:Leetcode.203 Remove Linked List Elements
---
###### tags: `leetcode easy`
##### 類型:`Linked List` `Recursion`


---
## 題目大要:
Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

( 給val，刪除list中符合val的node )

Example 1:
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513024246447.png)
```
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```
Example 2:

```
Input: head = [], val = 1
Output: []
```
Example 3:
```
Input: head = [7,7,7,7], val = 7
Output: []
```

Constraints:

The number of nodes in the list is in the range [0, 104].
1 <= Node.val <= 50
0 <= val <= 50


---
## 解法(演算法):
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513001754815.png)
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513001811800.png)
---
## 程式碼(C++)
面試題:

```C++
ListNode* deleteNode_byval(ListNode *head, int val) {
	//List為空
	if (!head) {
		printf("List is NULL\n");
		return head;
	}

	ListNode* current_node = head;
	ListNode* previos_node = NULL;	//紀錄當前node之前的List的最後一個node，即為當前的前一個node
	ListNode* delete_node = NULL;

	while (current_node) {								//current_node=頭，迴圈遍歷所有node
		if (current_node->val == val){					//當前Node符合刪除條件
			if(current_node == head)					//判斷當前node是否為Head
				head = head->next;						//將head下一node成為head
			else										//非Head
				previos_node->next = current_node->next; //先前node->next指向下一個node (跳過要刪除的)

			delete_node = current_node;					//當前Node成為要被刪除的node
		}
		else											//不符合，移動pre到當前
			previos_node = current_node;

		current_node = current_node->next;				//當前再往下一指向
		delete delete_node;								//刪除, 要在Current後面!
		delete_node = NULL;
	}

	return head;
}
```

自己刻:
```C++
ListNode* removeElements(ListNode* head, int val) {
    ListNode dummy(0);
    ListNode *pre = &dummy;
    dummy.next = head;
    ListNode *cur = head;

    while(cur != NULL){
        /* 如果current的值==指定刪除的值(val) */
        if(cur->val == val){
            cur = cur->next; // current往後一位
            pre->next = cur; // previous指向current
        }
        /* 否則current跟previous每次往前一步 */
        else{
            pre = cur;
            cur = cur->next;
        }
    }


    return dummy.next;
}
```

# 主題:83. Remove Duplicates from Sorted List
---
###### tags: `leetcode` `easy`
##### 類型: `Linked List`


---
## 題目大要:
Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

( 從已排序的List刪除重複val的Node
	想法：利用/移動Pre成為Cur  )

Example 1:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220510231505459.png)

```
Input: head = [1,1,2]
Output: [1,2]
```
Example 2:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220510231534181.png)
```
Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

Constraints:

The number of nodes in the list is in the range [0, 300].
-100 <= Node.val <= 100
The list is guaranteed to be sorted in ascending order.




---
## 解法(演算法):
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513024725975.png)
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513024742318.png)
---
## 程式碼(C++)
面試題:

```C++
ListNode* deleteNode_byDuplicates(ListNode *head) {
	//List為空
	if (!head) {
		printf("List is NULL\n");
		return head;
	}

	ListNode* current_node = head->next; 	//從第1個 Node(Head->next)
	ListNode* previos_node = head;			//與第0個 Node(Head) 開始，Pre與Cur為前後關係
	ListNode* delete_node = NULL;

	while (current_node) {
		if (current_node->val == previos_node->val){
			previos_node->next = current_node->next;	//若前後相等Pre指向Cur下一個，如同刪除Cur
			delete_node = current_node;
		}
		else
			previos_node = current_node; //若前後不等於，移動Pre到下一個(Current)

		current_node = current_node->next;
		delete delete_node;
		delete_node = NULL;
	}

	return head;
}
```
自己刻:
```C++
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode *cur = head;
        ListNode dummy(9999); // 虛擬節點
        dummy.next = head;
        ListNode *pre = &dummy;

        while(cur!=NULL){
            /* previous與currnet相同，current往前一位，previous指向current(刪除重複節點) */
            if(cur->val == pre->val){
                cur = cur->next;
                pre->next = cur;
            }
            else{ // 兩者不相同，current與previous都往前
                pre = cur;
                cur = cur->next;
            }
        }

        return dummy.next;
    }
};
```
# 主題:82. Remove Duplicates from Sorted List II
---
###### tags: `leetcode` `Medium`
##### 類型:`Linked List` `Two Pointers`


---
## 題目大要:
Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

( 從已排序的List刪除相同val的Node (全部刪除)
想法：先建立虛擬node在Head之前(dummy)
    再移動Pre )

Example 1:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025023843.png)

```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

Example 2:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-2022051302503684.png)

```
Input: head = [1,1,1,2,3]
Output: [2,3]
```

Constraints:

The number of nodes in the list is in the range [0, 300].
-100 <= Node.val <= 100
The list is guaranteed to be sorted in ascending order.
Accepted
488.5K
Submiss



---
## 解法(演算法):
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025145364.png)
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025212516.png)
---
## 程式碼(C++)
面試題:

```C++
ListNode* deleteNode_byDuplicatesAll(ListNode *head) {
	//Node數量小於2
	if (!head || !head->next)
        return head;

	ListNode dummy(0);
	ListNode *previos_node = &dummy;
	dummy.next = head;				//將Head之前在接上一個虛擬Node，防以刪除Head為空
	int val = head->next->val;		//記錄下一node的值，得以比較前後(head與head next)

	while (head) {
		if (head->val == val) {
			while (head && head->val == val)	//若非空且還有相同val的node，指向下一
				head = head->next;

			previos_node->next = head;			//將不相同的val node連接在後面

			if (head && head->next)				//當前head或下一node兩者非空
				val =  head->next->val;			//更新:使用下一val比較
			else
				break;
		}
		else {
			previos_node = head;				//若前後不相等，往下一個移動
			head = head->next;
			if (head->next)						//更新:下一非空，使用下一val比較
				val = head->next->val;
			else
				break;
		}
	}

	return dummy.next; //回傳虛擬node後面的node即可
}
```
自己刻:
```C++
ListNode* deleteDuplicates(ListNode* head) {
    ListNode dummy(0);
    ListNode *pre = &dummy;
    dummy.next = head;
    ListNode *cur = head;

    while(cur!=NULL){
        if(cur->next!=NULL && cur->val==cur->next->val){
            int val = cur->next->val;
            while(cur!=NULL && cur->val == val)
                cur = cur->next;

            pre->next = cur;
        }
        else{
            pre = cur;
            cur = cur->next;
        }

    }
    return dummy.next;
}
```

# 主題:19. Remove Nth Node From End of List
---
###### tags: `leetcode` `Medium`
##### 類型: `Linked List` `Two Pointers`


---
## 題目大要:
Given the head of a linked list, remove the nth node from the end of the list and return its head.

(	刪除從倒數過來nth的node )

Example 1:

![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025656850.png)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

Example 2:

```
Input: head = [1], n = 1
Output: []
```
Example 3:

```
Input: head = [1,2], n = 1
Output: [1]
```

Constraints:

The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz




---
## 解法(演算法):
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025811883.png)
![](https://github.com/asiagodtonegg3beo/meet/raw/main/assets/markdown-img-paste-20220513025840937.png)
---
## 程式碼(C++)
```C++
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode *front = head;
    ListNode *rear = head;

    while (n--)
		front = front->next;	//往前走n步

	if (!front)					//front為空
		return head->next;

	while (front->next) {
        rear = rear->next;
        front = front->next;
    }

    if (rear->next)
    	rear->next = rear->next->next; //跳過(刪除)倒數nth
    else
    	rear->next = NULL;

    return head;
}

```
自己刻:
```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {

        int count = 0;
        ListNode* cur = head;
        ListNode dummy(0); // 虛擬節點
        ListNode* pre = &dummy;
        dummy.next = head;


        /* 計算node數量，O(n) */
        while(cur!=NULL){
            cur=cur->next;
            count++;
        }
        cur = head; // 計算完後重新指回head
        int target = count - n; // 刪除目標節點index = 總數-倒數nth節點

        while(target>0){ // target=0時current會移動到待刪除節點上，previous移至前一個節點
            pre = cur;
            cur = cur->next;
            target--;
        }


        pre->next = cur->next; // 刪除節點

        return dummy.next;
    }
};
```
