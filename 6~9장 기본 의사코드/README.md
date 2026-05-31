# 스택

**스택 초기화 (배열 기반)**

```text
Alg initStack()
1. t <- -1
2. return S

```

**스택 삽입 (배열 기반)**

```text
Alg push(e)
1. if (t = N - 1)
       fullStackException()
2. t <- t + 1
3. S[t] <- e
4. return

```

**스택 삭제 (배열 기반)**

```text
Alg pop()
1. if (isEmpty())
       emptyStackException()
2. t <- t - 1
3. return S[t + 1]

```

**스택 비어있는지 확인 (배열 기반)**

```text
Alg isEmpty()
1. return t = -1

```

**스택 크기 반환 (배열 기반)**

```text
Alg size()
1. return t + 1

```

**스택 맨 위 원소 반환 (배열 기반)**

```text
Alg top()
1. if (isEmpty())
       emptyStackException()
2. return S[t]

```

**스택 초기화 (연결리스트 기반)**

```text
Alg initStack()
1. t <- Ø
2. return

```

**스택 삽입 (연결리스트 기반)**

```text
Alg push(e)
1. p <- getnode()
2. p.elem <- e
3. p.next <- t
4. t <- p
5. return

```

**스택 비어있는지 확인 (연결리스트 기반)**

```text
Alg isEmpty()
1. return t = Ø

```

**스택 삭제 (연결리스트 기반)**

```text
Alg pop()
1. if (isEmpty())
       emptyStackException()
2. e <- t.elem
3. p <- t
4. t <- t.next
5. putnode(p)
6. return e

```

**심볼 균형 검사**

```text
Alg isBalanced()
1. S <- empty stack
2. while (!endOfFile())
       s <- getSymbol()
       if (isOpenSymbol(s))
           S.push(s)
       elseif (isCloseSymbol(s))
           if (S.isEmpty())
               return False
           t <- S.pop()
           if (!isCounterpart(s, t))
               return False
3. return S.isEmpty()

```

**기간 계산 알고리즘 (정의 적용)**

```text
Alg spans(X, S, n)
1. for i <- 0 to n - 1
       s <- 1
       while ((s <= i) & (X[i - s] <= X[i]))
           s <- s + 1
       S[i] <- s
2. return

```

**기간 계산 알고리즘 (스택 사용)**

```text
Alg spans(X, S, n)
1. A <- empty stack
2. for i <- 0 to n - 1
       while (!A.isEmpty() & (X[A.top()] <= X[i]))
           A.pop()
       if (A.isEmpty())
           S[i] <- i + 1
       else
           S[i] <- i - A.top()
       A.push(i)
3. while (!A.isEmpty())
       A.pop()
4. return

```

**수식 전환 (중위수식 -> 후위수식)**

```text
Alg convert()
1. S <- empty stack
2. while (!endOfFile())
       s <- getSymbol()
       if (isOperand(s))
           write(s)
       elseif (s = '(')
           S.push(s)
       elseif (s = ')')
           while (S.top() != '(')
               write(S.pop())
           S.pop()
       else
           while (!S.isEmpty() & (P[s] <= P[S.top()]))
               write(S.pop())
           S.push(s)
3. while (!S.isEmpty())
       write(S.pop())
4. return

```

**수식 평가 알고리즘**

```text
Alg evaluate()
1. S <- empty stack
2. while (!endOfFile())
       s <- getSymbol()
       if (isOperand(s))
           S.push(s)
       else
           a <- S.pop()
           b <- S.pop()
           S.push(doOperator(s, b, a))
3. write(S.pop())
4. return

```

**연산자 수행 알고리즘**

```text
Alg doOperator(op, x, y)
1. switch (op)
       '+': v <- x + y
       '-': v <- x - y
       '*': v <- x * y
       '/': v <- x / y
2. return v

```

**다중스택 초기화 (1D 배열 사용)**

```text
Alg initMultiStack()
1. stacksize <- N / n
2. for i <- 0 to n - 1
       b[i] <- stacksize * i - 1
       t[i] <- b[i]
3. b[n] <- N - 1
4. return

```

