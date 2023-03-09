Part 1: DSA
Problem 1: Stack
Implement a stack data structure in Python. The stack should support the following operations:
push(item) - Add an item to the top of the stack.
pop() - Remove and return the item on the top of the stack.
peek() - Return the item on the top of the stack without removing it.
is_empty() - Return True if the stack is empty, else False.

class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()

    def peek(self):
        if not self.is_empty():
            return self.items[-1]

    def is_empty(self):
        return len(self.items) == 0


# Create a new stack
s = Stack()
s.push(1)
s.push(2)
s.push(3)
print(s.is_empty()) # Output: False
print(s.peek()) # Output: 3
s.pop()
print(s.peek()) # Output: 2
s.pop()
s.pop()
print(s.is_empty()) # Output: True


Problem 2: Queue
Implement a queue data structure in Python. The queue should support the following operations:
enqueue(item) - Add an item to the back of the queue.
dequeue() - Remove and return the item at the front of the queue.
peek() - Return the item at the front of the queue without removing it.
is_empty() - Return True if the queue is empty, else False.

class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.items.pop(0)

    def peek(self):
        if not self.is_empty():
            return self.items[0]

    def is_empty(self):
        return len(self.items) == 0


# Create a new queue
q = Queue()
q.enqueue(1)
q.enqueue(2)
q.enqueue(3)
print(q.is_empty()) # Output: False
print(q.peek()) # Output: 1
q.dequeue()
print(q.peek()) # Output: 2
q.dequeue()
q.dequeue()
print(q.is_empty()) # Output: True


Problem 3: Binary Search Tree
Implement a binary search tree (BST) data structure in Python. The BST should support the following operations:
insert(item) - Insert an item into the tree.
delete(item) - Remove an item from the tree.
search(item) - Return True if the item is in the tree, else False.
size() - Return the number of nodes in the tree.

class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None
        self.count = 0

    def insert(self, val):
        if not self.root:
            self.root = Node(val)
        else:
            self._insert(val, self.root)

    def _insert(self, val, node):
        if val < node.val:
            if not node.left:
                node.left = Node(val)
            else:
                self._insert(val, node.left)
        else:
            if not node.right:
                node.right = Node(val)
            else:
                self._insert(val, node.right)
        self.count += 1

    def delete(self, val):
        if self.root:
            self.root, deleted = self._delete(val, self.root)
            if deleted:
                self.count -= 1

    def _delete(self, val, node):
        if not node:
            return node, False

        deleted = False
        if val == node.val:
            deleted = True
            if not node.left and not node.right:
                return None, deleted
            elif not node.left:
                return node.right, deleted
            elif not node.right:
                return node.left, deleted
            else:
                successor = self._find_min(node.right)
                node.val = successor.val
                node.right, _ = self._delete(successor.val, node.right)
        elif val < node.val:
            node.left, deleted = self._delete(val, node.left)
        else:
            node.right, deleted = self._delete(val, node.right)

        return node, deleted

    def search(self, val):
        return self._search(val, self.root)

    def _search(self, val, node):
        if not node:
            return False
        elif val == node.val:
            return True
        elif val < node.val:
            return self._search(val, node.left)
        else:
            return self._search(val, node.right)

    def size(self):
        return self.count

    def _find_min(self, node):
        while node.left:
            node = node.left
        return node


# Create a new binary search tree
bst = BinarySearchTree()

# Insert some items into the tree
bst.insert(5)
bst.insert(3)
bst.insert(8)
bst.insert(1)
bst.insert(4)
bst.insert(7)
bst.insert(9)

# Check the size of the tree
print(bst.size()) # Output: 7

# Search for an item in the tree
print(bst.search(4)) # Output: True
print(bst.search(6)) # Output: False

# Delete an item from the tree
bst.delete(3)

# Check the size of the tree after deleting an item
print(bst.size()) # Output: 6


Part 2: Python
Problem 1: Anagram Checker
Write a Python function that takes in two strings and returns True if they are anagrams of each other, else False. An anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

def is_anagram(s1, s2):
    s1 = s1.replace(" ", "").lower()
    s2 = s2.replace(" ", "").lower()
    return sorted(s1) == sorted(s2)

# Get input from user
s1 = input("Enter first string: ")
s2 = input("Enter second string: ")

# Check if the two strings are anagrams of each other
if is_anagram(s1, s2):
    print("The two strings are anagrams of each other.")
else:
    print("The two strings are not anagrams of each other.")


Problem 2: FizzBuzz
Write a Python function that takes in an integer n and prints the numbers from 1 to n. For multiples of 3, print "Fizz" instead of the number. For multiples of 5, print "Buzz" instead of the number. For multiples of both 3 and 5, print "FizzBuzz" instead of the number.

def fizzbuzz(n):
    for i in range(1, n+1):
        if i % 3 == 0 and i % 5 == 0:
            print("FizzBuzz")
        elif i % 3 == 0:
            print("Fizz")
        elif i % 5 == 0:
            print("Buzz")
        else:
            print(i)

# Get input from user
n = int(input("Enter a number: "))

# Call the fizzbuzz function with the user input
fizzbuzz(n)


Problem 3: Fibonacci Sequence
Write a Python function that takes in an integer n and returns the nth number in the Fibonacci sequence. The Fibonacci sequence is a series of numbers in which each number after the first two is the sum of the two preceding ones.

def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

# Get input from user
n = int(input("Enter a number: "))

# Call the fibonacci function with the user input
result = fibonacci(n)

# Print the result
print(f"The {n}th number in the Fibonacci sequence is {result}.")


