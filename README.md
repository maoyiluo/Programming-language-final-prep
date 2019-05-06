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
   plus 1 2 = 1 succ 2 = succ 2 = (λ n s z. s (n s z)) 2 = λ s z. s( 2 s z) = λ s z. s ( (λ s z. s (s z)) s z)  = λ s z. s (s (s z)) = 3
  ```
</details>
  10. prove that exp 2 2 = 4. exp m n = λ m n. n m.
  <details>
  <summary>answer</summary>
  exp 2 2 = (λ m n. n m) 2 2 = (λ n. n 2) 2 = 2 2 = (λ s z. s(s (z)) 2 = λ z. 2 (2 (z) ) = λ z. 2 ((λ s z. s(s(z))) z) =λ s. 2 ((λ s z. s(s(z))) s) = λ s. 2 (λ  z. s(s(z)))  = λ s. (λ s z. s(s(z))) (λ  z. s(s(z))) =  λ s. λ z. (λ  z. s(s(z)) (λ  z. s(s(z)) z) = λ s. λ z. (λ  z. s(s(z)) s(s(z) )  = λ s z. s(s(s(s(z)) = 4.
</details>
  11. prove that pred 1 = 0
  <details>
  <summary>answer</summary>
  pred 1 = snd (1 (λ p. pair( succ (fst p))(fst p))(pair 0 0)) = (λp. p false)
</details>
