# Implement-Tree
this id my implementation of Binary Tree with other methods:)
import java.util.*;


public  class MyTree implements Tree {
    Node root;
    public MyTree() {
    }
    @Override
    public boolean isEmpty(){
        return (root==null);
    }
  public Node getRoot(){
      return root;
  }
    @Override
    public void clear(){
        root=null;
    }
    @Override
    public void inOrder(){
        inOrder(root);// increasing order
       System.out.println("");
    }
    private void inOrder(Node root){
        if(root!=null){// left>>root>>right
           inOrder(root.left);
           System.out.print(root.value+ " ");
           inOrder(root.right);  
        }
    }
    @Override
    public void insert(int x){
        root =insert(x,root);
    }

    private Node insert(int x, Node root) {
        if(root==null)//if the treee is empty&& inserting in the null position هون بعرف نود جديدفيه القيمة وبربطه مع الي قبل حسب الريكيرجين
            return new Node(x);   
        else{
            // here I have traversing to the right/left subtree><
            if(root.value>x)// traversing to the left<<< 
            root.left= insert(x,root.left);// المسااواة هون ضرورية لأني بعمل ادخال بالتالي لازم اربط نودات مع بعض وبربطهم من خلال نودات معرفة سابقا مع اسناد قيمة النود الجديد ليمين او يسار النود
        else if(root.value<x)// traversing to the right>>>
            root.right=insert(x,root.right);
        else return root; // Duplicate node not inserted <>
        }
        return root;// هذي ضرورتها بتكون بعد نهاية الركيرجين المفروض ارجع كل نود مكانه ..يعني هون انا بتعامل بوينترات ممكن تتغير لهيك لازم ارجع كل نود لمكانه لحتى ما تتتدمر الشجرة
    }
    public boolean search(int value){
      Node c=search(value,root);
      if(c==null)return false;
      return true;
    } 
    private Node search(int value, Node root) {
        if(root==null|| root.value==value)//tree id empty or value foundedad at this root
            return root;
        if(root.value>value)//traverse left subtree
         return search (value,root.left);
        return search(value,root.right);//traversing to the right subtree 
    }
    

 public int Min(){
      Node min= Min(root);
 return min.value;      
   }
    private Node Min(Node root) {
      if(root.left==null)return root;
     return Min(root.left);
    }
    @Override
    public void delete(int x){
        root=delete(x,root);
    }


    private Node delete(int x, Node root) {
        if(root==null)return root;
        if(root.value<x)
           root.right= delete(x,root.right);
        else if(root.value>x)
           root.left=delete(x,root.left);
        else{
            if(root.left==null)
                return root.right;
            else if(root.right==null)
               return root.left;
            root.value=Min(root.right).value;//   
            root.right=delete(root.value,root.right);
        }
        return root;
    }
     
    @Override
     public void postOrder(){
        postOrder(root);//left>>right>>root
        System.out.println("");
    }

    private void postOrder(Node root) {
        if(root==null)return;
        postOrder(root.left);
        postOrder(root.right);
        System.out.print(root.value +" ");
    }
    @Override
  public void preOrder(){
        preOrder(root);//root>>left>>right
        System.out.println("");
    }

    private void preOrder(Node root) {
        if(root==null){ System.out.print("null "); return;}
        System.out.print(root.value + " ");
        preOrder(root.left);
        preOrder(root.right);
    }
   //Returns a path from the root leading to the specified element 
    public int path(int x){
        if(root.value==x)return 0;
      return path(x,root,0);
    }
    
       

    private int path(int x,Node root, int i) {
if(root==null|| root.value==x){//tree id empty or value foundedad at this root
            return 1;}
       // System.out.println(i);
        if(root.value>x)//traverse left subtree
          return i+path (x,root.left,++i);
          return i+path(x,root.right,++i);   
        }
    int a[]=new int [4]; int i=0;


    public List<Integer> inorderTraversal(Node root) {
        List<Integer> res= new ArrayList <>();
        Stack <Node>s = new Stack<>();
        Node cur= root, preNode =null;
        while(cur!=null || !s.isEmpty()){
            if(cur!=null){
         s.push(cur);
         cur=cur.left;}
            else{
              preNode =s.pop();
             res.add(preNode.value);
             cur=preNode.right;
            }
        }
        return res;
    }
        public List<Integer> preorderTraversal(Node root) {
            Stack <Node>s= new Stack<>();
            List <Integer> res= new ArrayList<>();
            Node cur=root, pre=null;
            while(cur!=null || !s.isEmpty()){
            if(cur!=null){
                res.add(cur.value);
                s.push(cur);
                cur=cur.left;
            }
            else{
                pre=s.pop();
                cur=pre.right;
            }
        }
            return res;
        
        }
        public List<Integer> postorderTraversal(Node root) {
           Stack <Node>s= new Stack<>();
            List <Integer> res= new ArrayList<>();
            Node cur=root, pre=null;
            s.push(root);
            while(!s.isEmpty() ){
                cur=s.peek();
                if(cur.left!=null){
                    s.push(cur.left);
                    cur.left=null;
                }
                else if(cur.right!=null){
                    s.push(cur.right);
                  cur.right=null;
                }
                else{
                    res.add(s.pop().value);
                }
            }
            return res;
        }
        
}
     
   
    
    

