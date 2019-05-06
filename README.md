# Programming-language-final-prep

## Lambda expression
1. Is arrow left associative or right associative? f->y->x
<details>
  <summary>answer</summar>
    arrow is right associative. To understand it, let see f->(y->x). It means this function takes a parameter f, and return a function that takes a parameter y and return x. 
    It's easier to understand it by this example: 
    let f x y = x. The type of f is x->y->x. Then the type f x: y->x. That's exactly what happen when x->(y->x).
</details>
