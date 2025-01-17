---
share: "true"
title: BAGS, QUERES, AND STACKS
---

### stacks and queue introduce
the stack and queue, differ in the way in which the item to be removed is chosen.
- stack LIFO
- queue FIFO
![Pasted image 20250117151739.png](/images/Pasted%20image%2020250117151739.png)
Our sub text today is all about modular programming.
The idea is to completely separate the interface and the implementation.
So when we have these types of data structures and data types that are precisely defined, like stacks and queues ans so forth, what we weant to do is completely separate the details of the implementation form the client. The client can have many different implementations from which to choose, but the client code should only perform the basic operations.
The implementation, on the other hand, can't know the details of the client needs. All it's supposed to do is implement those operations.In other way, many clients can reuse the same implementation. 
So this allows use to create modular, reusable libraries of algorithms and data structure that we can use to build more complicated algorithms and data structures.

### stacks
![Pasted image 20250117152755.png](/images/Pasted%20image%2020250117152755.png)

the first implementation is to use linked-list.
![Pasted image 20250117153025.png](/images/Pasted%20image%2020250117153025.png)

analysis of performance
have no loop
![Pasted image 20250117153243.png](/images/Pasted%20image%2020250117153243.png)



array implementation
![Pasted image 20250117153727.png](/images/Pasted%20image%2020250117153727.png)
Now there's a fundamental defect in using an array and that is that you have to declare the size of the array ahead of time and then so the stack has a certain capacity.

But we do have to worry in Java about a problem called Loitering(对象游离) and that is the idea that we have references to an object in our array implementation in the stack array when we're not really using it. So when we decrement that value N, there's still a pointer to the thing that we took off the stack in that array. Even though we know we're not using it, the Java system doesn't know that.
![Pasted image 20250117154333.png](/images/Pasted%20image%2020250117154333.png)



### resizing arrays
first thing you might think of is, when the client pushes a new item onto stack, increase the size of the array by 1, and when it pops, decrease the size of the array by 1.
but it's too expensive to do that.
The reason is that you have to create a new array, size one bigger, and copy all the items to that new array.
Inserting first N items takes time proportional to $N^2$

So the well-known technique for doing that, called repeated doubling.
If array is full, create a new array of twice the size, and copy items.
{{< figure src="/images/Pasted image 20250117185355.png"  width="400" height="">}}

Inserting first N items takes time proportional to N
And the reason is that you only create a new array every time it doubles. But by the time that it doubles, you've inserted that many items into the stack. So on average, it's like adding a cost of one to each operation. So if you just calculate the cost of inserting the first N items, you're going to have instead of the sum of the integers from to 1 to N, you're going to have the sum of the powers of 2 from 1 to N. And that'll give a total cost of about 3N.
{{< figure src="/images/Pasted image 20250117185723.png"  width="500" height="">}}
So that's called amortized analysis(平摊分析), where we consider the total cost average over all operations.

shrink array?
the first we consider is half size of array when array is one-half full.
But there is one phenomenon called thrashing(抖动)
{{< figure src="/images/Pasted image 20250117190044.png"  width="500" height="">}}
If the client happens to do push-pop-push-pop alternating when the array if full, then it's going to be doubling, having, doubling, having. Creating new arrays on every operation.
each operation takes time proportional to N.

the efficient solution is to wait until the array gets one-quarter full before you have it.
{{< figure src="/images/Pasted image 20250117190305.png"  width="400" height="">}}

- So the invariant of that is that the array is always between 25% and 100% full.
- the every time you resize, you're already paid for it in an amortized sense by interesting, pushing or popping.

![Pasted image 20250117190719.png](/images/Pasted%20image%2020250117190719.png)
use less memory than linked-list stack.
