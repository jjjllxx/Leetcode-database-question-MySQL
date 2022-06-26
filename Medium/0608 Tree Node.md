# 608. Tree Node
https://leetcode.cn/problems/tree-node/  
Table: Tree

| Column Name | Type |
|-------------|------|
| id          | int  |
| p_id        | int  |

id is the primary key column for this table.   
Each row of this table contains information about the id of a node and the id of its parent node in a tree.   
The given structure is always a valid tree.  
 

Each node in the tree can be one of three types:

1. "Leaf": if the node is a leaf node.
2. "Root": if the node is the root of the tree.
3. "Inner": If the node is neither a leaf node nor a root node.

Write an SQL query to report the type of each node in the tree.
Return the result table ordered by id in ascending order.
The query result format is in the following example.

Example 1:   
<img width="310" alt="image" src="https://user-images.githubusercontent.com/60777462/175795423-faf065c0-88ed-4133-9401-9693378b657d.png">

Input: 
Tree table:

| id | p_id |
|----|------|
| 1  | null |
| 2  | 1    |
| 3  | 1    |
| 4  | 2    |
| 5  | 2    |

Output: 

| id | type  |
|----|------|
| 1  | Root  |
| 2  | Inner |
| 3  | Leaf  |
| 4  | Leaf  |
| 5  | Leaf  |

Explanation:    
Node 1 is the root node because its parent node is null and it has child nodes 2 and 3.    
Node 2 is an inner node because it has parent node 1 and child node 4 and 5.    
Nodes 3, 4, and 5 are leaf nodes because they have parent nodes and they do not have child nodes.  

Example 2:       
<img width="82" alt="image" src="https://user-images.githubusercontent.com/60777462/175795447-1f72956f-4299-4f91-923b-af06d69e19da.png">   
Input:   
Tree table:  

| id | p_id |
|----|------|
| 1  | null |

Output:   

| id | type  |
|----|------|
| 1  | Root  |

Explanation: If there is only one node on the tree, you only need to output its root attributes.   

## case
``` sql
# Write your MySQL query statement below
SELECT
    id,
    CASE
        WHEN p_id IS NULL THEN 'Root'
        WHEN id IN (SELECT DISTINCT p_id FROM Tree) THEN 'Inner'
        ELSE 'Leaf'
    END AS type
FROM Tree
```
