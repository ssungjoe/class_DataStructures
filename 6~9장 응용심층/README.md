# 스택

연습 6-1. 후위수식 변환

- **해설:** 스택을 활용한 알고리즘을 모의실행하면 연산자 우선순위에 따라 괄호 안이 먼저 처리되고, 곱셈/나눗셈이 덧셈/뺄셈보다 먼저 처리되어 결과적으로 `4 3 * 17 3 + 5 6 15 3 / - 1 + * / -` 와 같은 후위 수식이 산출됩니다.

변형 스택 fullStackException (연습 6-2)

```text
Alg fullStackException()
1. for i <- 0 to N - 2
       S[i] <- S[i + 1]
2. t <- t - 1
3. return

```

큰 정수 입출력 알고리즘 (연습 6-3)

```text
Alg getPutBig()
1. S <- empty stack
2. getBig(S)
3. putBig(S)
4. return

Alg getBig(S)
1. while (!endOfLine())
       c <- readChar()
       S.push(cToD(c))
2. return

Alg putBig(S)
1. C <- empty stack
2. while (!S.isEmpty())
       C.push(S.pop())
3. while (!C.isEmpty())
       writeChar(dToC(C.pop()))
4. return

```

_최소값 지원 스택 (심층 6-1_) \*

```text
Alg push(e)
1. S.push(e)
2. if (M.isEmpty() | e <= M.top())
       M.push(e)
3. return

Alg pop()
1. e <- S.pop()
2. if (e = M.top())
       M.pop()
3. return e

Alg findMin()
1. return M.top()

```

_원형배열 변형 스택 (심층 6-2_) \*

```text
Alg initStack()
1. t <- 0
2. n <- 0
3. return

Alg isEmpty()
1. return n = 0

Alg size()
1. return n

Alg top()
1. if (isEmpty())
       emptyStackException()
2. return S[t]

Alg push(e)
1. t <- (t + 1) % N
2. S[t] <- e
3. if (n < N)
       n <- n + 1
4. return

Alg pop()
1. if (isEmpty())
       emptyStackException()
2. e <- S[t]
3. t <- (t - 1 + N) % N
4. n <- n - 1
5. return e

```

_후위수식 우향 연산자 확장 (심층 6-3_) \*

- **해설:** 배열 P에 `^` 연산자의 우선순위를 가장 높게(예: 3) 추가합니다. `convert` 알고리즘에서는 top의 연산자와 현재 연산자의 우선순위가 같을 때 좌향(LtoR)이면 pop하지만, `isRToL`이 참(우향)이면 pop하지 않고 스택에 push하도록 분기문을 `while (!S.isEmpty() & (P[s] < P[S.top()] | (P[s] = P[S.top()] & !isRToL(s))))` 와 같이 수정합니다. `doOperator`에는 `^` 분기를 추가해 거듭제곱을 수행합니다.

```text
{우선순위 P: 첨자는 '(' '+' '-' '*' '/' '^' 에 대응}
P: array[0..5] of integers = (0, 1, 1, 2, 2, 3)

Alg isRToL(o)
1. return o = '^'                       {^ 만 우결합(right-to-left)}

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
           while (!S.isEmpty() & (P[s] < P[S.top()] | (P[s] = P[S.top()] & !isRToL(s))))
               write(S.pop())
           S.push(s)
3. while (!S.isEmpty())
       write(S.pop())
4. return

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

Alg doOperator(op, x, y)
1. switch (op)
       '+': v <- x + y
       '-': v <- x - y
       '*': v <- x * y
       '/': v <- x / y
       '^': v <- x ^ y
2. return v

```

- **핵심:** `convert`의 pop 조건만 바뀝니다. 좌결합 연산자는 우선순위가 같을 때 pop(좌결합), `^`는 `isRToL`이 참이라 우선순위가 같으면 pop하지 않고 push → 우결합. `evaluate`는 후위수식을 처리하므로 결합성과 무관하게 기존과 동일하고, `doOperator`에만 `^` 분기를 추가하면 됩니다. (예: `2 ^ 3 ^ 2` → 후위 `2 3 2 ^ ^` → 2^(3^2)=512)

_이중스택 알고리즘 (심층 6-4_) \*

