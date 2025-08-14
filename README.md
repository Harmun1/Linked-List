# Linked-List
A class with recursive implementations of add and remove methods, as well as contains, insert, and reverse methods. Will rearrange the order of the nodes by changing the next value that each node holds.
# Author: Harmun Sandhu
# Description: Class with recursive implementations to add, remove, check if value is in list, insert, and reverse methods.

class Node:
    """Represents Node object"""
    def __init__(self, data):
        """Takes data as parameter"""
        self.data = data
        self.next = None

class LinkedList:
    """Represents LinkedList object"""
    def __init__(self):
        """Holds as parameter"""
        self._head = None

    def get_head(self):
        """Returns first Node object"""
        return self._head

    def recur_add(self, node, data):
        """Recursive function to add new node"""
        if node.next is None:
            node.next = Node(data)
        else:
            self.recur_add(node.next, data)

    def add(self, data):
        """Adds new node to linked list"""
        if self._head is None:
            self._head = Node(data)
        else:
            self.recur_add(self._head, data)

    def recur_remove(self, prev_node, current_node, target):
        """Recursive function to remove node from linked list"""
        if current_node is None:
            return
        if current_node.data == target:
            if prev_node is None:
                self._head = current_node.next
            else:
                prev_node.next = current_node.next
        else:
            self.recur_remove(current_node, current_node.next, target)

    def remove(self, target):
        """Removes node from linked list"""
        """Remove the first node with the given data from the linked list."""
        self.recur_remove(None, self._head, target)

    def recur_contains(self, node, target):
        """Recursive function to check if node is in linked list"""
        """Recursive helper function to check if a node with the given data exists in the linked list."""
        if node is None:
            return False
        if node.data == target:
            return True
        return self.recur_contains(node.next, target)

    def contains(self, target):
        """Check if node is in linked list"""
        """Check if a node with the given data exists in the linked list."""
        return self.recur_contains(self._head, target)

    def recur_insert(self, prev_node, current_node, data, position):
        """Recursive function to insert new node"""
        if position == 0:
            new_node = Node(data)
            if prev_node is None:
                new_node.next = self._head
                self._head = new_node
            else:
                new_node.next = current_node
                prev_node.next = new_node
        else:
            if current_node is None:
                raise IndexError("Index out of range")
            self.recur_insert(current_node, current_node.next, data, position - 1)

    def insert(self, data, position):
        """Inserts new node at given position"""
        if position < 0:
            raise IndexError("Index out of range")
        self.recur_insert(None, self._head, data, position)

    def recur_reverse(self, prev_node, current_node):
        """Recursive function to reverse linked list"""
        if current_node is None:
            self._head = prev_node
            return
        next_node = current_node.next
        current_node.next = prev_node
        self.recur_reverse(current_node, next_node)

    def reverse(self):
        """Reverses linked list"""
        self.recur_reverse(None, self._head)

    def recur_to_plain_list(self, node, result_list):
        """Recursive function to convert linked list"""
        if node is None:
            return
        result_list.append(node.data)
        self.recur_to_plain_list(node.next, result_list)

    def to_plain_list(self):
        """Converts the linked list"""
        result_list = []
        self.recur_to_plain_list(self._head, result_list)
        return result_list