**다중스택 크기 반환 (1D 배열 사용)**

```text
Alg size(i)
1. return t[i] - b[i]

```

**다중스택 비어있는지 확인 (1D 배열 사용)**

```text
Alg isEmpty(i)
1. return t[i] = b[i]

```

**다중스택 만원인지 확인 (1D 배열 사용)**

```text
Alg isFull(i)
1. return t[i] = b[i + 1]

```

**다중스택 맨 위 원소 반환 (1D 배열 사용)**

```text
Alg top(i)
1. if (isEmpty(i))
       emptyStackException()
2. return A[t[i]]

```

**다중스택 삽입 (1D 배열 사용)**

```text
Alg push(i, e)
1. if (isFull(i))
       fullStackException(i)
2. t[i] <- t[i] + 1
3. A[t[i]] <- e
4. return

```

**다중스택 삭제 (1D 배열 사용)**

```text
Alg pop(i)
1. if (isEmpty(i))
       emptyStackException()
2. t[i] <- t[i] - 1
3. return A[t[i] + 1]

```

**다중스택 초기화 (연결리스트 배열 사용)**

```text
Alg initMultiStack()
1. for i <- 0 to n - 1
       t[i] <- Ø
2. return

```

**다중스택 비어있는지 확인 (연결리스트 배열 사용)**

```text
Alg isEmpty(i)
1. return t[i] = Ø

```

**다중스택 맨 위 원소 반환 (연결리스트 배열 사용)**

```text
Alg top(i)
1. if (isEmpty(i))
       emptyStackException()
2. return t[i].elem

```

**다중스택 삽입 (연결리스트 배열 사용)**

```text
Alg push(i, e)
1. q <- getnode()
2. q.elem <- e
3. q.next <- t[i]
4. t[i] <- q
5. return

```

**다중스택 삭제 (연결리스트 배열 사용)**

```text
Alg pop(i)
1. if (isEmpty(i))
       emptyStackException()
2. e <- t[i].elem
3. q <- t[i]
4. t[i] <- t[i].next
5. putnode(q)
6. return e

```

---

# 큐

**빈 큐 확인 (배열 기반)**

```text
Alg isEmpty()
1. return (r + 1) % N = f

```

**만원 큐 확인 (배열 기반)**

```text
Alg isFull()
1. return (r + 2) % N = f

```

**큐 초기화 (배열 기반)**

```text
Alg initQueue()
1. f <- 0
2. r <- N - 1
3. return

```

**큐 삽입 (배열 기반)**

```text
Alg enqueue(e)
1. if (isFull())
       fullQueueException()
2. r <- (r + 1) % N
3. Q[r] <- e
4. return

```

**큐 삭제 (배열 기반)**

```text
Alg dequeue()
1. if (isEmpty())
       emptyQueueException()
2. e <- Q[f]
3. f <- (f + 1) % N
4. return e

```

**큐 크기 확인 (배열 기반)**

```text
Alg size()
1. return (N - f + r + 1) % N

```

**큐 앞 원소 확인 (배열 기반)**

```text
Alg front()
1. if (isEmpty())
       emptyQueueException()
2. return Q[f]

```

**큐 초기화 (연결리스트 기반)**

```text
Alg initQueue()
1. f, r <- Ø
2. return

```

**빈 큐 확인 (연결리스트 기반)**

```text
Alg isEmpty()
1. return f = Ø

```

**큐 삽입 (연결리스트 기반)**

```text
Alg enqueue(e)
1. p <- getnode()
2. p.elem <- e
3. p.next <- Ø
4. if (isEmpty())
       f, r <- p
   else
       r.next <- p
       r <- p
5. return

```

**큐 삭제 (연결리스트 기반)**

```text
Alg dequeue()
1. if (isEmpty())
       emptyQueueException()
2. e <- f.elem
3. p <- f
4. f <- f.next
5. if (f = Ø)
       r <- Ø
6. putnode(p)
7. return e

```

---

