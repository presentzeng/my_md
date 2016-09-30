 [1.基本语法](#1)  
 [2.得到的启发](#2)

<h2 id="1">1.基本语法</h2>


1. expressions
> `(op p1 p2 p3 ...)`

	
	input:		(+ 2 3)
	output:		5
	

	
	input:		(/ 6 2)
	output:		3
	
2. Define function

> `(define (<name> <formal parameters>) <body>)`

	
	input:		(define (square x) (* x x))
				(square 4)
	output:		16
	

3. Conditional Expressions
> `(cond (<p> <e>))`

	
	(define (abs x)
		(cond ((> x 0) x)
			  ((= x 0) 0)
			  ((< x 0) (- x))))
	

4. if-else
> `(if <predicate> <consequent> <alternative>)`

	
	(define (abs x)
		(if	(< x 0)
			(- x)
			x))
	


5. and or not
> `(and <e1> <e2>)  (or <e1> <e2>) (not <e>)`

    
	(define (>= x y)
		(or (> x y) (= x y)))
	

6. random  
	```
	random 9
	```

7. let  
	```
	(define (test)
		(let ((a 1))
		(+ a 4)))   ;;这里a已经被赋值成1
	```

8. remainder
	```
	remainder 4 1 求余数
	```

9. 内部定义
	```
	(define (func a b)
    	(define (test a)
    		(+ a 1))
    (test b))
	```
	定义一个func,然后再内部再定义一个,结尾调用

	且这个包含可以无线递归下去
	如
	```
	(define (func a b)
   	 (define (test a)
   	  (define (my n)
      (+ n 1))
    (my 2))
    (test 3))

	(func 1 2)

	```


10. lambda
	```
	(define func (lambda (x) (+ x 4)))
	```


11. 循环定义
    ```
	(((lambda (x) (lambda (y) (+ x y))) 1) 2)
	```
	


12. if_version2
	```
	(if ...)
		(begin
			(...)
			(...)		
	
	```

13. (cadr x) = (car (cdr x))


14. 在递归比较精度的时候采用了差值方式,如下

	`guess - x < 0.001`

	这样会在x很大的时候出问题,因为会一直尝试递归以达到精度要求
	导致进入死循环

	改成比例相关的即可

	`(guess -x) / x < 0.001`



15. log  
	在scheme里面,log就是以自然常数e为底的
	

16. pair
	```
	(define p (cons 4 5))
	(car p) 4  (cdr p) 5
	(set-cdr! p "yes")
	(cdr p) yes
	```
	

17. filter
	
	```
	(filter even? (list 1 2 3 4))
	(2, 4)
	```

18. `cdr只能对cons用cadr只能对list用`

19. map
	```
	(map proc list)
	proc会去遍历list的第一层
	
	map display '(1 2 3）
	打印: 1 2 3

	map display '(1 (2 3) 4)
	打印: 1然后报错因为(2 3)非数字
	```

	
> map还有另外一种功能
	```
	(map * '(1 2 3) (2 3 4) (3 4 5))
	(6 24 60)

	```
20. 若一时无法想到如何完成递归,可以试着写出等价表达式

21. 设计模式
	```
	(define (accumulate op init list)
   	(if (null? list)
       init
       (op
        (car list)
        (accumulate op init (cdr list)))))
	
	;;(op list1 (op list2 (op init)))
	;;从list的最后面开始与init做操作
	```

22. cons
    ```
	(cons 2 (cons 1 '())) --> (2 1)
	(cons (cons 2 '()) 1)  --> ((2) . 1)
	(cons 2 3)  --> (2 . 3)
	(cons 2 '(3)) --> (2 3)
	```
### Applicative & normal order
normal         : fully expand and then reduce  
Applicative	   :evaluate the arguments and then apply

### 基于mit-scheme的一些例子

1. a的值为2而不是100

    
	(define (func a b c)
	(if (< c 2)
      (func (+ a 1) (+ a 99) (+ 1 c))
      a))


2. 进入死循环


	(define (inc x)
 		(+ x 1))
	 (define (dec x)
  		(- x 1))
	 (define (+ a b)
 		(if (= a 0)
   		b
     	(inc (+ (dec a) b))))

3. if是不能加else的,else是和cond配对作为default选项

4. 找bug


	(define (func n)
		n)
	(+ func(- n 1)) 

这里错在func(- n 1)没用括号括起来
### debug技巧

1. trace工具


	(trace op)
	(op ...)