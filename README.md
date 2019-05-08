# Programming-language-final-prep

## Lambda expression
 1. Is arrow left associative or right associative? f->y->x
  <details>
   <summary>answer</summary>
    arrow is **right associative**. 
    To understand it, let see f->(y->x). It means this function takes a parameter f, and return a function that takes a parameter y and return x. It's easier to understand it by this example. let f x y = x. The type of f is x->y->x. Then the type f x: y->x. That's exactly what happen when x->(y->x).
  </details>
  2. Is application left associative or right associative? f x y
<details>
  <summary>answer</summary>
   applicaiton is left associaive. f x y = (f x) y.
</details>
  3. what is alpha renaming?
  <details>
  <summary>answer</summary>
   λ x. t(x,z). We can see that in this lambda expression, z is free occurance and x is bound in the  λ x. Alpha renaming means we can rename the bound occurance x if the rename do not cause conflict( like using a name that has been used by some another variable.
</details>
  4. how to determine whether a occurance is bound or free? 
  <details>
  <summary>answer</summary>
   we need to figure out the scope of each lambda expression. like ((λ y. (λ x. t x) x). We can see that the first 'x' is bound by the parameter x. But the lambda expression (λ x. t x) only bound the x in the body of this function. the second 'x' is free variable since in the outmose function y is the bound variable
</details>
  5. what is beta reduction?
  <details>
  <summary>answer</summary>
   beta reduction is like evaluation of an application. For example, (λ x. t x) y is an application, function (λ x. t x)  takes a parameter y and should return something. In this case, it's t y.
</details>
  6. what is evaluation strategy? In what kinds of situation we need it?
  <details>
  <summary>answer</summary>
   evaluation strategy is like call by name or call by value. Consider this situation (λ x. t x) ((λ z. z) y). This is an application, however, the parameter of the frist function is another application. Therefore we have two choice, one is we evaluate the application (λ z. z) y before we pass it, like (λ z. z) y = y ,  (λ x. t x) ((λ z. z) y) = (λ x. t x) y = t y. The second choice is we pass the whole expression in to the body, like (λ x. t x) ((λ z. z) y) = t ((λ z. z) y) = t y.
</details>
  7. explain normal order
  <details>
  <summary>answer</summary>
   normal order is call by name. It means instead of evaluate the value of parameter, it pass the whole expression of parameter
</details>
  8. explain applicative order
  <details>
  <summary>answer</summary>
   applicative order is call by value. It means we evaluate the parameter before we pass it into a function.
</details>
  9. prove that plus 1 2 = 3. plus m n =λ m n. m succ n.  succ = λ n s z. s(n s z)
  <details>
  <summary>answer</summary>
    
  ```
   plus 1 2 
   = 1 succ 2 
   = succ 2 
   = (λ n s z. s (n s z)) 2 
   = λ s z. s( 2 s z) 
   = λ s z. s ( (λ s z. s (s z)) s z)  
   = λ s z. s (s (s z)) = 3
  ```
</details>
  10. prove that exp 2 2 = 4. exp m n = λ m n. n m.
  <details>
  <summary>answer</summary>
  
  ```
  exp 2 2 = (λ m n. n m) 2 2 
  = (λ n. n 2) 2 = 2 2 
  = (λ s z. s(s (z)) 2 
  = λ z. 2 (2 (z)) 
  = λ z. 2 ((λ s z. s(s(z))) z) 
  = λ s. 2 ((λ s z. s(s(z))) s) 
  = λ s. 2 (λ  z. s(s(z)))  
  = λ s. (λ s z. s(s(z))) (λ  z. s(s(z))) 
  =  λ s. λ z. (λ  z. s(s(z)) (λ  z. s(s(z)) z) 
  = λ s. λ z. (λ  z. s(s(z)) s(s(z) )  
  = λ s z. s(s(s(s(z)) = 4.
  ```
</details>
  11. prove that pred 1 = 0
  <details>
  <summary>answer</summary>
  
  ```
  pred 1 
  = snd (1 (λ p. pair( succ (fst p))(fst p))(pair 0 0)) 
  = (λp. p false)((λ s z. s z) (λ p. pair( succ (fst p))(fst p))(pair 0 0))
  = (λp. p false)((λ p. pair(succ (fst p))(fst p)) (pair 0 0))
  = (λp. p false)((λ p. (λ x y b. b x y)(succ (fst p))(fst p)) (pair 0 0))
  = (λp. p false)((λ p. λb. b(succ (fst p))(fst p)) (pair 0 0))
  = (λp. p false)((λ p. λb. b (succ (fst p))(fst p)) (λ z. z 0 0))
  = (λp. p false)((λ p. λb. b (succ ((λy. y true) p))((λy. y true) p)) (λ z. z 0 0))
  = (λp. p false)((λ p. λb. b (succ ((λy. y true) p))((λy. y true) p)) (λ z. z 0 0))
  = (λp. p false)((λ p. λb. b (succ (p true))(p true)) (λ z. z 0 0))
  = (λp. p false)((λ p. λb. b ((λ n s z. s(n s z)) (p true))(p true)) (λ z. z 0 0))
  = (λp. p false)((λ p. λb. b ((λs z. s((p true) s z)))(p true)) (λ z. z 0 0))
  = (λp. p false)(λb. b ((λs z. s(0 s z))) 0)
  = (λp. p false)(λb. b 1 0)
  = (λb. b 1 0) false
  = 0
  ```
</details>

## generic type

1. What is scala generics? How to implement？
  <details>
    <summary>answer</summary>
      generics is that a class can take a type as parameter. To implement it in scala, use [A]:
      
      class Queue[A] private (private val queue: List[A]) {
       def enqueue(x: A): Queue[A] = new Queue[A](queue :+ x)

       def dequeue: (A, Queue[A]) = {
        require(!isEmpty, "Queue.dequeue on empty queue")
        val x :: queue1 = queue(x, new Queue(queue1))
        }

     def isEmpty: Boolean = queue.isEmpty

      override def toString: String = {s"Queue${queue.toString.drop(4)}}
      }
  </details>
2. What is the three types of relationship between the generics of super class and subclass? If `T <: S`, what is the relationship between `C[T]` and `C[S]`?
  <details>
  <summary>answer</summary>
      There are three types of relationship:
        - covariant:`C[T] <: C[S]`
        - contravariant: `C[T] :> C[S]`
        - invariant: no specific relationship between these two classes. ***Default***
  </details>
3. How to make a generics type covariant or contravariant?
<details>
		<summary>answer</summary>
				
    class generics[+A]: covariant
    class generics[-A]: contravariant
				
</details>

4. here are some examples to explain why sometimes covariant or contravariant will go wrong.
First of all, our goal is to **let the compiler find the error at compiling time.**
```scala
class CoVar[+T](x: T) {
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)
}

class ContraVar[-T](x: T) {
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)
}
```
So we can see that there has some error in the definition of these two class. `CoVar` has a parameter `y:T` at the contravariant position, and `ContraVar` returns `T` at a covariant positon. Here is the code to show how it can go wrong:
```scala
class CoVar[+T](x: T) {
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)
}

class C extend CoVar[String]{
  overrided method2(y: String): List[String] = {
   println(y.length)
   List[String] = List(x,y)
  }
}

val c1 = new C("hello")
val c2:CoVar[Any] = c1 //Ok because CoVar[Any] >: CoVar[String] >: C
c2.method2(1) //OK at complie time because integer is Anytype.
```
But the program will crash at runtime because c2.method2 will be dynamic dispatched to the method2 in `C`, and it tries to get the length of an integer. To solve this problem(I mean we hope compiler can detect the error) we have to add some constraints to the parameter of method2:
```scala
class CoVar[+T](x: T) {
  def method1: T = x
  def method2[U>:T](y: U): List[T] = List(x,y)
}

class C extend CoVar[String]{
  overrided method2[U>:String](y: U): List[U] = {
   println(y.length) //compiler will find  that this line has error.
   List[U] = List(x,y)
  }
}

val c1 = new C("hello")
val c2:CoVar[Any] = c1 //Ok because CoVar[Any] >: CoVar[String] >: C
c2.method2(1) //OK at complie time because integer is Anytype.
```
This time when we override method 2 we have to set the same constraint on U. Therefore this time complier will detect that we are calling something that only the avalible in String but we only know U is String or its supertype, so it finds the error.
Here is the example that why the `ContraVar` is wrong:
```scala
class ContraVar[-T](x: T) {
  def method1: T = x
  def method2(y: T): List[T] = List(x,y)
}

val c1 = new ContraVar[Any](1)
val c2:ContraVar[String] = c1 //OK because Any >: String so ContraVar[Any] <: ContraVar[String]
c2.method1().length // here T = String, so it should be ok at compile time
```
It's clear that it will crash at runtime.
```scala
class ContraVar[-T,U>:T](x: T) {
  def method1: U = x
  def method2(y: T): List[U] = List(x,y)
}

val c1 = new ContraVar[Any,Any](1)
val c2:ContraVar[String,Any] = c1 // U has to be a supertype of String so I set it to Any.
c2.method1().length // compiler will find it's wrong because we are asking for length at a object with type Any!
```
5. the **involuted** upper bound and lower bound
First of all I claim these two statement:
- `covariant` promise a `upper bound` return type. The return type m should be the type T itself or T's subtype.
- `contravariant` promise a `lower bound` input type. The input type m should be the type T or T's subtype.  

It's really confusing to see that we are using different word to describe the same thing: type m should be type T or T's subtype. So here is my personal understanding, I can't guarantee that it's correct but it can somehow help me to remember these two statement.

we know that for `covariant`, if `T <: S`, then `C[T] <: C[S]`. Therefore if `m <: T`, then `C[m]<:C[T]`. This should somehow explain why it's the `upper bound`. For `contravariant`, if `m<:T`, then `C[m]>:C[T]`. That's why we call it `lower bound`.
## memory management
1. clarify some definition:
- constructor: Just constructor, nothing special
- Copy construtor: When we declare a new variable, if we are using this way `p e = q`, then we are calling a copy constructor.
```c++
p a;
p b = a; //copy constructor
```
- assignment: This operation is for two variable that **has been declared** like 
 ```c++
 p a;
 p b;
 a = b; //assginment
 ```
 2. shallow copy or deep copy
 - for shallow copy, we create a reference to the existance object. **Only one object on the heap**
 - for deep copy, we create a exactly the same object on the heap. **Two object on the heap**