# 트리

**노드의 깊이 확인**

```text
Alg depth(v)
1. if (isRoot(v))
       return 0
   else
       return 1 + depth(parent(v))

```

**노드의 높이 확인**

```text
Alg height(v)
1. if (isExternal(v))
       return 0
   else
       h <- 0
       for each w ∈ children(v)
           h <- max(h, height(w))
       return 1 + h

```

**선위순회**

```text
Alg preOrder(v)
1. visit(v)
2. for each w ∈ children(v)
       preOrder(w)

```

**구조적 문서 목차 인쇄**

```text
Alg printTableOfContents(v)
1. rPrint(v, 0)
2. return

```

**목차 인쇄 보조 알고리즘**

```text
Alg rPrint(v, d)
1. for i <- 1 to d
       write(Tab)
2. write(element(v))
3. for each w ∈ children(v)
       rPrint(w, d + 1)
4. return

```

**후위순회**

```text
Alg postOrder(v)
1. for each w ∈ children(v)
       postOrder(w)
2. visit(v)

```

**디스크 사용량 계산**

```text
Alg diskUsage(v)
1. sum <- 0
2. for each w ∈ children(v)
       sum <- sum + diskUsage(w)
3. return sum + space(v)

```

**레벨순회**

```text
Alg levelOrder(v)
1. Q <- empty queue
2. Q.enqueue(v)
3. while (!Q.isEmpty())
       v <- Q.dequeue()
       visit(v)
       for each w ∈ children(v)
           Q.enqueue(w)
4. return

```

**계층구조 인쇄**

```text
Alg printHierarchy(v)
1. Q <- empty queue
2. Q.enqueue(v)
3. while (!Q.isEmpty())
       v <- Q.dequeue()
       write(depth(v), element(v))
       for each w ∈ children(v)
           Q.enqueue(w)
4. return

```

**이진트리 선위순회**

```text
Alg binaryPreOrder(v)
1. visit(v)
2. if (isInternal(v))
       binaryPreOrder(leftChild(v))
       binaryPreOrder(rightChild(v))

```

**이진트리 후위순회**

```text
Alg binaryPostOrder(v)
1. if (isInternal(v))
       binaryPostOrder(leftChild(v))
       binaryPostOrder(rightChild(v))
2. visit(v)

```

**수식 평가 알고리즘**

```text
Alg evalExpr(v)
1. if (isExternal(v))
       return element(v)
   else
       x <- evalExpr(leftChild(v))
       y <- evalExpr(rightChild(v))
       ◊ <- element(v)
       return x ◊ y

```

**중위순회**

```text
Alg inOrder(v)
1. if (isInternal(v))
       inOrder(leftChild(v))
2. visit(v)
3. if (isInternal(v))
       inOrder(rightChild(v))

```

**이진트리 그리기**

```text
Alg drawBinaryTree(v)
1. rDBT(v, 0)

```

**이진트리 그리기 보조 알고리즘**

```text
Alg rDBT(v, rank)
1. if (isInternal(v))
       rDBT(leftChild(v), rank)
2. rank <- rank + 1
   drawNodeXY(v, rank, depth(v))
3. if (isInternal(v))
       rDBT(rightChild(v), rank)

```

**수식 인쇄 알고리즘**

```text
Alg printExpr(v)
1. if (isInternal(v))
       write('(')
       printExpr(leftChild(v))
2. write(element(v))
3. if (isInternal(v))
       printExpr(rightChild(v))
       write(')')

```

**오일러 투어 순회**

```text
Alg eulerTour(v)
1. visitLeft(v)
2. if (isInternal(v))
       eulerTour(leftChild(v))
3. visitBelow(v)
4. if (isInternal(v))
       eulerTour(rightChild(v))
5. visitRight(v)

```

**부트리 크기 구하기 알고리즘 모음**

```text
Alg findSizeOfSubtrees(v)
1. k <- 0
2. eulerTour(v)

Alg visitLeft(v)
1. k <- k + 1
2. v.kleft <- k

Alg visitBelow(v)
1. return

Alg visitRight(v)
1. v.size <- k - v.kleft + 1

```

