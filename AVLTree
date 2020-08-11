import java.util.Arrays;




/**
 *
 * AVLTree
 *
 * An implementation of a AVL Tree with
 * distinct integer keys and info
 *
 */

public class AVLTree {

	private AVLNode root;

  /**
   * public boolean empty()
   *
   * returns true if and only if the tree is empty
   *
   */
	public boolean empty() {
		  if (this.getRoot() == null) {
			  return true;
		  }
		  return false;
	}
	
	/**
	 * builds empty tree
	 * 
	 */
	public AVLTree () {
		this.root = null;
	}
	
	
	/**
	 * builds tree with root as sent as parameter
	 * 
	 */
	public AVLTree (IAVLNode root) {
		this.root = (AVLNode) root;
	}
	


 /**
   * public String search(int k)
   *
   * returns the info of an item with key k if it exists in the tree
   * otherwise, returns null
   */
  public String search(int k)
  {
	  IAVLNode x = this.getRoot();
	  while (x != null) {
		  if (k == x.getKey()) {
			  return x.getValue();
		  }
		  else if (k < x.getKey()) {
			  x = x.getLeft();
		  }
		  else {
			  x = x.getRight();
		  }
	  }
	  return null;
  }
  static int numOfRotates=0;
  /**
   * public int insert(int k, String i)
   *
   * inserts an item with key k and info i to the AVL tree.
   * the tree must remain valid (keep its invariants).
   * returns the number of rebalancing operations, or 0 if no rebalancing operations were necessary.
   * returns -1 if an item with key k already exists in the tree.
   */
   public int insert(int k, String i) {
	   numOfRotates=0;
	   IAVLNode x=new AVLNode(k,i);
	   if (this.empty()) {
		   this.root=(AVLNode) x;
		   x.setHeight(0);
		   return 0;
	   }
	   if (search(k)!=null) {
		   return -1;
	   }
	   AVLNode y=(AVLNode)this.getRoot();
	   //y will be the parent of the new node (if node with key k not exists)
	   while(true) {  
		   y.setHeight(y.getHeight()+1);
		   y.setSize(y.getSize()+1);
		   if(y.getKey()>k) {
			   if (y.getLeft().isRealNode()) {
				   y=(AVLNode) y.getLeft();
			   }
			   else {
				   break;
			   }
		   }
		   else {
			   if (y.getRight().isRealNode()) {
				   y=(AVLNode) y.getRight();
			   }
			   else {
				   break;
			   }
		   }
	   }
	   boolean flag=wasUnaryNode(y);
	   if(y.getKey()>k) {
		   y.setLeft(x);
	   }
	   else {
		   y.setRight(x);
	   }
	   x.setParent(y);
	   //case A
	   if(flag) {
		   return 0;
	   }
	   else {
		   y.promote();
		   numOfRotates++;
		   if (y.getParent()!=null) {
			   y=(AVLNode) y.getParent();
			   rebalance(y);  
		   }
	   }
	  return numOfRotates;	
	 }
   
