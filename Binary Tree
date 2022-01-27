package binary_tree;
class Node{
    Node left, right, parent;
    int data;
}
public class Binary_Tree {
// FUNCTIONS & GLOBAL VARIABLES
    static Node root;

    static void insert(int data){
        // buat node baru
        Node new_node = new Node();
        new_node.data = data;
        if(root == null){ // tree kosong
            root = new_node;
        }else{
            Node position = root;
            boolean found = false;
            while(!found){
                if(new_node.data < position.data){
                    if(position.left == null){
                        found = true;
                        new_node.parent = position;
                        position.left = new_node;
                    }else{
                        position = position.left;
                    }
                }else{
                    if(position.right == null){
                        found = true;
                        new_node.parent = position;
                        position.right = new_node;
                    }else{
                        position = position.right;
                    }
                }
            }
        }
    }

    static void view(){
        node_view(root, "");
    }
    static void node_view(Node node, String spaces){
        if(node == null){
            System.out.println(spaces + "EMPTY");
        }else{
            System.out.println(spaces + node.data);
            node_view(node.left, spaces+"    ");
            node_view(node.right, spaces + "    ");
        }
    }

    static void postfix (Node localroot){
        if(localroot != null){
            System.out.print("(");
            postfix(localroot.left);
            postfix(localroot.right);
            System.out.print(" "+localroot.data+" ");
            System.out.print(")");
        }
    }

    static void delete(int deleted){
        boolean found = false;
        Node x = root;
        while(x != null){
            if(x.data == deleted){
                found = true;
                break;
            }else if(x.left != null  && deleted < x.data){
                x = x.left;
            }else if(x.right != null && deleted > x.data){
                x = x.right;
            }else{
                found = false;
                break;
            }
        }
        if(!found){
            // do nothing, node not found
        }else{
            boolean is_root = x.parent == null;
            boolean is_right = !is_root && x == x.parent.right;
            boolean is_left = !is_root && x == x.parent.left;
            // jika tidak punya anak
            if(x.left == null && x.right == null){
                if(is_root){ //  tdk punya anak & adalah root
                    root = null;
                }else{ // tdk punya anak & bukan root
                    if(is_left){ // tdk punya anak & adalah anak kiri
                        x.parent.left = null;
                    }else if(is_right){ // tdk punya anak & adalah anak kanan
                        x.parent.right = null;
                    }
                    x.parent = null; // putuskan hubungan dengan parent
                }
            }else if(x.left != null && x.right == null){ // hanya punya anak kiri
                if(is_root){
                    root = x.left;
                    root.parent.left = null;
                    root.parent = null;
                }else{
                    if(is_left){
                        x.parent.left = x.left;
                    }else if(is_right){
                        x.parent.right = x.left;
                    }
                    x.left.parent = x.parent;
                    x.parent = null;
                    x.left = null;
                }
            }else if(x.left == null && x.right != null){ // hanya punya anak kanan
                if(is_root){ // root
                    root = x.right;
                    root.parent.right = null;
                    root.parent = null;
                }else{ // bukan root
                    if(is_left){
                        x.parent.left = x.right;
                    }else if(is_right){
                        x.parent.right = x.right;
                    }
                    x.right.parent = x.parent;
                    x.parent = null;
                    x.right = null;
                }
            }else{ // punya 2 anak
                Node replacement = x.right; // kanan sekali
                while(replacement.left != null){ // kiri sekiri-kirinya
                    replacement = replacement.left;
                }
                if(replacement.right != null){ // kalau replacement punya anak kanan
                    replacement.parent.left = replacement.right;
                    replacement.right.parent = replacement.parent;
                }else{ // kalau replacement tidak punya anak
                    replacement.parent.left = null;
                }
                // replace x
                if(is_root){
                    replacement.parent = null; 
                    root = replacement;
                }else if(is_left){
                    replacement.parent = x.parent;
                    x.parent.left = replacement;
                }else if(is_right){
                    replacement.parent = x.parent;
                    x.parent.right = replacement;
                }                
                replacement.left = x.left;
                replacement.right = x.right;
                if(replacement.left != null){
                    replacement.left.parent = replacement;
                }
                if(replacement.right != null){
                    replacement.right.parent = replacement;
                }
                // hapus x dari tree
                x.parent = null;
                x.left = null;
                x.right = null;
            }
        }
    }

    public static void main(String[] args) {
        insert(5);
        insert(7);
        insert(6);
        insert(8);
        insert(2);
        insert(4);
        insert(1);
        view();
        delete(5);
        view();
        postfix(root);
    }    
}