**배열 기반 이진트리 메쏘드들**

```text
Alg element(v)
1. return T[v]

Alg root()
1. return 1

Alg isRoot(v)
1. return v = 1

Alg parent(v)
1. return v / 2

Alg leftChild(v)
1. return 2v

Alg rightChild(v)
1. return 2v + 1

Alg sibling(v)
1. if (even(v))
       return v - 1
   else
       return v + 1

Alg isInternal(v)
1. return (2v < N) & (T[2v] != Null)

Alg isExternal(v)
1. return (2v >= N) || (T[2v] = Null)

Alg setElement(v, e)
1. T[v] <- e
2. return e

Alg swapElements(v, w)
1. tmp <- T[v]
2. T[v] <- T[w]
3. T[w] <- tmp
4. return

```

**연결 이진트리 메쏘드들**

```text
Alg element(v)
1. return v.elem

Alg root()
1. return root

Alg isRoot(v)
1. return v = root

Alg parent(v)
1. return v.parent

Alg leftChild(v)
1. return v.left

Alg rightChild(v)
1. return v.right

Alg sibling(v)
1. p <- v.parent
2. if (p.left = v)
       return p.right
   else
       return p.left

Alg isInternal(v)
1. return (v.left != Ø) & (v.right != Ø)

Alg isExternal(v)
1. return (v.left = Ø) & (v.right = Ø)

Alg setElement(v, e)
1. v.elem <- e
2. return e

Alg swapElements(v, w)
1. tmp <- v.elem
2. v.elem <- w.elem
3. w.elem <- tmp
4. return

```

**연결트리 (Ver.2) 메쏘드들**

```text
Alg element(v)
1. return v.elem

Alg root()
1. return root

Alg isRoot(v)
1. return v = root

Alg parent(v)
1. return v.parent

Alg children(v)
1. C <- Ø
2. c <- v.first
3. while (c != Ø)
       C <- C U {c}
       c <- c.next
4. return C

Alg isInternal(v)
1. return v.first != Ø

Alg isExternal(v)
1. return v.first = Ø

Alg setElement(v, e)
1. v.elem <- e
2. return e

Alg swapElements(v, w)
1. tmp <- v.elem
2. v.elem <- w.elem
3. w.elem <- tmp
4. return

```

**선위순회 계승자 구하기**

```text
Alg preOrderSucc(v)
1. if (isInternal(v))
       return leftChild(v)
2. p <- parent(v)
3. while (leftChild(p) != v)
       if (isRoot(p))
           invalidNodeException()
       v <- p
       p <- parent(p)
4. return rightChild(p)

```

**중위순회 계승자 구하기**

```text
Alg inOrderSucc(v)
1. if (isInternal(v))
       v <- rightChild(v)
       while (isInternal(v))
           v <- leftChild(v)
       return v
2. p <- parent(v)
3. while (leftChild(p) != v)
       if (isRoot(p))
           invalidNodeException()
       v <- p
       p <- parent(p)
4. return p

```

**후위순회 계승자 구하기**

```text
Alg postOrderSucc(v)
1. if (isRoot(v))
       invalidNodeException()
2. p <- parent(v)
3. if (rightChild(p) = v)
       return p
4. v <- rightChild(p)
5. while (!isExternal(v))
       v <- leftChild(v)
6. return v

```

**로만노드 판별 및 크기 반환**

```text
Alg romanSize(v)
1. if (isExternal(v))
       return 1
2. l <- romanSize(leftChild(v))
3. if (l = 0)
       return 0
4. r <- romanSize(rightChild(v))
5. if ((r > 0) & (|l - r| <= 5))
       return l + r + 1
   else
       return 0

```

**결정트리 구축 (배열 사용)**