   /**
    * private void rebalance(IAVLNode y)
    * 
    * reblance the tree after insertion by 7 options.
    * counting how much balance act we did.
    */
   private void rebalance(IAVLNode y) {
	   if ((y.getRank()- y.getLeft().getRank()==0 && y.getRank()-y.getRight().getRank()==1)||(y.getRank()-y.getRight().getRank()==0 && y.getRank()-y.getLeft().getRank()==1)) {// 01 situation
		   balance01(y);
	   }
	   else if (y.getRank()-y.getLeft().getRank()==0 && y.getRank()-y.getRight().getRank()==2) {
		   if(y.getLeft().getRank()-y.getLeft().getLeft().getRank()==1 && y.getLeft().getRank()-y.getLeft().getRight().getRank()==2) {
			   balance02_12(y);
		   }
		   else if(y.getLeft().getRank()-y.getLeft().getLeft().getRank()==2 && y.getLeft().getRank()-y.getLeft().getRight().getRank()==1) {
			   balance02_21(y);
		   }
		   else if(y.getLeft().getRank()-y.getLeft().getLeft().getRank()==1  && y.getLeft().getRank()-y.getLeft().getRight().getRank()==1) {
			   rotateR(y);
			   numOfRotates++;
		   }
	   }
	   else if(y.getRank()-y.getLeft().getRank()==2 && y.getRank()-y.getRight().getRank()==0) {
		   if (y.getRight().getRank()-y.getRight().getLeft().getRank()==2 && y.getRight().getRank()-y.getRight().getRight().getRank()==1) {
			   balance20_21(y);
		   }
		   else if(y.getRight().getRank()-y.getRight().getLeft().getRank()==1 && y.getRight().getRank()-y.getRight().getRight().getRank()==2) {
			   balance20_12(y);
		   }
		   else if(y.getRight().getRank()-y.getRight().getLeft().getRank()==1 && y.getRight().getRank()-y.getRight().getRight().getRank()==1) {
			   rotateL(y);
			   numOfRotates++;
			   
		   }
	   }
   }
   
   /**
    * balance01(IAVLNode y)
    * 
    * promote node y and increasing by 1 the counter.
    * if y's parent isn't null we call rebalance again.
    */
   public void balance01(IAVLNode y) {
	   y.promote();
	   numOfRotates++;
	   if (y.getParent()!=null) {
		   rebalance(y.getParent());
	   }
   }
   
   /**
    * public void balance02_12(IAVLNode y)
    * 
    * make rotate to right with node y and his left son.
    * demote y and increasing by 2 the counter.
    */
   public void balance02_12(IAVLNode y) {
	   rotateR(y);
	   y.demote();
	   numOfRotates+=2;
   }
   
   /**
    * balance02_21(IAVLNode y)
    * 
    * make rotate to left with y and his left son.
    * make rotate to right with y and his right son.
    * demote y and his brother,promote his father and increasing by 5 the counter.
    */
   public void balance02_21(IAVLNode y) {
	   rotateL(y.getLeft());
	   rotateR(y);
	   y.getParent().promote();
	   y.demote();
	   y.getParent().getLeft().demote();
	   numOfRotates+=5;
   }
   
   /**
    * balance20_12(IAVLNode y)
    * 
    * make rotate to right with y and his right son.
    * make rotate to left with y and his left son.
    * demote y and his brother,promote his father and increasing by 5 the counter.
    */
   public void balance20_12(IAVLNode y) {
	   rotateR(y.getRight());
	   rotateL(y);
	   y.getParent().promote();
	   y.demote();
	   y.getParent().getRight().demote();
	   numOfRotates+=5;
   }
   
   /**
    * public void balance20_21(IAVLNode y)
    * 
    * make rotate to left with node y and his right son.
    * demote y and increasing by 2 the counter.
    */
   public void balance20_21(IAVLNode y) {
	   rotateL(y);
	   y.demote();
	   numOfRotates+=2;
   }
   
   /**
    * private IAVLNode rotateR(IAVLNode x)
    * 
    * make the rotate to right with y and his left son.
    * update their size and height.
    */
   private IAVLNode rotateR(IAVLNode x) {
	   IAVLNode y=x.getLeft();
	   x.setLeft(y.getRight());
	   y.getRight().setParent(x);
	   y.setRight(x);
	   y.setParent(x.getParent());
	   x.setParent(y);
	   IAVLNode parent=y.getParent();
	   if (parent!=null) {
		   if (this.getRoot()==x) {
			   this.root=(AVLNode) x.getParent();
		   }
		   else {
			   if(parent.getKey()<y.getKey()) {
				   parent.setRight(y);
			   }
			   else {
				   parent.setLeft(y);
			   }
		   	}
	   	}
	   else {
		   this.root=(AVLNode) x.getParent();
	   }
	   x.updetSize();
	   x.updateHeight();
	   y.updetSize();
	   y.updateHeight();
	   return y;
   }
	   


