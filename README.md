# Construct-Binary-Tree-from-Inorder-and-Postorder-Traversal

Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

class Solution:
    def buildHelper(self, inorder, ins, inl, postorder, posts, postl, index):
        if posts > postl or ins > inl:
            return None
        root = TreeNode(postorder[postl])
        ind = index[root.val]
        x = ind - ins
        root.left = self.buildHelper(inorder, ins, ind - 1, postorder, posts, posts + x - 1, index)
        root.right = self.buildHelper(inorder, ind + 1, inl, postorder, posts + x, postl - 1, index)

        return root

    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        index = {val: i for i, val in enumerate(inorder)}
        
        return self.buildHelper(inorder, 0, len(inorder) - 1, postorder, 0, len(postorder) - 1, index)