```text
Alg buildDecisionTree()
1. write("***Let's build a dichotomous QA system")
2. makeInternalNode(1)
3. return

Alg makeInternalNode(i)
1. write("Enter question: ")
2. T[i] <- read()
3. write("Question if yes to", T[i], "?")
4. if (read() = "yes")
       makeInternalNode(2i)
   else
       makeExternalNode(2i)
5. write("Question if no to", T[i], "?")
6. if (read() = "yes")
       makeInternalNode(2i + 1)
   else
       makeExternalNode(2i + 1)
7. return

Alg makeExternalNode(i)
1. write("Enter decision: ")
2. T[i] <- read()
3. if (2i < N)
       T[2i], T[2i + 1] <- Null
4. return

```

**결정트리 구축 (연결리스트 사용)**

```text
Alg buildDecisionTree()
1. write("***Let's build a dichotomous QA system")
2. return makeInternalNode()

Alg makeInternalNode()
1. v <- getnode()
2. write("Enter question: ")
3. v.elem <- read()
4. write("Question if yes to", v.elem, "?")
5. if (read() = "yes")
       v.left <- makeInternalNode()
   else
       v.left <- makeExternalNode()
6. write("Question if no to", v.elem, "?")
7. if (read() = "yes")
       v.right <- makeInternalNode()
   else
       v.right <- makeExternalNode()
8. return v

Alg makeExternalNode()
1. v <- getnode()
2. write("Enter decision: ")
3. v.elem <- read()
4. v.left, v.right <- Ø
5. return v

```

**결정트리 실행**

```text
Alg runDecisionTree(v)
1. write("***Please answer questions")
2. processNode(v)

Alg processNode(v)
1. write(element(v))
2. if (isInternal(v))
       if (read() = "yes")
           processNode(leftChild(v))
       else
           processNode(rightChild(v))

```

---

# 분리집합

**find 연산 (배열 사용)**

```text
Alg find(e)
1. return S[e]

```

**union 연산 (배열 사용)**

```text
Alg union(x, y)
1. for i <- 0 to n - 1
       if (S[i] = y)
           S[i] <- x
2. return

```

**find 연산 (연결리스트 사용)**

```text
Alg find(e)
1. return setid((node(e).set).elem)

```

**union 연산 (연결리스트 사용)**

```text
Alg union(A, B)
1. if (S[A].size < S[B].size)
       smallerSet, largerSet <- A, B
   else
       smallerSet, largerSet <- B, A
2. headS, tailS <- S[smallerSet].head, S[smallerSet].tail
3. headL, tailL <- S[largerSet].head, S[largerSet].tail
4. p <- headS
5. while (p != Ø)
       p.set <- headL
       p <- p.next
6. tailL.next <- headS
7. S[largerSet].tail <- tailS
8. S[largerSet].size <- S[A].size + S[B].size
9. S[smallerSet].head, S[smallerSet].tail <- Ø
10. S[smallerSet].size <- 0
11. return

```

**find 연산 (트리 기반)**

```text
Alg find(e)
1. if (Parent[e] = e)
       return e
   else
       return find(Parent[e])

```

**union 연산 (트리 기반)**

```text
Alg union(x, y)
1. Parent[y] <- x
2. return

```

**find 및 union 연산 (경로압축 & 크기 기반 트리)**

```text
Alg find(e)
1. if (Parent[e] = e)
       return e
   else
       Parent[e] <- find(Parent[e])
       return Parent[e]

Alg union(x, y)
1. if (Size[x] < Size[y])
       Parent[x] <- y
       Size[y] <- Size[x] + Size[y]
   else
       Parent[y] <- x
       Size[x] <- Size[x] + Size[y]
3. return

```

**union 연산 (높이 기반 합집합)**

```text
Alg union(x, y)
1. if (Height[x] < Height[y])
       Parent[x] <- y
   else
       Parent[y] <- x
2. if (Height[x] = Height[y])
       Height[x] <- Height[x] + 1
3. return

```

**find 연산 (부분적 경로압축 적용)**

```text
Alg find(e)
1. p <- e
2. while (Parent[p] != p)
       par <- Parent[p]
       if (Parent[par] != par)
           Parent[p] <- Parent[par]
       p <- par
3. return p

```
