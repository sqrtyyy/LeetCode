# Trees

+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)
+ [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
+ [Same Tree](#same-tree)
+ [Invert Binary Tree](#invert-binary-tree)
+ [Path Sum](#path-sum)
+ [Binary Tree Level Order Traversal](#binary-tree-level-order-traversal)
+ [Subtree of Another Tree](#subtree-of-another-tree)
+ [Kth Smallest Element in a BST](#kth-smallest-element-in-a-bst)
+ [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)
+ [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
+ [Inorder Successor in BST](#inorder-successor-in-bst)
+ [Validate Binary Search Tree](#validate-binary-search-tree)
+ [Binary Search Tree Iterator](#binary-search-tree-iterator)

## Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

### Recursive
```C++
empty
```

## Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

### Recursive
```C++
class Solution {
public:
    bool Comp(TreeNode* root1, TreeNode* root2){
        if(!root1 || !root2)
            return !root1 && !root2; 
        return (root1->val == root2->val) && Comp(root1->left, root2->right) && Comp(root1->right, root2->left);
    }
    bool isSymmetric(TreeNode* root) {
        return !root || Comp(root->left, root->right);
    }
};
```

## Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

### Recursive
```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(!root)
            return 0;
        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};
```

## Same Tree

https://leetcode.com/problems/same-tree/

### Recursive
```C++
class Solution {
public:
    bool isSameTree(TreeNode* tree1, TreeNode* tree2) {
        if(!tree1 || !tree2)
            return !tree1 && !tree2;
        return (tree1->val == tree2->val) && isSameTree(tree1->left, tree2->left) && isSameTree(tree1->right, tree2->right);
    }
};
```

## Invert Binary Tree

https://leetcode.com/problems/invert-binary-tree/

### Recursive
```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(!root)
            return root;
        swap(root->left, root->right);
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

## Path Sum

https://leetcode.com/problems/path-sum/

### Recursive
```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if(!root)
            return false;
        if(root->val == sum && !root-> left && !root->right)
            return true;
        return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);
    }
};
```

## Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

## Subtree of Another Tree

https://leetcode.com/problems/subtree-of-another-tree/

## Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

## Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

## Inorder Successor in BST

https://www.lintcode.com/problem/inorder-successor-in-bst/description

## Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

## Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/