   /**
    * private IAVLNode rotateL(IAVLNode x)
    * 
    * make the rotate to left with y and his right son.
    * update their size and height.
    */
   private IAVLNode rotateL(IAVLNode x) {
	   IAVLNode y=x.getRight();
	   x.setRight(y.getLeft());
	   y.getLeft().setParent(x);
	   y.setLeft(x);
	   y.setParent(x.getParent());
	   x.setParent(y);
	   IAVLNode parent=y.getParent();
	   if (parent!=null) {
		   if (this.getRoot()==x) {
			   this.root=(AVLNode) x.getParent();
		   }
		   else {
			   if(parent.getKey()<y.getKey()) {
				   parent.setRight(y);
			   }
			   else {
				   parent.setLeft(y);
			   }
		   }
	   }
	   else {
		   this.root=(AVLNode) x.getParent();
	   }
	   x.updetSize();
	   x.updateHeight();
	   y.updetSize();
	   y.updateHeight();
	   return y;
   }
   /**
    * private boolean wasUnaryNode(IAVLNode y)
    * 
    * return true iff y is unary (has only one child
    */
	private boolean wasUnaryNode(IAVLNode y) {
		if ((y.getLeft().getRank()==0 && y.getRight().getRank()==-1)||(y.getRight().getRank()==0 && y.getLeft().getRank()==-1)) {
			return true;
		}
		return false;
	}
  /**
   * public int delete(int k)
   *
   * deletes an item with key k from the binary tree, if it is there;
   * the tree must remain valid (keep its invariants).
   * returns the number of rebalancing operations, or 0 if no rebalancing operations were needed.
   * returns -1 if an item with key k was not found in the tree.
   */
   public int delete(int k)
   {
	   AVLNode x = this.root;
	   if (this.search(k) == null) {
		   return -1;
	   }
	   if (x != null && x.key == k && x.rank == 0) { // if root.key = k and root is leaf 
		   this.root = null;
		   return 0;
	   }
	   
	   x.setSize(x.getSize() -1);
	   while (x != null) {
			  if (k == x.key) {
				  if (x.getRank() == 0) { // if x is leaf
					  if (x.getParent().getLeft().equals(x)) { // if x is left child
						  x.getParent().setLeft(new AVLNode());
						  x.getParent().getLeft().setParent((AVLNode)x.getParent());
						  return rebalanceDel((AVLNode) x.getParent());
						  
					  }
					  else { //if x is right child
						  x.getParent().setRight(new AVLNode());
						  x.getParent().getRight().setParent((AVLNode)x.getParent());
						  return rebalanceDel((AVLNode) x.getParent());
					  }
				  }
				  
				  else if ((x.getRight().isRealNode() && !x.getLeft().isRealNode()) || ((!x.getRight().isRealNode()) && x.getLeft().isRealNode())) { // if x is unary
					  if (this.root == x) {
						  if (x.left.getRank() == 0) { // x has left child
							  this.root = (AVLNode) x.getLeft();
							  this.root.setParent(null);
							  this.root.setSize(1);
							  return 0;
						  }
						  if (x.right.getRank() == 0) { // x has right child
							  this.root = (AVLNode) x.getRight();
							  this.root.setParent(null);
							  this.root.setSize(1);
							  return 0;
						  }
					  }
					  else if (x.getParent().getLeft().equals(x)) { // if x is left child
						  if (x.left.getRank() == 0) { // x has left child
							  x.getParent().setLeft(x.getLeft());
							  if (this.getRoot() == x) {
								  return rebalanceDel((AVLNode) x);
							  }
							  return rebalanceDel((AVLNode) x.getParent());
						  }
						  else { // x has right child
							  x.getParent().setLeft(x.getRight());
							  x.getRight().setParent(x.getParent());
							  if (this.getRoot() == x) {
								  return rebalanceDel((AVLNode) x);
							  }
							  return rebalanceDel((AVLNode) x.getParent());
						  }
					  }
					  else { // if x is right child
						  if (x.left.getRank() == 0) { // x has left child
							  x.getParent().setRight(x.getLeft());
							  x.getLeft().setParent(x.getParent());
							  if (this.getRoot() == x) {
								  return rebalanceDel((AVLNode) x);
							  }
							  return rebalanceDel((AVLNode) x.getParent());
						  }
						  else { // x has right child
							  x.getParent().setRight(x.getRight());
							  if (this.getRoot() == x) {
								  return rebalanceDel((AVLNode) x);
							  }
							  return rebalanceDel((AVLNode) x.getParent());
						  }
					  }
				  }
				  
				  else if (!x.isRealNode()) { // if x is virtual leaf
					  return -1;
				  }
				  
				  else { // if x is binary node
					  AVLNode succ = this.Successor(x);
					  x.setKey(succ.getKey());
					  x.setValue(succ.getValue());
					  if (succ.getParent().getLeft().equals(succ)) { // if succ is left child
						  if (succ.getRank() == 1) { // if succ is unary
							  succ.getParent().setLeft(succ.getRight());
							  succ.getRight().setParent(succ.getParent());
							  return rebalanceDel((AVLNode) succ.getParent());
							  }
							  else {
								  succ.getParent().setLeft(new AVLNode());
								  succ.getParent().getLeft().setParent((AVLNode)succ.getParent());
								  return rebalanceDel((AVLNode) succ.getParent());
						  }
					  }
					  else {
						  if (succ.getRank() == 1) { // if succ is unary
							  succ.getParent().setRight(succ.getRight());
							  succ.getRight().setParent(succ.getParent());
							  return rebalanceDel((AVLNode) succ.getParent());
						  }
						  else {
							  succ.getParent().setRight(new AVLNode());
							  succ.getParent().getRight().setParent((AVLNode)succ.getParent());
							  return rebalanceDel((AVLNode) succ.getParent());
						  }
					  }
				  }
			  }
			  else if (k < x.key) {
				  x = x.left;
				  x.setSize(x.getSize() -1);
			  }
			  else {
				  x = x.right;
				  x.setSize(x.getSize() -1);
			  }
		  }
	   return 0; 
   }
   
