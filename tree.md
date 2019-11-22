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

https://leetcode.com/problems/binary-tree-inorder-traversal/

### Recursive
```C++
class Solution {
 public:
  void InorderArrayCreate(TreeNode* root, vector<int>& result) {
    if (!root) return;
    InorderArrayCreate(root->left, result);
    result.push_back(root->val);
    InorderArrayCreate(root->right, result);
  }
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result;
    InorderArrayCreate(root, result);
    return result;
  }
};
```

### Iterative
```C++
class Solution {
 public:
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> nodes;
    TreeNode* current = root;
    while (!nodes.empty() || current != NULL) {
      while (current) {
        nodes.push(current);
        current = current->left;
      }
      current = nodes.top();
      result.push_back(current->val);
      nodes.pop();
      current = current->right;
    };
    return result;
  }
};
```

## Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

### Recursive
```C++
class Solution {
 public:
  bool Comp(TreeNode* root1, TreeNode* root2) {
    if (!root1 || !root2) return !root1 && !root2;
    return (root1->val == root2->val) && Comp(root1->left, root2->right) &&
           Comp(root1->right, root2->left);
  }
  bool isSymmetric(TreeNode* root) {
    return !root || Comp(root->left, root->right);
  }
};
```
### Iterative
```C++
class Solution {
 public:
  bool isSymmetric(TreeNode* root) {
    if (!root) return true;
    stack<TreeNode*> nodesLeft;
    stack<TreeNode*> nodesRight;
    TreeNode* currentLeft = root->left;
    TreeNode* currentRight = root->right;
    while (!nodesLeft.empty() || currentLeft != NULL) {
      while (currentLeft) {
        if (!currentRight) return false;
        nodesLeft.push(currentLeft);
        currentLeft = currentLeft->left;
        nodesRight.push(currentRight);
        currentRight = currentRight->right;
      }
      if (currentRight) return false;
      currentLeft = nodesLeft.top();
      currentRight = nodesRight.top();
      if (currentLeft->val != currentRight->val) return false;
      nodesLeft.pop();
      nodesRight.pop();
      currentLeft = currentLeft->right;
      currentRight = currentRight->left;
    }
    if (!currentLeft && currentRight) return false;
    return true;
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
    if (!root) return 0;
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
    if (!tree1 || !tree2) return !tree1 && !tree2;
    return (tree1->val == tree2->val) && isSameTree(tree1->left, tree2->left) &&
           isSameTree(tree1->right, tree2->right);
  }
};
```
### Iterative
```C++
class Solution {
 public:
  bool isSameTree(TreeNode* tree1, TreeNode* tree2) {
    stack<TreeNode*> nodes1;
    stack<TreeNode*> nodes2;
    TreeNode* current1 = tree1;
    TreeNode* current2 = tree2;
    while (!nodes1.empty() || current1 != NULL) {
      while (current1) {
        if (!current2) return false;
        nodes1.push(current1);
        current1 = current1->left;
        nodes2.push(current2);
        current2 = current2->left;
      }
      if (current2) return false;
      current1 = nodes1.top();
      current2 = nodes2.top();
      if (current1->val != current2->val) return false;
      nodes1.pop();
      nodes2.pop();
      current1 = current1->right;
      current2 = current2->right;
    }
    if (!current1 && current2) return false;
    return true;
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
    if (!root) return root;
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
    if (!root) return false;
    if (root->val == sum && !root->left && !root->right) return true;
    return hasPathSum(root->left, sum - root->val) ||
           hasPathSum(root->right, sum - root->val);
  }
};
```

## Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

### Recursive
```C++
class Solution {
 public:
  void Levels(TreeNode* root, vector<vector<int>>& result, int level) {
    if (!root) return;
    if (level >= result.size()) result.resize(level + 1);
    result[level].push_back(root->val);
    Levels(root->left, result, level + 1);
    Levels(root->right, result, level + 1);
  }
  vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    Levels(root, result, 0);
    return result;
  }
};
```

### Iterative
```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) return {};
        vector<vector<int>> result;
        queue <pair<TreeNode*, int>> order;
        order.push(make_pair(root, 0));
        while (order.size()){
            pair<TreeNode*, int> curQ = order.front();
            int lvl = curQ.second;
            TreeNode* curN = curQ.first;
            order.pop();
            if (lvl == result.size()) result.resize(lvl + 1);
            result[lvl].push_back(curN->val);
            if (curN->left) order.push(make_pair(curN->left,lvl + 1));
            if (curN->right) order.push(make_pair(curN->right, lvl + 1));
        }
        return result;
    }
};
```

