Leetcode - 543

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        

        // return diameter1(root);

        // return diameter2_by_using_class_pair(root);

        // Approch 3rd using change and traversal concepts
        diameter3_by_using_static_variable(root);
        return dai;
    }

    static int dai=0;
    public int diameter3_by_using_static_variable(TreeNode node){

        // In this approch main we find a daimeter but i return a height

        if(node==null){
            return -1;
        }

        int ld=diameter3_by_using_static_variable(node.left);
        int rd=diameter3_by_using_static_variable(node.right);

        dai=Math.max(dai,ld+rd+2);

        return Math.max(ld,rd) +1;
    }

    public static class Pair{
        int hi;
        int dai;
    }

    public Pair ans(TreeNode node){
        if(node==null){
            Pair temp=new Pair();
            temp.hi=-1;
            temp.dai=0;

            return temp;
        }

        Pair lp=ans(node.left);
        Pair rp=ans(node.right);

        Pair my_pair=new Pair();

        my_pair.hi= Math.max(lp.hi,rp.hi)+1;
        my_pair.dai= Math.max(Math.max(lp.dai,rp.dai),lp.hi+rp.hi+2);

        return my_pair;
    }
    public int diameter2_by_using_class_pair(TreeNode node){

        Pair ans=ans(node);

        return ans.dai;
    }

    public int height(TreeNode node){

        return node==null ? -1 : Math.max(height(node.left),height(node.right))+1;
    }

    public int diameter1(TreeNode node){
        if(node==null){
            return 0;
        }

        int ld=diameter1(node.left);
        int rd=diameter1(node.right);

        int lh=height(node.left);
        int rh=height(node.right);

        int my_dai= lh+rh+2;

        return Math.max(Math.max(ld,rd),my_dai);
    }
}
