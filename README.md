# SOP

BFS concept :
import java.util.*;
public class Main {
    private int vertices;
    private LinkedList<Integer>[] adjList;
    Main(int v) {
        vertices = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adjList[i] = new LinkedList<>();
    }
    void addEdge(int src, int dest) {
        adjList[src].add(dest);
    }
    void bfs(int startNode) {
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();
        visited[startNode] = true;
        queue.add(startNode);
        System.out.println("BFS Traversal starting from node " + startNode + ":");
        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");
            for (int neighbor : adjList[current]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }
    public static void main(String[] args) {
        Main graph = new Main(6);
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(2, 4);
        graph.addEdge(3, 5);
        graph.addEdge(4, 5);
        graph.bfs(0);
    }
}




BALANCED :
class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;
    TreeNode(int value) {
        data = value;
        left = right = null;
    }
}

public class BalancedBinaryTree {
    // class helper
    static class TreeInfo {
        boolean isBalanced;
        int height;
        TreeInfo(boolean isBalanced, int height) {
            this.isBalanced = isBalanced;
            this.height = height;
        }
    }
    // Recursive fun
    static TreeInfo checkBalanced(TreeNode root) {
        if (root == null) return new TreeInfo(true, 0);
        TreeInfo left = checkBalanced(root.left);
        TreeInfo right = checkBalanced(root.right);
        boolean isBalanced = left.isBalanced && right.isBalanced &&
                             Math.abs(left.height - right.height) <= 1;
        int height = 1 + Math.max(left.height, right.height);
        return new TreeInfo(isBalanced, height);
    }
    static boolean isTreeBalanced(TreeNode root) {
        return checkBalanced(root).isBalanced;
    }
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        //root.left.left.left = new TreeNode(5);  //unbalanced
        if (isTreeBalanced(root)) {
            System.out.println("Tree is balanced");
        } else {
            System.out.println("Tree is NOT balanced");
        }
    }
}




DIAMETER :
class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;
    TreeNode(int value) {
        data = value;
        left = right = null;
    }
}

public class TreeDiameter {
    static class TreeInfo {
        int height;
        int diameter;
        TreeInfo(int height, int diameter) {
            this.height = height;
            this.diameter = diameter;
        }
    }
    // Recursive fun
    static TreeInfo getDiameter(TreeNode root) {
        if (root == null)
            return new TreeInfo(0, 0);
        TreeInfo leftInfo = getDiameter(root.left);
        TreeInfo rightInfo = getDiameter(root.right);
        int height = 1 + Math.max(leftInfo.height, rightInfo.height);
        // Diameter
        int diameterThroughRoot = leftInfo.height + rightInfo.height;
        // Max dia
        int diameter = Math.max(diameterThroughRoot,
                        Math.max(leftInfo.diameter, rightInfo.diameter));
        return new TreeInfo(height, diameter);
    }
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.left.left.left = new TreeNode(6);
        TreeInfo result = getDiameter(root);
        System.out.println("Diameter of the tree is: " + result.diameter);
    }
}



MAX DEPTH :
class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;
    TreeNode(int value) {
        data = value;
        left = right = null;
    }
}
public class TreeMaxDepth {
    // Recursive fun
    static int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        return 1 + Math.max(leftDepth, rightDepth);
    }
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.left.left = new TreeNode(5);
        System.out.println("Max depth of the tree is: " + maxDepth(root));
    }
}
