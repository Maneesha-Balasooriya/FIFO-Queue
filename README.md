# FIFO-Queue
Implement FIFO queues using  Linked List , Using an Array  and Queue (LinkedList)


import java.util.*;

// FIFO Queue using a Linked List
class LinkedListQueue<T> {
    private Node<T> front, rear;
    
    private static class Node<T> {
        T data;
        Node<T> next;
        Node(T data) { this.data = data; }
    }
    
    public void enqueue(T data) {
        Node<T> newNode = new Node<>(data);
        if (rear != null) rear.next = newNode;
        rear = newNode;
        if (front == null) front = rear;
    }
    
    public T dequeue() {
        if (front == null) throw new NoSuchElementException("Queue is empty");
        T data = front.data;
        front = front.next;
        if (front == null) rear = null;
        return data;
    }
}

// FIFO Queue using an Array
class ArrayQueue<T> {
    private List<T> queue = new ArrayList<>();
    
    public void enqueue(T data) { queue.add(data); }
    
    public T dequeue() {
        if (queue.isEmpty()) throw new NoSuchElementException("Queue is empty");
        return queue.remove(0);
    }
}

// FIFO Queue using Java's Built-in Queue (LinkedList)
class BuiltInQueue<T> {
    private Queue<T> queue = new LinkedList<>();
    
    public void enqueue(T data) { queue.offer(data); }
    
    public T dequeue() { return queue.poll(); }
}

// Steque (Stack + Queue hybrid)
class Steque<T> {
    private Deque<T> deque = new LinkedList<>();
    
    public void push(T data) { deque.addFirst(data); } // Stack push
    
    public void enqueue(T data) { deque.addLast(data); } // Queue enqueue
    
    public T pop() { 
        if (deque.isEmpty()) throw new NoSuchElementException("Steque is empty");
        return deque.removeFirst(); 
    }
}

// Circular Queue
class CircularQueue<T> {
    private T[] queue;
    private int front, rear, size, capacity;
    
    public CircularQueue(int capacity) {
        this.capacity = capacity;
        queue = (T[]) new Object[capacity];
        front = rear = size = 0;
    }
    
    public void enqueue(T data) {
        if (size == capacity) throw new IllegalStateException("Queue is full");
        queue[rear] = data;
        rear = (rear + 1) % capacity;
        size++;
    }
    
    public T dequeue() {
        if (size == 0) throw new NoSuchElementException("Queue is empty");
        T data = queue[front];
        front = (front + 1) % capacity;
        size--;
        return data;
    }
}

public class QueueDemo {
    public static void main(String[] args) {
        // Example usage
        LinkedListQueue<Integer> llq = new LinkedListQueue<>();
        llq.enqueue(10);
        llq.enqueue(20);
        System.out.println(llq.dequeue()); // 10
        
        ArrayQueue<Integer> aq = new ArrayQueue<>();
        aq.enqueue(30);
        aq.enqueue(40);
        System.out.println(aq.dequeue()); // 30
        
        BuiltInQueue<Integer> biq = new BuiltInQueue<>();
        biq.enqueue(50);
        biq.enqueue(60);
        System.out.println(biq.dequeue()); // 50
        
        Steque<Integer> steque = new Steque<>();
        steque.push(70);
        steque.enqueue(80);
        System.out.println(steque.pop()); // 70
        
        CircularQueue<Integer> cq = new CircularQueue<>(3);
        cq.enqueue(90);
        cq.enqueue(100);
        System.out.println(cq.dequeue()); // 90
    }
}