   /**
	 * rebalance tree after deletion to be valid AVL
	 * returns number of operations needed to balance the tree
	 * 
	 */
   private int rebalanceDel(IAVLNode node) {
	   int cnt = 0;
	   if (node == null) { // if node is null
		   return 0;
	   }
	   while (node != null) { 
		   // if case a
		   if (node.getRank() == node.getRight().getRank() + 2 &&(node.getRank() == node.getLeft().getRank() + 2)){
			   node.demote();
			   cnt++;
			   node = node.getParent();
		   }
		   else {
			   break;
		   }
	   }
	   while (node != null) {
		   // if case a
		   if (node.getRank() == node.getRight().getRank() + 2 &&(node.getRank() == node.getLeft().getRank() + 2)){
			   node.demote();
			   cnt++;
			   node = node.getParent();
		   }
		   // right case
		   else if (node.getRank() == node.getRight().getRank() + 1 &&(node.getRank() == node.getLeft().getRank() + 3)) {
			   IAVLNode y = node.getRight();
			   if (y.getRight() != null && y.getLeft() != null) {
				   //case b
				   if (y.getRank() == y.getRight().getRank() +1 && (y.getRank() == y.getLeft().getRank() +1)){
					   node.demote();
					   y.promote();
					   rotateL(node);
					   cnt += 3;
					   node = null;
				   }
				   // case c
				   else if (y.getRank() == y.getRight().getRank() +1 && (y.getRank() == y.getLeft().getRank() +2)) {
					   node.demote();
					   node.demote();
					   cnt += 3;
					   node = rotateL(node).getParent();
				   }
				   // case d
				   else if (y.getRank() == (y.getRight()).getRank() +2 && (y.getRank() == y.getLeft().getRank() +1)) {
					   node.demote();
					   node.demote();
					   y.demote();
					   y.getLeft().promote();
					   rotateR(y);
					   node = rotateL(node).getParent();
					   cnt += 2;
				   }
			   }
		   }
		   // left case
		   else if (node.getRank() == node.getRight().getRank() + 3 &&(node.getRank() == node.getLeft().getRank() + 1)) {
			   IAVLNode y = node.getLeft();
			   if (y.getRight() != null && y.getLeft() != null) {
				   //case b
				   if (y.getRank() == y.getRight().getRank() +1 && (y.getRank() == y.getLeft().getRank() +1)){
					   node.demote();
					   y.promote();
					   rotateR(node);
					   cnt += 3;
					   node = null;
				   }
				   //case c
				   else if (y.getRank() == y.getRight().getRank() +2 && (y.getRank() == y.getLeft().getRank() +1)) {
					   node.demote();
					   node.demote();
					   cnt += 3;
					   node = rotateR(node).getParent();
				   }
				   //case d
				   else if (y.getRank() == ((AVLNode)y.getRight()).getRank() +1 && (y.getRank() == ((AVLNode)y.getLeft()).getRank() +2)) {
					   
					   node.demote();
					   node.demote();
					   y.demote();
					   y.getRight().promote();
					   rotateL(y);
					   node = rotateR(node).getParent();
					   cnt += 2;
				   }
			   }
			   else {
				   node = null;
			   }
		   }
		   else {
			   break;
		   }
	   }
	   return cnt;
   }
   