```text
Alg isFull()
1. return t1 + 1 = t2

Alg top(i)
1. if (i = 1)
       return S[t1]
   else
       return S[t2]

Alg push(i, e)
1. if (isFull())
       fullStackException()
2. if (i = 1)
       t1 <- t1 + 1
       S[t1] <- e
   else
       t2 <- t2 - 1
       S[t2] <- e
3. return

Alg pop(i)
1. if (i = 1)
       e <- S[t1]
       t1 <- t1 - 1
       return e
   else
       e <- S[t2]
       t2 <- t2 + 1
       return e

```

다중스택 부동베이스 이동 (심층 6-5)

```text
Alg moveStacksLeft(l, r)
1. for k <- l to r
       for j <- b[k] to t[k]
           S[j - 1] <- S[j]
       b[k] <- b[k] - 1
       t[k] <- t[k] - 1
2. return

Alg moveStacksRight(l, r)
1. for k <- r downto l
       for j <- t[k] downto b[k]
           S[j + 1] <- S[j]
       b[k] <- b[k] + 1
       t[k] <- t[k] + 1
2. return

Alg fullStackException(i)
1. for k <- i - 1 downto 0
       if (!isFull(k))
           moveStacksLeft(k + 1, i)
           return
2. for k <- i + 1 to n - 1
       if (!isFull(k))
           moveStacksRight(i + 1, k)
           return
3. return

```

큰 정수 연산 (심층 6-6)

```text
Alg addBig(A, B, C)
1. carry <- 0
2. T <- empty stack
3. while (!A.isEmpty() | !B.isEmpty() | carry > 0)
       sum <- carry
       if (!A.isEmpty()) sum <- sum + A.pop()
       if (!B.isEmpty()) sum <- sum + B.pop()
       T.push(sum % 10)
       carry <- sum / 10
4. while (!T.isEmpty())
       C.push(T.pop())
5. return

Alg subBig(A, B, C)
1. borrow <- 0
2. T <- empty stack
3. while (!A.isEmpty())
       diff <- A.pop() - borrow
       if (!B.isEmpty())
           diff <- diff - B.pop()
       if (diff < 0)
           diff <- diff + 10
           borrow <- 1
       else
           borrow <- 0
       T.push(diff)
4. while (!T.isEmpty())
       C.push(T.pop())
5. return

Alg isBigger(A, B)
1. sA <- 0
2. sB <- 0
3. TA <- empty stack
4. TB <- empty stack
5. while (!A.isEmpty())
       TA.push(A.pop())
       sA <- sA + 1
6. while (!B.isEmpty())
       TB.push(B.pop())
       sB <- sB + 1
7. isB <- False
8. decided <- False
9. if (sA > sB)
       isB <- True
       decided <- True
   elseif (sA < sB)
       isB <- False
       decided <- True
10. while (!TA.isEmpty() & !TB.isEmpty())
       a <- TA.pop()
       b <- TB.pop()
       A.push(a)
       B.push(b)
       if (!decided)
           if (a > b)
               isB <- True
               decided <- True
           elseif (a < b)
               isB <- False
               decided <- True
11. while (!TA.isEmpty())
       A.push(TA.pop())
12. while (!TB.isEmpty())
       B.push(TB.pop())
13. return isB

```

---

# 큐

변수 n을 이용한 원형큐 (연습 7-1)

```text
Alg initQueue()
1. f <- 0
2. r <- 0
3. n <- 0
4. return

Alg size()
1. return n

Alg isEmpty()
1. return n = 0

Alg isFull()
1. return n = N

Alg front()
1. if (isEmpty())
       emptyQueueException()
2. return Q[f]

Alg enqueue(e)
1. if (isFull())
       fullQueueException()
2. Q[r] <- e
3. r <- (r + 1) % N
4. n <- n + 1
5. return

Alg dequeue()
1. if (isEmpty())
       emptyQueueException()
2. e <- Q[f]
3. f <- (f + 1) % N
4. n <- n - 1
5. return e

```

헤더와 트레일러를 이용한 연결큐 (연습 7-2)

```text
Alg initQueue()
1. H <- getnode()
2. T <- getnode()
3. H.next <- T
4. T.prev <- H
5. return

Alg isEmpty()
1. return H.next = T

Alg front()
1. if (isEmpty())
       emptyQueueException()
2. return H.next.elem

Alg enqueue(e)
1. p <- getnode()
2. p.elem <- e
3. p.prev <- T.prev
4. p.next <- T
5. T.prev.next <- p
6. T.prev <- p
7. return

Alg dequeue()
1. if (isEmpty())
       emptyQueueException()
2. p <- H.next
3. e <- p.elem
4. H.next <- p.next
5. p.next.prev <- H
6. putnode(p)
7. return e

```

