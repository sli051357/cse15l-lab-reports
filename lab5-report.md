# Lab Report 5

## Part 1

(This is adopted from my own PA8 bug from CSE 12; however, I was able to stare at it long enough to fix it...)

**Anonymous Moose says...**

Help! When I try to remove 4 from this binary search tree, it throws a NullPointerException! 

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/79f6f7e0-ed5c-46c3-8e64-27a5dc18633c)

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/8ab65c34-7cb3-475d-a87c-405ecc32bb8d)

I'm confused because the test I wrote to remove another node with two children (node 2) worked fine, but this one didn't. I'm confused because I used a recursive call so that the successor (node 5) could be removed, which should jump to the part of my remove method that checks if a node has a right child (which node 5 does). However, it seems like the part where a node has no children is called. I'm confused how that's jumping there. It's specifically the `if (currNode.getParent().getLeft().equals(currNode))` conditional that is throwing the error. 

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/ef0bef51-aaf1-446d-ae1f-d7a633717179)
![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/91dcb21e-8c74-4e7b-bad0-3f44663b4d1e)

Furthermore, it is impossible for `currNode` to be null, because that is something I check for when looking for the node:

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/6635e573-a1ac-42a5-987d-0bc6ec05e9f3)

Please help!

**Scary TA replied...**

Please refer to post @183 in announcements for common debugging techniques or come to tutor hours. 

**Anonymous Moose replied...**

I'm really sorry, but I'm currently in the hospital because a scooter ran me over on campus and broke my leg. Do you have any alternatives?

**Scary (?) TA replied...**

I'm sorry to hear that. Marking this post as private so we can discuss this.

Looking at your issue, it seems that `currNode.getParent().getLeft()` part of the conditional is causing the error by being null, which means that the left child of the node is null. Since the node is a leaf, that means that it has to be a right child of the parent. Why do you think the if statement doesn't jump to the else, and can you think of a way to get the statement to jump there?

**Anonymous Moose replied...**

I think I figured it out! Since I know that the leaf is either the left or right child, I need to check if the left child of the parent is null. If it is, then it is automatically the right child, so I don't need a null check there. Thus, if I add a part to the conditional that checks if the left child is null (both to this part and any other subsequent parts of the method that have a similar function) the problem might be solved.

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/054dec80-7b8e-4db6-b6ab-0d123a4507f4)

That was the issue! Thank you so much!

**Not Scary At All TA replied...**

No problem, hope you get well soon.

***

The file and directory structure is as follows, where the files `RemoveTester.java`, `MyBST.java`, and `test.sh` are within the same directory:

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/8cffde3e-738f-488b-b529-60df44c1fd11)

These were the contents of the important files before fixing the bug:

The `remove` method in `MyBST.java` (which caused the bug): 
```java
public V remove(K key) {
        // node does not exist
        if (search(key) == null) {
            return null;
        }

        // find node (set currNode to removed node)
        MyBSTNode<K, V> currNode = root;
        while (currNode != null) {
            if (currNode.getKey().equals(key)) {
                break;
            } else if (key.compareTo(currNode.getKey()) < 0) {
                currNode = currNode.getLeft();
            } else {
                currNode = currNode.getRight();
            }
        }
        V returnValue = currNode.getValue();

        // node is leaf
        if (currNode.getLeft() == null && currNode.getRight() == null) {
            // node is root
            if (currNode.getParent() == null) {
                root = null;
            } else {
                // is left leaf
                if (currNode.getParent().getLeft().equals(currNode)) {
                    currNode.getParent().setLeft(null);
                }

                // is right leaf
                else {
                    currNode.getParent().setRight(null);
                }
            }
            size--;
        }

        // node only has left child
        else if (currNode.getLeft() != null && currNode.getRight() == null) {
            // node is root
            if (currNode.getParent() == null) {
                root = currNode.getLeft();
            } else {
                // currNode is left child
                if (currNode.getParent().getLeft().equals(currNode)) {
                    currNode.getParent().setLeft(currNode.getLeft());
                } 

                // currNode is right child
                else {
                    currNode.getParent().setRight(currNode.getLeft());
                }
                
            }
            size--;
        }

        // node only has right child
        else if (currNode.getLeft() != null && currNode.getRight() == null) {
            // node is root
            if (currNode.getParent() == null) {
                root = currNode.getRight();
            } else {
                // currNode is left child
                if (currNode.getParent().getLeft().equals(currNode)) {
                    currNode.getParent().setLeft(currNode.getRight());
                }

                // currNode is right child
                else {
                    currNode.getParent().setRight(currNode.getRight());
                }
            }
            size--;
        }
        
        // node has two children
        else {
            // copy data from successor
            K newKey = currNode.successor().getKey();
            V newValue = currNode.successor().getValue();

            // remove successor (also updates size)
            remove(currNode.successor().getKey());

            // reassign data
            currNode.setKey(newKey);
            currNode.setValue(newValue);
            
        }
        return returnValue;
    }
```

The test in `RemoveTester.java` that caught the error:
```java
@Test 
    public void testRemoveWithChildrenAgain() {
        MyBST.MyBSTNode<Integer, Integer> root = tree.root;
        tree.insert(6, 60);
        Integer returnValue = tree.remove(4);

        assertEquals("node removed", null, tree.search(4));
        assertEquals("left child's parent updated", 5, tree.root.getLeft().getRight().getLeft().getLeft().getParent().getKey().intValue());
        assertEquals("right child's parent updated", 5, tree.root.getLeft().getRight().getLeft().getRight().getParent().getKey().intValue());
        assertEquals("value correct", 5, 
                tree.root.getLeft().getRight().getLeft().getKey().intValue());
        assertEquals("return correct", Integer.valueOf(40), 
                returnValue);
        assertEquals("size updated", 9, tree.size);
    }
```

The bash file that was used to run the tester:
```bash
CPATH='.;..\libs\junit-4.13.2.jar;..\libs\hamcrest-2.2.jar'

set -e
javac -cp "$CPATH" MyBST.java RemoveTester.java
java -cp $CPATH org.junit.runner.JUnitCore RemoveTester
```

The command I used to run the bash file was `bash test.sh`, which ran the tester. This tester then ran the `remove()` method in `MyBST.java`, which threw the error.

To fix this bug, I added `currNode.getParent().getLeft() != null` in every conditional that included `currNode.getParent().getLeft().equals(currNode)`. This was because if the left child node of the parent was null, this conditional would be called and then throw an error. Since this specific conditional was checking whether or not `currNode` was the left or right child of the parent node, if the left child was null, than that meant that `currNode` had to be the right one. Thus, if the left child was null, the program would then jump to the specific implementation for a right node, as expected.

## Part 2

I learned a lot about using the terminal, which seems fairly obvious (since that's an important aspect of this course)! My dad always loves to tell me about how important the terminal is and I've also seen it being used, but I never really found the time or motivation to actually learn it. Luckily, I have to take this course, so I am now armed with a much more diverse skillset! I just think that it's amazing how there are so many things that you can do from the command line that are much more convenient than the GUI, and how you can basically handle an entire computer from the terminal. I also really enjoyed writing bash scripts because I used to be part of a team for CyberPatriot (a cybersecurity competition) in high school, where we always heard that the top teams wrote "scripts" to automate things like checking password security or looking for files that shouldn't be there, and although my team always dreamed about writing one, we never did. After writing my own, I can see how important and efficient they are, and it's just impressive that you can automate so many things to work so conveniently.
