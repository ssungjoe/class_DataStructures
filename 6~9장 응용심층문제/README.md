# 스택

연습 6-1. 후위수식 변환

- **해설:** 스택을 활용한 알고리즘을 모의실행하면 연산자 우선순위에 따라 괄호 안이 먼저 처리되고, 곱셈/나눗셈이 덧셈/뺄셈보다 먼저 처리되어 결과적으로 `4 3 * 17 3 + 5 / 6 15 3 / - 1 + * -` 와 같은 후위 수식이 산출됩니다.

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

```

_(inject와 eject도 이와 유사한 포인터 조작을 통해 양 끝단에서 처리합니다)_

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

트리의 크기 반환 (연습 8-1, 8-4, 8-5 공통 로직)

```text
Alg size(v)
1. c <- 1
2. for each w in children(v)
       c <- c + size(w)
3. return c

```

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

**수식트리 그리기 및 기타 해설 (연습 8-3, 8-7, 8-10)**

- **8-3 해설:** 순서트리 탐색에 있어 선위와 후위는 루트 방문 시점이 맨 처음과 맨 마지막으로 완전히 상반되므로 동일한 순서가 될 수 없습니다. 역순 탐색 역시 한쪽으로 치우친 특수 사향 트리를 제외하고는 일반적인 트리의 자식 노드 순회 방향(왼쪽에서 오른쪽)이 고정되어 있다면 불가능합니다.

- **8-7 해설:** 4개의 숫자 1, 5, 6, 7과 연산자 3개를 활용해 21을 만들어야 합니다. 수식 `6 / (1 - (5 / 7))` 이 21이 되며, 이를 수식 트리로 그리면 루트가 `/`, 왼쪽 자식이 `6`, 오른쪽 자식이 `-`가 됩니다. 다시 `-`의 왼쪽은 `1`, 오른쪽은 `/`가 되며 가장 하단의 `/` 자식으로 `5`와 `7`이 배치됩니다.

- **8-8 해설** 노드의 깊이/높이/균형치
  - 깊이(Depth): 해당 노드에서 루트까지 올라가며 거치는 간선의 수입니다. 루트의 깊이는 0입니다.
  - 높이(Height): 해당 노드에서 가장 깊은 단말 노드(Leaf)까지 내려가는 가장 긴 간선의 수입니다. 단말 노드의 높이는 0입니다.
  - 균형치(Balance Factor): 해당 노드의 (왼쪽 자식 트리의 높이) - (오른쪽 자식 트리의 높이)의 절댓값입니다. 빈 트리의 높이는 통상 0로 계산합니다.

- **8-9 해설** '유사한 이진트리(Similar Binary Trees)'란 노드에 들어있는 데이터(element)와 상관없이 트리의 뼈대(구조, shape)가 완전히 동일한 트리를 의미합니다. 따라서 구조가 동일한 두 트리 T와 T'를 동일한 순회 방식(예: 선위순회)으로 순회하면, 방문하게 되는 노드의 위치적 순서는 완벽하게 일치합니다. (물론 출력되는 데이터 값은 다를 수 있습니다.)

- **8-10 해설:** 트리를 추적해보면 m과 k가 공통으로 속하는 가장 낮은 조상은 노드 b입니다. 두 노드 간의 거리는 m에서 b까지의 깊이 차이와 k에서 b까지의 깊이 차이의 합으로 구해집니다(경로 간선의 개수 합산).
  - A. 노드 m, k: LCA는 노드 b입니다. (m에서 b까지 거리 3 + k에서 b까지 거리 2 = 총 거리 5)
  - B. 노드 c, h: LCA는 노드 a입니다. (c에서 a까지 거리 1 + h에서 a까지 거리 3 = 총 거리 4)
  - C. 노드 p, b: LCA는 노드 b입니다. (p에서 b까지 거리 3 + b에서 b까지 거리 0 = 총 거리 3)

경로길이 선형 알고리즘 (심층 8-2, 8-3)

```text
Alg pathLength(v, d)
1. sum <- d
2. for each w in children(v)
       sum <- sum + pathLength(w, d + 1)
3. return sum

```

_(내부/외부 경로길이도 동일하게 순회하며 `isInternal`, `isExternal` 조건일 때만 d값을 더합니다)_

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

- 3개의 상호재귀 함수는 각각 노드를 언제 visit() 하느냐(맨 처음, 중간, 맨 끝)에 따라 기본 순회와 동일한 결과를 냅니다.
  - alphaOrder(v): 호출 즉시 자신을 방문하고 자식을 탐색하므로 선위 순회(Pre-order)와 완전히 동일합니다.
  - betaOrder(v): 왼쪽 자식들을 끝까지 파고든 뒤 자신을 방문하므로 중위 순회(In-order)와 동일합니다.
  - gammaOrder(v): 자식들을 모두 탐색한 후 마지막에 자신을 방문하므로 후위 순회(Post-order)와 동일합니다.

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