   /**
	 * returns node with the smallest value who has bigger value than x 
	 * returns null if x is node with maximum value in tree
	 * 
	 */

   public AVLNode Successor (AVLNode x) {
	   if (x.getRight() != null && x.getRight().isRealNode()) {
		   x = (AVLNode) x.getRight();
		   while (x.getLeft().isRealNode()) {
			   x = (AVLNode) x.getLeft();
		   }
		   return x;
	   }
	   AVLNode y = (AVLNode) x.getParent();
	   while (y!= null && x == y.getRight()) {
		   x = y;
		   y = x.parent;
	   }
	   return y;
   }
   
   
   /**
    * public String min()
    *
    * Returns the info of the item with the smallest key in the tree,
    * or null if the tree is empty
    */
   public String min()
   {
	   if (this.empty()) {
		   return null;
	   }
	   IAVLNode x=this.getRoot();
	   while(x.getLeft().isRealNode()) {
		   x=x.getLeft();
	   }
	   return x.getValue();
   }

   /**
    * public String max()
    *
    * Returns the info of the item with the largest key in the tree,
    * or null if the tree is empty
    */
   public String max()
   {
	   if (this.empty()) {
		   return null;
	   }
	   IAVLNode x=this.getRoot();
	   while(x.getRight().isRealNode()) {
		   x=x.getRight();
	   }
	   return x.getValue();
   }

  /**
   * public int[] keysToArray()
   *
   * Returns a sorted array which contains all keys in the tree,
   * or an empty array if the tree is empty.
   */
   static int i=0;
  public int[] keysToArray()
  {
	  i=0;
	  if (this.empty()) {
		  return new int [0];
	  }
	  int[] arr = new int[this.size()];
	  inOrder(this.getRoot(),arr);
	  return arr;
  }

  /**
   *  private void inOrder(IAVLNode node,int[] st)
   *  
   *  adding the  key's nodes to the tree by order
   */
  private void inOrder(IAVLNode node,int[] st) {
	  if(node.isRealNode()) {
		  inOrder(node.getLeft(),st);
		  st[i]=node.getKey();
		  i++;
		  inOrder(node.getRight(),st);
	  }
  }
  /**
   * public String[] infoToArray()
   *
   * Returns an array which contains all info in the tree,
   * sorted by their respective keys,
   * or an empty array if the tree is empty.
   */
  public String[] infoToArray()
  {
	  i=0;
	  if (this.empty()) {
		  return new String [0];
	  }
	  String[] arr = new String[this.size()];
	  inOrderString(this.getRoot(),arr);
	  return arr;
  }