큐 뒤집기 (연습 7-3)

```text
Alg reverseQueue(Q)
1. S <- empty stack
2. while (!Q.isEmpty())
       S.push(Q.dequeue())
3. while (!S.isEmpty())
       Q.enqueue(S.pop())
4. return

```

상각실행시간 분석 (연습 7-4, 7-5)

- **7-4 해설:** 전체 n회 작업의 최악시간이 O(n log n)이므로 이를 n으로 나눈 상각실행시간은 O(log n)입니다. 하지만 1회 작업의 최악 실행시간은 단일 작업에 대한 상한이므로, 전체 n회의 작업이 몰릴 수 있는 최악의 시나리오를 상정할 때 O(n log n)이 될 수 있습니다.

- **7-5 해설:** 콩예의 주장은 틀렸습니다. 상각실행시간은 최악의 작업 패턴을 여러 번 수행했을 때의 '평균' 비용을 의미하므로 실제 개별 연산 실행시간의 상한 역할을 하며, 실행시간의 하한을 나타내는 개념이 아닙니다.

원형데크 알고리즘 (심층 7-1)

```text
Alg push(e)
1. if (isFull())
       fullDequeException()
2. f <- (f - 1 + N) % N
3. D[f] <- e
4. return

Alg pop()
1. if (isEmpty())
       emptyDequeException()
2. e <- D[f]
3. f <- (f + 1) % N
4. return e

Alg inject(e)
1. if (isFull())
       fullDequeException()
2. D[r] <- e
3. r <- (r + 1) % N
4. return

Alg eject()
1. if (isEmpty())
       emptyDequeException()
2. r <- (r - 1 + N) % N
3. return D[r]

```

연결데크 알고리즘 (심층 7-2)

```text
Alg push(e)
1. p <- getnode()
2. p.elem <- e
3. p.prev <- Ø
4. p.next <- f
5. if (isEmpty())
       r <- p
   else
       f.prev <- p
6. f <- p
7. return

Alg pop()
1. if (isEmpty())
       emptyDequeException()
2. e <- f.elem
3. p <- f
4. f <- f.next
5. if (f = Ø)
       r <- Ø
   else
       f.prev <- Ø
6. putnode(p)
7. return e

Alg inject(e)
1. p <- getnode()
2. p.elem <- e
3. p.next <- Ø
4. p.prev <- r
5. if (isEmpty())
       f <- p
   else
       r.next <- p
6. r <- p
7. return

Alg eject()
1. if (isEmpty())
       emptyDequeException()
2. e <- r.elem
3. p <- r
4. r <- r.prev
5. if (r = Ø)
       f <- Ø
   else
       r.next <- Ø
6. putnode(p)
7. return e

```

_(inject·eject는 push·pop과 front↔rear 대칭이다: 포인터 next↔prev, f↔r를 맞바꾼 형태)_

두 스택 합동큐 알고리즘 (심층 7-3)

```text
Alg enqueue(e)
1. inStack.push(e)
2. return

Alg dequeue()
1. if (outStack.isEmpty())
       while (!inStack.isEmpty())
           outStack.push(inStack.pop())
2. if (outStack.isEmpty())
       emptyQueueException()
3. return outStack.pop()

```

두 큐 합동스택 알고리즘 (심층 7-4)

```text
Alg push(e)
1. Q1.enqueue(e)
2. return

Alg pop()
1. if (Q1.isEmpty())
       emptyStackException()
2. e <- Q1.dequeue()
3. while (!Q1.isEmpty())
       Q2.enqueue(e)
       e <- Q1.dequeue()
4. temp <- Q1
5. Q1 <- Q2
6. Q2 <- temp
7. return e

```

---

# 트리

트리의 크기 반환 (연습 8-1 일반트리 / 8-4 연결 이진트리 공통 로직)

```text
Alg size(v)
1. c <- 1
2. for each w in children(v)
       c <- c + size(w)
3. return c

```

_(8-1은 일반트리, 8-4는 연결 이진트리에 적용한다. 8-4의 경우 children(v) 대신 leftChild(v)·rightChild(v)를 순회해도 동일하다. 둘 다 선위순회를 특화한 형태로 O(n)이다.)_

배열 기반 이진트리의 크기 (연습 8-5)

```text
Alg size()
1. return rSize(root())

Alg rSize(i)
1. if (i >= N)
       return 0
2. if (T[i] = Null)
       return 0
3. return 1 + rSize(2i) + rSize(2i + 1)

```

