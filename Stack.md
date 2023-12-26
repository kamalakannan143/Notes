[[QA's]]

**How stack works:**
A program contains a calling function. function does something and returns back once the action is done.
Segment of memory where data like local variables is get added/removed. (LIFO - last in first out )
Eg: (static int i=0) or (int a,b;)

#References  https://nickolasteixeira.medium.com/stack-vs-heap-whats-the-difference-and-why-should-i-care-5abc78da1a88 #Pending

**Stack Overflow**
Multiple times of calling an recursive function can eat all of the available memory allocated into stack. So it may occurs a stack overflow.

![[Pasted image 20230723100008.png|550]]

After the memory of buffer get exceeded it will go to the return address and which we wants to achieve.

Because these return address consists of sensitive data

![[Pasted image 20230723115452.png]]

\x90 means move to next 

![[Pasted image 20230723190508.png]]