  /**
   *  private void inOrderString(IAVLNode node,int[] st)
   *  
   *  adding the  value's nodes to the tree by order
   */
  private void inOrderString(IAVLNode node,String[] st) {
	  if(node.isRealNode()) {
		  inOrderString(node.getLeft(),st);
		  st[i]=node.getValue();
		  i++;
		  inOrderString(node.getRight(),st);
	  }
  }
  

   /**
    * public int size()
    *
    * Returns the number of nodes in the tree.
    *
    * precondition: none
    * postcondition: none
    */
   public int size()
   {
	   if (this.empty()) {
		   return 0;
	   }
	   return this.getRoot().getSize();
   }
   
     /**
    * public int getRoot()
    *
    * Returns the root AVL node, or null if the tree is empty
    *
    * precondition: none
    * postcondition: none
    */
   public IAVLNode getRoot()
   {
	   return this.root;
   }
     /**
    * public string split(int x)
    *
    * splits the tree into 2 trees according to the key x. 
    * Returns an array [t1, t2] with two AVL trees. keys(t1) < x < keys(t2).
	  * precondition: search(x) != null
    * postcondition: none
    */   
   public AVLTree[] split(int x)
   {
	   IAVLNode y=this.root;
	   while (y != null) {
		   if (y.getKey() == x) {
			   break;
		   }
		   else if (y.getKey() < x) {
			   y = y.getRight();
		   }
		   else {
			   y = y.getLeft();
		   }
	   }
	   IAVLNode bigger=y.getRight();
	   bigger.setParent(null);
	   IAVLNode smaller=y.getLeft();
	   smaller.setParent(null);
	   AVLTree t1 = new AVLTree();
	   if(smaller.isRealNode()) {
		   t1.root=(AVLNode)smaller;
	   }
	   else {
		   t1.root=null;
	   }
	   AVLTree t2 = new AVLTree();
	   if (bigger.isRealNode()) {
		   t2.root=(AVLNode) bigger;
	   }
	   else {
		   t2.root=null;
	   }
	   IAVLNode parent=y.getParent();
	   while (parent!=null) {
		   if (y.getKey()==parent.getRight().getKey()) {
			   y=new AVLNode(parent.getKey(),parent.getValue());
			   AVLTree t3 = new AVLTree();
			   if (parent.getLeft().isRealNode()) {
				   t3.root=(AVLNode) parent.getLeft();
				   t3.root.setParent(null);
			   }
			   else {
				   t3.root=null;
			   }
			   t1.join(y,t3);
		   }
		   else {
			   y=new AVLNode(parent.getKey(),parent.getValue());
			   AVLTree t4 = new AVLTree();
			   if (parent.getRight().isRealNode()) {
				   t4.root=(AVLNode) parent.getRight();
				   t4.root.setParent(null);
			   }
			   else {
				   t4.root=null;
			   }
			   t2.join(y,t4);
		   }
		   parent=parent.getParent();
	   }
	   AVLTree [] res= {t1,t2};
	   return res; 
   }
   /**
    * public join(IAVLNode x, AVLTree t)
    *
    * joins t and x with the tree. 	
    * Returns the complexity of the operation (rank difference between the tree and t)
	  * precondition: keys(x,t) < keys() or keys(x,t) > keys()
    * postcondition: none
    */   
   public int join(IAVLNode x, AVLTree t)
   {
	   int toRet = 0;
	   if (this.root == null && t.root == null) {
		   return 1;
	   }
	   
	   else if (this.root == null) {
		   t.insert(x.getKey(), x.getValue());
		   this.root = t.root;
		   return this.root.getSize();
	   }
	   
	   else if (t.root == null) {
		   this.insert(x.getKey(), x.getValue());
		   return this.root.getSize();
	   }
	   
	   
	   else if (this.root.key < x.getKey()) { // if keys(x,t) > keys()
		   toRet = 1 +Math.abs(((AVLNode) t.getRoot()).getRank()-((AVLNode) this.getRoot()).getRank());
		   AVLNode first = t.root;
		   if (this.root.rank > first.rank) { // if x should be root
			   first = this.root;
			   while (first.rank > this.root.rank && first.getRight().getRank() != -1) { // go to first vertex on left spine with rank<= this.root.rank()
				   first.setSize(1 + t.root.getSize() + first.getSize());
				   first = first.right;
			   }
			   x.setLeft(first);
			   x.setRight(t.getRoot());
			   x.setParent(first.getParent());
			   t.getRoot().setParent(x);
			   first.setParent(x);
			   x.setSize(1 + this.root.getSize() + t.getRoot().getSize());
			   x.setRank(1 + Math.max(x.getRight().getHeight(), x.getLeft().getHeight()));
			  
			   
		   }
		   else if (this.root.getRank() == first.getRank()) {
			   first.setParent(x);
			   x.setRight(first);
			   x.setLeft(this.root);
			   this.root.setParent(x);
			   x.setSize(1 + this.root.getSize() + t.getRoot().getSize());
			   x.setRank(1 + Math.max(x.getRight().getHeight(), x.getLeft().getHeight()));
			   this.root = (AVLNode) x;
		   }
		   else {
			   while (first.rank > this.root.rank && first.getLeft().getRank() != -1) { // go to first vertex on left spine with rank<= this.root.rank()
				   first.setSize(1 + this.root.getSize() + first.getSize());
				   first = first.left;
			   }
			   x.setSize(1 + first.getSize() + this.getRoot().getSize());
			   x.setParent(first.parent);
			   x.setRank(1 + Math.max(this.getRoot().getHeight(), first.getHeight()));
			   x.setLeft(this.root);
			   this.root.setParent(x);
			   x.setRight(first);
			   
			   if (first.getParent() != null) {
				   this.root = t.root;
				   first.parent.setLeft(x);
			   }
			   else {
				   this.root = (AVLNode) x;
			   }
			   first.setParent(x);
		   }
	   }
	   
	   else if (this.root.key > x.getKey()) {
		   toRet = 1 +Math.abs(t.getRoot().getRank()- this.getRoot().getRank());
		   AVLNode first = this.root;
		   if (t.root.rank > first.rank) { // if x should be root
			   first = t.root;
			   while (first.rank > this.root.rank && first.getRight().getRank() != -1) { // go to first vertex on left spine with rank<= this.root.rank()
				   first.setSize(1 + t.root.getSize() + first.getSize());
				   first = first.right;
			   }
			   
			   x.setLeft(first);
			   x.setRight(this.getRoot());
			   x.setParent(first.getParent());
			   first.getParent().setRight(x);
			   this.getRoot().setParent(x);
			   first.setParent(x);
			   x.setSize(1 + this.root.getSize() + t.getRoot().getSize());
			   x.setRank(1 + Math.max(x.getRight().getHeight(), x.getLeft().getHeight()));
			   this.root = t.root;
		   }
		   else if (t.root.getRank() == first.getRank()) {
			   x.setSize(t.root.getSize() + this.root.getSize() + 1);
			   first.setParent(x);
			   x.setLeft(t.root);
			   x.setRight(first);
			   t.root.setParent(x);
			   this.root = (AVLNode) x;
			   x.setRank(1 + Math.max(x.getRight().getHeight(), x.getLeft().getHeight()));
		   }
		   
		   else {
			   while (first.rank > t.root.rank && first.getLeft().getRank() != -1) { // go to first vertex on left spine with rank<= t.root.rank()
				   first.setSize(1 + first.getSize() + t.getRoot().getSize());
				   first = first.left;
			   }
			   x.setSize(1 + first.getSize() + t.getRoot().getSize());
			   x.setParent(first.parent);
			   x.setRank(1 + Math.max(t.getRoot().getHeight(), first.getHeight()));
			   x.setRight(first);
			   x.setLeft(t.root);
			   t.root.setParent(x);
			   if (first.getParent() != null) {
				   this.root = t.root;
				   first.parent.setLeft(x);
			   }
			   else {
				   this.root = (AVLNode) x;
			   }
			   first.setParent(x);
		   }
	   }
	   while (x != null) {
		   rebalance((AVLNode)x);
		   rebalanceDel((AVLNode) x);
		   x= x.getParent();
	   }
	   return toRet;
   }
   