_(크기 N인 배열 T로 구현된 이진트리다. 루트는 첨자 1, 노드 i의 두 자식은 2i·2i+1에 위치하며, 빈 자리는 Null로 표시된다. 첨자가 배열 범위(N)를 벗어나거나 Null이면 노드가 없는 것이므로 0을 반환한다. 실제 존재하는 노드만 한 번씩 방문하므로 O(n)이다. 만약 단순히 배열 전체를 훑어 `for i <- 1 to N - 1`에서 `T[i] != Null`인 칸을 세는 O(N) 방식도 가능하다.)_

디스크 사용량과 들여쓰기 (연습 8-2)

```text
Alg diskUsage(v, d)
1. sum <- 0
2. for each w in children(v)
       sum <- sum + diskUsage(w, d + 1)
3. sum <- sum + space(v)
4. for i <- 1 to d
       write(Tab)
5. write(element(v), sum)
6. return sum

```

내부, 외부 노드 수 계산 (연습 8-6)

```text
Alg countInternalNodes(v)
1. if (isExternal(v))
       return 0
2. c <- 1
3. for each w in children(v)
       c <- c + countInternalNodes(w)
4. return c

Alg countExternalNodes(v)
1. if (isExternal(v))
       return 1
2. c <- 0
3. for each w in children(v)
       c <- c + countExternalNodes(w)
4. return c

```

**수식트리 그리기 및 기타 해설 (연습 8-3, 8-7, 8-8, 8-9, 8-10)**

- **8-3 해설:** (A) 선위와 후위는 루트 방문 시점이 맨 처음·맨 마지막으로 상반되므로, 노드가 2개 이상이면 후위순회와 동일한 순서로 선위순회할 수 없습니다(단, 노드가 1개뿐인 트리는 선위=후위로 동일). (B) 후위순회의 역순과 선위순회가 같아지는 경우는 모든 내부노드가 자식을 하나만 갖는 사향(편향) 트리뿐이며, 일반적인 트리에서는 자식 순회 방향이 왼쪽→오른쪽으로 고정되어 있어 불가능합니다.

- **8-7 해설:** 4개의 숫자 1, 5, 6, 7과 연산자 3개를 활용해 21을 만들어야 합니다. 수식 `6 / (1 - (5 / 7))` 이 21이 되며, 이를 수식 트리로 그리면 루트가 `/`, 왼쪽 자식이 `6`, 오른쪽 자식이 `-`가 됩니다. 다시 `-`의 왼쪽은 `1`, 오른쪽은 `/`가 되며 가장 하단의 `/` 자식으로 `5`와 `7`이 배치됩니다.

- **8-8 해설 (순회 계승자):** 그림 이진트리(루트 A; A의 자식 B·C, B의 자식 D·E, C의 자식 F·G, E의 자식 H·I, 이 중 D·F·G·H·I는 외부노드)에서 각 순회 순서와 계승자는 다음과 같습니다.
  - 선위순회 = `A B D E H I C F G` → **노드 I의 선위순회 계승자 = C**
  - 중위순회 = `D B H E I A F C G` → **노드 A의 중위순회 계승자 = F**
  - 후위순회 = `D H I E B F G C A` → **노드 C의 후위순회 계승자 = A**

- **8-9 해설 (경로길이):** 그림 트리(루트 a)의 깊이는 a=0 / b·c=1 / d·e·f=2 / g·h·i·j·k=3 / l·m·n·o=4 / p=5 이며, 내부노드는 a·b·d·f·h·j·o, 외부노드는 c·e·g·i·k·l·m·n·p 입니다.
  - 경로길이(모든 노드 깊이의 합) = 0 + (1×2) + (2×3) + (3×5) + (4×4) + 5 = **44**
  - 내부경로길이(내부노드 깊이의 합) = 0+1+2+2+3+3+4 = **15**
  - 외부경로길이(외부노드 깊이의 합) = 1+2+3+3+3+4+4+4+5 = **29** (검산: 15 + 29 = 44 ✓)

- **8-10 해설:** 트리를 추적해보면 m과 k가 공통으로 속하는 가장 낮은 조상은 노드 b입니다. 두 노드 간의 거리는 m에서 b까지의 깊이 차이와 k에서 b까지의 깊이 차이의 합으로 구해집니다(경로 간선의 개수 합산).
  - A. 노드 m, k: LCA는 노드 b입니다. (m에서 b까지 거리 3 + k에서 b까지 거리 2 = 총 거리 5)
  - B. 노드 c, h: LCA는 노드 a입니다. (c에서 a까지 거리 1 + h에서 a까지 거리 3 = 총 거리 4)
  - C. 노드 p, b: LCA는 노드 b입니다. (p의 깊이 5, b의 깊이 1 → p에서 b까지 거리 4 + b에서 b까지 거리 0 = 총 거리 4)

