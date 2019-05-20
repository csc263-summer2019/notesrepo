# Red Black Tree

Red-Black Trees are binary search trees that are named after the way the nodes are coloured.‌

Each node in a red-black tree is coloured either red or black. The height of a red black tree is at most 2 \* log\(n+1\).‌

A red black tree must maintain the following colouring rules:‌

1. every node must have a colour either red or black.
2. The root node must be black
3. If a node is red, its children must be black. null nodes are considered to be black.
4. Every path from root to null pointer must have exactly the same number of black nodes.

## Insertion <a id="insertion"></a>

We will begin our look at Red-Black trees with the bottom up insertion algorithm. This insertion algorithm is similar to that of the insertion algorithm we looked at for AVL trees/Binary search trees. Insert the new node according to regular binary search tree insertion rules. New nodes are added as red nodes. "Fix" the tree starting at the parent of the newly inserted node so that none of the rules are violated.‌

### General Insertion Algorithm <a id="general-insertion-algorithm"></a>

To insert into a red-black tree:‌

1\) find the correct empty tree and insert new node as a red node. 2\) working way up the tree back to parent fix the tree so that the red-black tree rules are maintained.‌

### Fixing nodes:‌ <a id="fixing-nodes"></a>

1. If a node is red at the root, change it to black.
2. If the new node is red, and its parent is black you don't need to do anything.
3. If a new node is red and its parent is red, what you do depends on colour of sibling of the parent
   * if the sibling of the parent is black, a rotation needs to be performed
   * if the sibling of the parent is red, a color swap with grandparent must be performed

### Example <a id="example"></a>

Starting with an empty tree let us take a look at how red-black tree insertions work.‌

In the pictures below, null nodes \(empty subtrees\) are denoted as black circles‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/nullnodes.png)

#### Insert 30 <a id="insert-30"></a>

‌

All nodes are inserted as red nodes:‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack1.png)

If the root is red, make it black:‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack2.png)

#### Insert 50 <a id="insert-50"></a>

‌

Insert 50 as a red node, parent is black so we don't have to change anything‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack3.png)

#### Insert 40 <a id="insert-40"></a>

‌

Inserting 40 as a red node.![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack4.png)‌

If parent is red, we must apply fix. Parent's sibling \(50's sibling\) is black, so we must perform a rotation.‌

The type of rotation depends on the insertion pathway. If the insertion path from grand parent to parent to node is straight \(both left or both right\) do a single rotation. If it is angled \(left then right or right then left\) we need to do a double.![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack5.png)‌

In this case, we need to do a double \(aka zig zag\) rotation.‌

Rotate first 40 and 50‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack6.png)

then rotate again with 30 and 40, this time doing a colour swap. A zigzag rotation is just an extra step that is needed to make the insertion path go in the same direction.‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack7.png)

Finally we end up with:‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack8.png)

#### Insert 20 <a id="insert-20"></a>

‌

inserting 20 as a red node.‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack9.png)

If parent is red we must apply a fix. Parent's sibling is red so we need to do a colour swap between parent+sibling and grandparent.‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack10.png)

Now as 40 is the root of the whole tree we must change 40's colour to black. As it is the root, we can just change it to black without causing other problems.‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack11.png)

#### Insert 10 <a id="insert-10"></a>

‌

inserting 10 as a red node. ​‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack12.png)

If parent is red, we must apply a fix. Parent's sibling is black, so a rotation is needed. This time, the insertion path from grandparent to parent to node is "left" then "left". Thus, we only need to perform a single rotation and colour swap.‌

![](https://cathyatseneca.gitbooks.io/data-structures-and-algorithms/content/assets/redblack13.png)

Finally we get:‌

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LFrWzEqLSRHjU6HG9dw%2F-LSuF8w3dHjFoMLjastR%2F-LSuFyxto8NJVw2mbir7%2Fredblack14.png?alt=media&token=911a9575-fe2c-4c60-95ed-3c799b66822c)