	/**
	   * public interface IAVLNode
	   * ! Do not delete or modify this - otherwise all tests will fail !
	   */
	public interface IAVLNode{	
		public int getKey(); //returns node's key (for virtuval node return -1)
		public String getValue(); //returns node's value [info] (for virtuval node return null)
		public void setLeft(IAVLNode node); //sets left child
		public IAVLNode getLeft(); //returns left child (if there is no left child return null)
		public void setRight(IAVLNode node); //sets right child
		public IAVLNode getRight(); //returns right child (if there is no right child return null)
		public void setParent(IAVLNode node); //sets parent
		public IAVLNode getParent(); //returns the parent (if there is no parent return null)
		public boolean isRealNode(); // Returns True if this is a non-virtual AVL node
    	public void setHeight(int height); // sets the height of the node
    	public int getHeight(); // Returns the height of the node (-1 for virtual nodes)
    	public void promote(); // sets rank to be previous rank + 1
    	public void demote();// sets rank to be previous rank - 1
    	public int getRank(); // returns rank of the node (-1 for virtual node)
    	public int getSize(); // returns size of the node (0 for virtual node)
    	public void setSize(int size); // sets the size of node
    	public int updetSize(); // sets the size to be left child size + right child size + 1
    	public void setRank(int rank); // sets rank of the node
    	public void updateHeight(); // sets height to be the value of rank
	}