경로길이 선형 알고리즘 (심층 8-2)

```text
Alg pathLength(v, d)
1. sum <- d
2. for each w in children(v)
       sum <- sum + pathLength(w, d + 1)
3. return sum

```

내부·외부 경로길이 (심층 8-3)

```text
Alg iPathLength(v, d)
1. if (isInternal(v))
       sum <- d
   else
       sum <- 0
2. for each w in children(v)
       sum <- sum + iPathLength(w, d + 1)
3. return sum

Alg ePathLength(v, d)
1. if (isExternal(v))
       sum <- d
   else
       sum <- 0
2. for each w in children(v)
       sum <- sum + ePathLength(w, d + 1)
3. return sum

```

_(pathLength·iPathLength·ePathLength 모두 깊이 d를 인자로 내려보내며 한 번의 순회로 O(n)에 계산한다. 내부경로길이는 내부노드에서만, 외부경로길이는 외부노드에서만 d를 더한다. 첫 호출은 d=0.)_

\*_일반 트리 최저공통조상과 거리 (심층 8-4_, 8-5\*)

```text
Alg lca(x, y)
1. while (depth(x) > depth(y))
       x <- parent(x)
2. while (depth(y) > depth(x))
       y <- parent(y)
3. while (x != y)
       x <- parent(x)
       y <- parent(y)
4. return x

Alg distance(x, y)
1. return depth(x) + depth(y) - 2 * depth(lca(x, y))

```

이진트리 복제 (심층 8-6)

```text
Alg copyBinaryTree(v)
1. u <- getnode()
2. u.elem <- element(v)
3. if (leftChild(v) != Ø)
       u.left <- copyBinaryTree(leftChild(v))
4. if (rightChild(v) != Ø)
       u.right <- copyBinaryTree(rightChild(v))
5. return u

```

상호재귀 순회 (심층 8-7)

- 문제 그림의 트리(루트 A, 자식 B·C / B의 자식 D·E / C의 자식 F·G / E의 자식 H·I, 단 D·F·G·H·I는 외부노드)에 대한 출력이다. 세 알고리즘은 표준 순회와 다른 **비전형적 순회**다.
  - **alphaOrder / betaOrder**: 두 함수가 서로를 호출하므로 노드의 출력 시점이 깊이의 홀짝에 따라 교대로 바뀐다(짝수 깊이=자식보다 먼저 출력, 홀수 깊이=자식들 사이에 출력). 따라서 표준 선위/중위 순회와 일반적으로 다르다.
    - `alphaOrder(v)` 출력 = **A D B E H I F C G** (선위순회 `A B D E H I C F G`와 다름)
  - **gammaOrder**: step 1과 step 3에서 자신을 두 번 출력하므로 각 노드가 정확히 두 번씩(총 2n개) 출력된다. 후위순회가 아니라, 노드에 진입할 때(선위 위치)와 이탈할 때(후위 위치) 각각 찍는 이중 방문이다.
    - `gammaOrder(v)` 출력 = **A B D D E H H I I E B C F F G G C A**

균형치 구하기 (심층 8-8)

```
Alg visitLeft(v)
1. return

Alg visitBelow(v)
1. return

Alg visitRight(v)
1. if (isExternal(v))
       v.h <- 0
   else
       v.h <- max(leftChild(v).h, rightChild(v).h) + 1
       v.bal <- abs(leftChild(v).h - rightChild(v).h)

```

수식인쇄 (심층 8-9)

```
Alg visitLeft(v)
1. if (isInternal(v))
       write('(')

Alg visitBelow(v)
1. write(element(v))

Alg visitRight(v)
1. if (isInternal(v))
       write(')')

```

수식평가 (심층 8-10)

```
Alg visitLeft(v)
1. return

Alg visitBelow(v)
1. return

Alg visitRight(v)
1. if (isExternal(v))
       v.val <- element(v)
   else
       x <- leftChild(v).val
       y <- rightChild(v).val
       op <- element(v)
       v.val <- doOperator(op, x, y)

```

유사 이진트리 확인 (심층 8-11)

