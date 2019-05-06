# Programming-language-final-prep

## Lambda expression
1. Is arrow left associative or right associative? f->y->x
<details>
  <summary>answer</summary>
    arrow is right associative. To understand it, let see f->(y->x). It means this function takes a parameter f, and return a function that takes a parameter y and return x.   
    It's easier to understand it by this example:  
    let f x y = x. The type of f is x->y->x. Then the type f x: y->x. That's exactly what happen when x->(y->x).
</details>

2.Is application left associative or right associative? f x y
<details>
  <summary>answer</summary>
   applicaiton is left associaive. f x y = (f x) y.
</details>
3.what is alpha renaming?
4.how to determine whether a occurance is bound or free? 
5.what is beta reduction?
6.what is evaluation strategy? In what kinds of situation we need it?
7.explain normal order
8.explain applicative order
9.prove that plus 1 2 = 3. plus m n =λ m n. m succ n.  succ = λ n s z. s(n s z)
10.prove that exp 2 2 = 4. exp m n = λ m n. n m.
11.prove that pred 1 = 0