   /**
   * public class AVLNode
   *
   * If you wish to implement classes other than AVLTree
   * (for example AVLNode), do it in this file, not in 
   * another file.
   * This class can and must be modified.
   * (It must implement IAVLNode)
   */
  public class AVLNode implements IAVLNode{
	  private AVLNode left, right, parent;
	  private int rank, key, size, height;
	  private String value;
	  
	  public AVLNode(int key,String value) {
		  this.key=key;
		  this.value=value;
		  this.size=1;
		  this.right=new AVLNode();
		  this.left=new AVLNode();
		  this.rank=0;
		  this.height=0;
	  }
	  public AVLNode() {
		  this.key=-1;
		  this.rank=-1;
	  }
		public int getKey()
		{
			if (!this.isRealNode()) {
				return -1;
			}
			return this.key;
		}
		public String getValue()
		{
			if (!this.isRealNode()) {
				return null;
			}
			return this.value;
		}
		public void setLeft(IAVLNode node)
		{
			this.left = (AVLNode) node;
		}
		public IAVLNode getLeft()
		{
			return this.left;
		}
		public void setRight(IAVLNode node)
		{
			this.right = (AVLNode) node;
		}
		public IAVLNode getRight()
		{
			return this.right;
		}
		public void setParent(IAVLNode node)
		{
			this.parent = (AVLNode) node;
		}
		public IAVLNode getParent()
		{
			return this.parent;
		}
		public boolean isRealNode()
		{
			if (this.key == -1) {
				return false; 
			}
			return true;
		}
		public void setHeight(int height)
		{
			this.height = height;
		}
		public int getHeight()
		{
			if (this.isRealNode()) {
				return this.getRank();
			}
			return -1;
		}
		public void promote() {
			this.rank++;
		}
		public void demote() {
			this.rank--;
		}
	    public int getRank() {
	    	return this.rank;
	    }
	    public int getSize() {
	    	return this.size;
	    }
	    public void setSize(int size) {
	    	this.size=size;
	    }
	    public int updetSize() {
	    	return this.size=((AVLNode)this.getLeft()).getSize() +((AVLNode)this.getRight()).getSize()+1;
	    }
		public void setRank(int rank) {
			this.rank = rank;
		}
	    private void setValue (String value) {
	    	this.value = value;
	    }
	    private void setKey (int key) {
	    	this.key = key;
	    }
	    public void updateHeight() {
	    	this.setHeight(this.getRank());
	    }

		
  }

}
  

