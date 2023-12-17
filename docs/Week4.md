# Week 4

#### Print the Elements of a Linked List
```java
    static void printLinkedList(SinglyLinkedListNode head) {
        if (head == null) return;
        System.out.println(head.data);
        printLinkedList(head.next);

    }
```

#### Insert a Node at the Tail of a Linked List
```java
    static SinglyLinkedListNode insertNodeAtTail(SinglyLinkedListNode head, int data) {
        if (head == null) {
            head = new SinglyLinkedListNode(data);
            return head;
        }
        SinglyLinkedListNode temp = head;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = new SinglyLinkedListNode(data);
        return head;
    }
```

#### Insert a node at the head of a linked list
```java
    static SinglyLinkedListNode insertNodeAtHead(SinglyLinkedListNode llist, int data) {
        if (llist == null) {
            llist = new SinglyLinkedListNode(data);
            return llist;
        }
        SinglyLinkedListNode temp = new SinglyLinkedListNode(data);
        temp.next = llist;
        return temp;
    }
```

#### Insert a node at a specific position in a linked list
```java
    static SinglyLinkedListNode insertNodeAtPosition(SinglyLinkedListNode head, int data, int position) {
        if (head == null) {
            head = new SinglyLinkedListNode(data);
            return head;
        }
        SinglyLinkedListNode temp = head;
        for (int i = 0; i < position - 1; i++) {
            temp = temp.next;
        }
        SinglyLinkedListNode newNode = new SinglyLinkedListNode(data);
        newNode.next = temp.next;
        temp.next = newNode;
        return head;
    }
```

#### Delete a Node
```java
    static SinglyLinkedListNode deleteNode(SinglyLinkedListNode head, int position) {
        if (head == null) return null;
        if (position == 0) return head.next;
        SinglyLinkedListNode temp = head;
        for (int i = 0; i < position - 1; i++) {
            temp = temp.next;
        }
        temp.next = temp.next.next;
        return head;
    }
```

#### Print in Reverse
```java
    static void reversePrint(SinglyLinkedListNode head) {
        if (head == null) return;
        reversePrint(head.next);
        System.out.println(head.data);
    }
```

#### Reverse a linked list
```java
    static SinglyLinkedListNode reverse(SinglyLinkedListNode head) {
        if (head == null) return null;
        SinglyLinkedListNode prev = null;
        SinglyLinkedListNode current = head;
        SinglyLinkedListNode next = null;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        return prev;
    }
```

#### Compare two linked lists
```java
    static boolean compareLists(SinglyLinkedListNode head1, SinglyLinkedListNode head2) {
        if (head1 == null && head2 == null) return true;
        if (head1 == null || head2 == null) return false;
        if (head1.data != head2.data) return false;
        return compareLists(head1.next, head2.next);
    }
```

#### Merge two sorted linked lists
```java
    static SinglyLinkedListNode mergeLists(SinglyLinkedListNode head1, SinglyLinkedListNode head2) {
        if (head1 == null) return head2;
        if (head2 == null) return head1;
        if (head1.data < head2.data) {
            head1.next = mergeLists(head1.next, head2);
            return head1;
        } else {
            head2.next = mergeLists(head1, head2.next);
            return head2;
        }
    }
```

#### Get Node Value
```java
    static int getNode(SinglyLinkedListNode head, int positionFromTail) {
        if (head == null) return 0;
        SinglyLinkedListNode temp = head;
        int count = 0;
        while (temp != null) {
            temp = temp.next;
            count++;
        }
        temp = head;
        for (int i = 0; i < count - positionFromTail - 1; i++) {
            temp = temp.next;
        }
        return temp.data;
    }
```