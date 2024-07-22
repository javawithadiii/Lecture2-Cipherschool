# Lecture2-Cipherschool
import java.util.Scanner;

class Node {
    int data;
    Node left;
    Node right;

    Node(int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

public class Main {
    static Node createNode(int data) {
        Node newNode = new Node(data);
        return newNode;
    }

    static Node insertNode(Node root, int data) {
        if (root == null) {
            root = createNode(data);
        } else if (data < root.data) {
            root.left = insertNode(root.left, data);
        } else if (data > root.data) {
            root.right = insertNode(root.right, data);
        }
        return root;
    }

    static boolean searchNode(Node root, int data) {
        if (root == null) {
            return false;
        } else if (root.data == data) {
            return true;
        } else if (data < root.data) {
            return searchNode(root.left, data);
        } else {
            return searchNode(root.right, data);
        }
    }

    static Node deleteNode(Node root, int data) {
        if (root == null) {
            return root;
        } else if (data < root.data) {
            root.left = deleteNode(root.left, data);
        } else if (data > root.data) {
            root.right = deleteNode(root.right, data);
        } else {

            if (root.left == null && root.right == null) {
                root = null;
            } else if (root.left == null) {
                Node temp = root;
                root = root.right;
                temp = null;
            } else if (root.right == null) {
                Node temp = root;
                root = root.left;
                temp = null;
            } else {

                Node temp = root.right;
                while (temp.left != null) {
                    temp = temp.left;
                }
                root.data = temp.data;
                root.right = deleteNode(root.right, temp.data);
            }
        }
        return root;
    }

    static void inorderTraversal(Node root) {
        if (root == null) {
            return;
        }
        inorderTraversal(root.left);
        System.out.print(root.data + " ");
        inorderTraversal(root.right);
    }

    public static void main(String[] args) {
        Node root = null;

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Insert node");
            System.out.println("2. Search node");
            System.out.println("3. Delete node");
            System.out.println("4. Inorder traversal");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter the data to insert: ");
                    int data = scanner.nextInt();
                    root = insertNode(root, data);
                    break;
                case 2:
                    System.out.print("Enter the data to search: ");
                    int searchData = scanner.nextInt();
                    if (searchNode(root, searchData)) {
                        System.out.println("Node " + searchData + " found in the BST.");
                    } else {
                        System.out.println("Node " + searchData + " not found in the BST.");
                    }
                    break;
                case 3:
                    System.out.print("Enter the data to delete: ");
                    int deleteData = scanner.nextInt();
                    root = deleteNode(root, deleteData);
                    System.out.println("Node " + deleteData + " deleted from the BST.");
                    break;
                case 4:
                    System.out.print("Inorder traversal: ");
                    inorderTraversal(root);
                    System.out.println();
                    break;
                case 5:
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
