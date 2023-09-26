// LAURA HUNDZINSKI DA ROCHA
// BCC 4B MANHÃ

class TreeNode {
    int data;
    TreeNode left;
    TreeNode right;

    public TreeNode(int data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

class BinarySearchTree {
    TreeNode root;

    public BinarySearchTree() {
        this.root = null;
    }

    // 1. Inserir um elemento em uma árvore binária de busca
    public void insert(int data) {
        root = insertRecursive(root, data);
    }

    private TreeNode insertRecursive(TreeNode current, int data) {
        if (current == null) {
            return new TreeNode(data);
        }

        if (data < current.data) {
            current.left = insertRecursive(current.left, data);
        } else if (data > current.data) {
            current.right = insertRecursive(current.right, data);
        }

        return current;
    }

    // 2. Percorrer a árvore nas formas préordem, inordem e pósordem
    public void preorderTraversal(TreeNode node) {
        if (node != null) {
            System.out.print(node.data + " ");
            preorderTraversal(node.left);
            preorderTraversal(node.right);
        }
    }

    public void inorderTraversal(TreeNode node) {
        if (node != null) {
            inorderTraversal(node.left);
            System.out.print(node.data + " ");
            inorderTraversal(node.right);
        }
    }

    public void postorderTraversal(TreeNode node) {
        if (node != null) {
            postorderTraversal(node.left);
            postorderTraversal(node.right);
            System.out.print(node.data + " ");
        }
    }

    // 3. Remover o maior elemento da árvore
    public void removeMax() {
        root = removeMaxRecursive(root);
    }

    private TreeNode removeMaxRecursive(TreeNode current) {
        if (current == null) {
            return null;
        }

        if (current.right == null) {
            return current.left;
        }

        current.right = removeMaxRecursive(current.right);
        return current;
    }

    // 4. Remover o menor elemento da árvore
    public void removeMin() {
        root = removeMinRecursive(root);
    }

    private TreeNode removeMinRecursive(TreeNode current) {
        if (current == null) {
            return null;
        }

        if (current.left == null) {
            return current.right;
        }

        current.left = removeMinRecursive(current.left);
        return current;
    }

    // 5. Remover um elemento específico da árvore
    public void remove(int data) {
        root = removeRecursive(root, data);
    }

    private TreeNode removeRecursive(TreeNode current, int data) {
        if (current == null) {
            return current;
        }

        if (data < current.data) {
            current.left = removeRecursive(current.left, data);
        } else if (data > current.data) {
            current.right = removeRecursive(current.right, data);
        } else {
            // Caso tenhamos encontrado o elemento a ser removido
            if (current.left == null) {
                return current.right;
            } else if (current.right == null) {
                return current.left;
            }

            // Se o nó a ser removido possui dois filhos, substitua-o pelo sucessor
            current.data = minValue(current.right);
            current.right = removeRecursive(current.right, current.data);
        }

        return current;
    }

    private int minValue(TreeNode node) {
        int minValue = node.data;
        while (node.left != null) {
            minValue = node.left.data;
            node = node.left;
        }
        return minValue;
    }
}

// Classe Main
public class Main {
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        tree.insert(50);
        tree.insert(30);
        tree.insert(70);
        tree.insert(20);
        tree.insert(40);
        tree.insert(60);
        tree.insert(80);

        System.out.println("Inorder Traversal:");
        tree.inorderTraversal(tree.root); // Imprimir a árvore em ordem

        System.out.println("\nRemovendo o maior elemento:");
        tree.removeMax();
        tree.inorderTraversal(tree.root); // Imprimir a árvore em ordem depois da remoção do maior elemento

        System.out.println("\nRemovendo o menor elemento:");
        tree.removeMin();
        tree.inorderTraversal(tree.root); // Imprimir a árvore em ordem depois da remoção do menor elemento

        System.out.println("\nRemovendo o elemento 40:");
        tree.remove(40);
        tree.inorderTraversal(tree.root); // Imprimir a árvore em ordem depois da remoção do elemento 40
    }
}