```text
Alg areSimilar(a, b)
1. if (isExternal(a) & isExternal(b))
       return True
2. if (isInternal(a) & isInternal(b))
       return areSimilar(leftChild(a), leftChild(b)) & areSimilar(rightChild(a), rightChild(b))
3. return False

```

로만노드 세기 (심층 8-12)

```
Alg countRoman(v)
1. [count, size] <- rCountRoman(v)
2. return count

Alg rCountRoman(v)
1. if (isExternal(v))
       return [1, 1]
2. [lCount, lSize] <- rCountRoman(leftChild(v))
3. [rCount, rSize] <- rCountRoman(rightChild(v))
4. count <- lCount + rCount
5. if (abs(lSize - rSize) <= 5)
       count <- count + 1
6. return [count, lSize + rSize + 1]

```

황제노드 찾기 (심층 8-13)

```
Alg isEmperor(v)
1. [count, size, isEmp] <- rEmperor(v)
2. return isEmp

Alg rEmperor(v)
1. if (isExternal(v))
       return [1, 1, False]
2. [lCount, lSize, lEmp] <- rEmperor(leftChild(v))
3. [rCount, rSize, rEmp] <- rEmperor(rightChild(v))
4. count <- lCount + rCount
5. size <- lSize + rSize + 1
6. isRom <- (abs(lSize - rSize) <= 5)
7. if (isRom)
       count <- count + 1
8. isEmp <- False
9. if (!isRom & (lCount = lSize) & (rCount = rSize))
       isEmp <- True
10. return [count, size, isEmp]

```

비재귀 이진트리 선위/중위 순회 (심층 8-14)

```text
Alg binaryPreOrder(v)
1. S <- empty stack
2. S.push(v)
3. while (!S.isEmpty())
       u <- S.pop()
       write(element(u))
       if (isInternal(u))
           S.push(rightChild(u))
           S.push(leftChild(u))
4. return

Alg binaryInOrder(v)
1. S <- empty stack
2. p <- v
3. while (True)
       while (isInternal(p))
           S.push(p)
           p <- leftChild(p)
       write(element(p))
       if (S.isEmpty())
           break
       p <- S.pop()
       write(element(p))
       p <- rightChild(p)
4. return

```

이진트리 레벨 인쇄 (심층 8-15)

```text
Alg printLevel(v, d)
1. if (d = 0)
       if (isInternal(v))
           write(element(v))
   else
       if (isInternal(v))
           printLevel(leftChild(v), d - 1)
           printLevel(rightChild(v), d - 1)
2. return

```

---

# 분리집합

연습 9-1. 크기에 의한 합집합 및 경로압축

- **해설:** `union(a, c)`는 크기가 같으므로 알파벳 순 등 임의의 기준에 따라 a가 루트가 되고 c가 자식이 됩니다(크기 2). `union(h, i)` 역시 h가 루트가 되고 i가 자식이 됩니다(크기 2). `union(a, h)`를 수행하면 두 트리의 크기가 같으므로 a의 자식으로 h가 편입되어 전체 트리의 크기는 4가 됩니다. 이후 `find(m)`을 실행하면 m부터 루트 b까지의 경로(m->k->g->d->b)를 따라가며 탐색하고, 경로 압축에 의해 탐색을 마친 뒤에는 m, k, g, d가 모두 직접 루트인 b를 가리키게 구조가 평평해집니다.

비재귀 find 알고리즘 (연습 9-2)

```text
Alg find(e)
1. p <- e
2. while (Parent[p] != p)
       p <- Parent[p]
3. root <- p
4. p <- e
5. while (Parent[p] != root)
       next_p <- Parent[p]
       Parent[p] <- root
       p <- next_p
6. return root

```

분리집합 ADT 크기합집합과 경로압축 (심층 9-1)

```text
Alg find(e)
1. if (Parent[e] = e)
       return e
   else
       Parent[e] <- find(Parent[e])
       return Parent[e]

Alg union(x, y)
1. rootX <- find(x)
2. rootY <- find(y)
3. if (rootX != rootY)
       if (Size[rootX] < Size[rootY])
           Parent[rootX] <- rootY
           Size[rootY] <- Size[rootX] + Size[rootY]
       else
           Parent[rootY] <- rootX
           Size[rootX] <- Size[rootX] + Size[rootY]
4. return

```

경로이등분 find 알고리즘 (심층 9-2)

```text
Alg find(e)
1. while (Parent[e] != e)
       Parent[e] <- Parent[Parent[e]]
       e <- Parent[e]
2. return e

```
