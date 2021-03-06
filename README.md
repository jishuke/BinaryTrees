# BinaryTrees
- 一些二叉树相关的操作(Some operations for binary tree)

## BinaryTreeGraph（JS版本）
- 用于展示二叉树的图形化小工具（Graph for displaying a binary tree）

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190407195900332-1594984894.png)

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190407195905516-147813996.png)

## BinaryTreePrinter（Java版本）
### 简介（Intro）
- 树状打印一棵二叉树（Print a binary tree like a real tree）
- 比如输入一棵二叉搜索树（For exampe, if you input a binary search tree）: 
  -  [381, 12, 410, 9, 40, 394, 540, 35, 190, 476, 760, 146, 445, 600, 800]
- 就会输出（Output）:

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406094223007-512106824.png)

- 或者输出（Or output）

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406094237106-573651641.png)

### 核心API（Core API）
```java
public final class BinaryTrees {
	// 打印一棵二叉树
	public static void print(BinaryTreeInfo tree);
	public static void print(BinaryTreeInfo tree, PrintStyle style);

	// 打印一棵二叉树（打印完自动换行）
	public static void println(BinaryTreeInfo tree);
	public static void println(BinaryTreeInfo tree, PrintStyle style);

	// 获得一棵二叉树的打印字符串
	public static String printString(BinaryTreeInfo tree);
	public static String printString(BinaryTreeInfo tree, PrintStyle style);

	// 可选的打印样式
	public enum PrintStyle {
		LEVEL_ORDER, 
		INORDER
	}
}
```

### 示例（Example）
- 先实现**BinaryTreeInfo**的相关操作(Implements BinaryTreeInfo)
  - 根节点是谁？（Who is the root node?）
  - 如何查找左节点？（How to get the left child?）
  - 如何查找右节点？（How to get the right child?）
  - 如何打印单个节点？（How to print a node?）
```java
/**
* BinarySearchTree是你自己编写的二叉树类
* BinarySearchTree is a binary tree class that is created by yourself.
*/
public class BinarySearchTree<E> implements BinaryTreeInfo {
	/**这里省略了大量代码，只贴出了脉络代码**/
	/** only show some main code **/
	
	private Node<E> root;
	private static class Node<E> {
		E element;
		Node<E> left;
		Node<E> right;
	}
	
	/********** BinaryTreeInfo **********/
	@Override
	public Object root() {
		// 根节点是谁？
		// who is the root node?
		return root;
	}

	@Override
	public Object left(Object node) {
		// 如何查找左节点？
		// how to get the left child of the node?
		return ((Node)node).left;
	}

	@Override
	public Object right(Object node) {
		// 如何查找右节点？
		// how to get the right child of the node?
		return ((Node)node).right;
	}

	@Override
	public Object string(Object node) {
		// 如何打印单个节点？
		// how to print the node?
		return ((Node)node).element;
	}
	/********** BinaryTreeInfo **********/
}
```

- 打印(Print)
```java
// 随机生成的一棵二叉搜索树（random generation）
BinarySearchTree<Integer> bst = ...;

// PrintStyle.LEVEL_ORDER（层序打印）
BinaryTrees.println(bst); 

// PrintStyle.INORDER（中序打印）
BinaryTrees.println(bst, PrintStyle.INORDER);
```

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406111607906-1148747309.png)

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406111614353-1717134516.png)

- 也可以生成字符串写入文件(Write to file)
```java
Files.writeToFile("F:/test/bst.txt", BinaryTrees.printString(bst));
```

- 甚至你还都不用定义二叉树类(Even you don't need to create a binary tree class)
```java
BinaryTrees.println(new BinaryTreeInfo() {
	@Override
	public Object root() {
		return 8;
	}

	@Override
	public Object left(Object node) {
		if (node.equals(8)) return 3;
		if (node.equals(3)) return 1;
		if (node.equals(6)) return 4;
		if (node.equals(14)) return 13;
		return null;
	}

	@Override
	public Object right(Object node) {
		if (node.equals(8)) return 10;
		if (node.equals(10)) return 14;
		if (node.equals(3)) return 6;
		if (node.equals(6)) return 7;
		return null;
	}
	
	@Override
	public Object string(Object node) {
		return node;
	}
});

BinaryTrees.println(new BinaryTreeInfo() {
	@Override
	public Object root() {
		return "Life";
	}
	
	@Override
	public Object left(Object node) {
		if (node.equals("Life")) return "Animal";
		if (node.equals("Person")) return "Man";
		if (node.equals("Animal")) return "Cat";
		if (node.equals("Dog")) return "Teddy";
		return null;
	}
	
	@Override
	public Object right(Object node) {
		if (node.equals("Life")) return "Person";
		if (node.equals("Person")) return "Woman";
		if (node.equals("Animal")) return "Dog";
		if (node.equals("Dog")) return "SingleDog";
		return null;
	}
	
	@Override
	public Object string(Object node) {
		return node;
	}
});
```
![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406100247015-1301544281.png)

![](https://img2018.cnblogs.com/blog/497279/201904/497279-20190406100252563-950745142.png)