## Subtree of Another Tree

https://leetcode.com/problems/subtree-of-another-tree/

### Recursive
```C++
class Solution {
 public:
  bool isSameTree(TreeNode* tree1, TreeNode* tree2) {
    if (!tree1 || !tree2) return !tree1 && !tree2;
    return (tree1->val == tree2->val) && isSameTree(tree1->left, tree2->left) &&
           isSameTree(tree1->right, tree2->right);
  }
  bool isSubtree(TreeNode* s, TreeNode* t) {
    if (!s || !t) return !s && !t;
    return isSameTree(s, t) || isSubtree(s->left, t) || isSubtree(s->right, t);
  }
};
```

## Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

### Recursive
```C++
class Solution {
 public:
  void InorderArrayCreate(TreeNode* root, vector<int>& result) {
    if (!root) return;
    InorderArrayCreate(root->left, result);
    result.push_back(root->val);
    InorderArrayCreate(root->right, result);
  }
  int kthSmallest(TreeNode* root, int k) {
    vector<int> result;
    InorderArrayCreate(root, result);
    return result[k - 1];
  }
};
```

## Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

### Recursive

#### IZI
```C++
class Solution {
 public:
  TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p ,q);
    return left && right ? root : left ? left : right;
  }
};
```

#### BOOL

```C++
class Solution {
 private:
  TreeNode* result;

 public:
  bool findAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root) return false;
    bool left = findAncestor(root->left, p, q);
    bool right = findAncestor(root->right, p, q);
    if ((left && right) || (left && (root == p || root == q)) ||
        ((root == p || root == q) && right)) {
      result = root;
    }
    return left || right || (root == p || root == q);
  }

  TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    findAncestor(root, p, q);
    return result;
  }
};
```

## Lowest Common Ancestor of a Binary Search Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

### Iterative
```C++
class Solution {
 public:
  TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    int Max = max(p->val, q->val);
    int Min = min(p->val, q->val);
    while (root && !(root->val >= Min && root->val <= Max))
      if (root->val < Min)
        root = root->right;
      else
        root = root->left;
    return root;
  }
};
```

## Inorder Successor in BST

### LintCode

https://www.lintcode.com/problem/inorder-successor-in-bst/description

#### Recursive
```C++
class Solution {
 public:
  TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
    vector<TreeNode*> result;
    InorderArrayCreate(root, result);
    auto node = find(result.begin(), result.end(), p);
    if (node == result.end() || p == result.back()) return NULL;
    return *next(node, 1);
  }

 private:
  void InorderArrayCreate(TreeNode* root, vector<TreeNode*>& result) {
    if (!root) return;
    InorderArrayCreate(root->left, result);
    result.push_back(root);
    InorderArrayCreate(root->right, result);
  }
};
```
### Ne LintCode

#### Structure

```C++
struct TreeNode {
TreeNode *parent;
TreeNode *left;
TreeNode *right;
};
```
#### Solution
```C++
TreeNode* inorderSuccessor(TreeNode* node) {
    if(!node) return NULL;
    TreeNode* cur = node;
    if (cur->right) {
      cur = cur->right;
      while (cur->right) cur = cur->left;
      return cur;
    }
    TreeNode* cur_parent = cur->parent;
    while (cur_parent && cur_parent->right == cur) {
        cur = cur_parent;
        cur_parent = cur_parent->parent;
    }
    return cur_parent;
}
```
 
## Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

### Recursive
```C++
class Solution {
 public:
  bool Comp(TreeNode* root, long int max, long int min) {
    if (!root) return true;
    if (min >= root->val || root->val >= max) return false;
    return Comp(root->left, root->val, min) &&
           Comp(root->right, max, root->val);
  }
  bool isValidBST(TreeNode* root) { return Comp(root, INFINITY, -INFINITY); }
};
```

## Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/

```C++
class BSTIterator {
 public:
  BSTIterator(TreeNode* root) { InorderArrayCreate(root); }
  int next() {
    int min = mins.front();
    mins.pop();
    return min;
  }
  bool hasNext() { return !mins.empty(); }

 protected:
  queue<int> mins;
  void InorderArrayCreate(TreeNode* node) {
    if (!node) return;
    InorderArrayCreate(node->left);
    mins.push(node->val);
    InorderArrayCreate(node->right);
  }
};
```
