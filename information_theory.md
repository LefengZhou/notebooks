# Information Theory

## Entropy

### Probability and random variables

mathematical denotations:
$$
p(x_0) = P(X=x_0) \longrightarrow X \sim p(x) \\
p(x_0,y_0) = P(X=x_0,Y=y_0) \longrightarrow X,Y \sim p(x,y) \\
p(x_0|y_0) = P(X=x_0|Y=y_0) \longrightarrow X|Y \sim p(x|y)
$$

### Entropy, joint entropy, and conditional entropy

entropy: **a measure of uncertainty** of a random variable. it is a function of probability distribution $p(x)$ instead of the actual value taken by $X$, although it is often denoted as $H(X)$.
$$
H(X) = E \log\frac{1}{p(X)} = -\sum_{x\in\mathscr{X}}p(x)\log p(x)
$$
joint entropy $H(X,Y)=E\log (1/p(X,Y))$, conditional entropy $H(X|Y) = E\log(1/p(X|Y))$

### Relative entropy and mutual information

relative entropy: a function of two probability distributions. It characterizes the distance, though the distance is not a mathematical distance.
$$
D(p||q) = \sum_x p(x) \log \frac{p(x)}{q(x)}
$$
mutual information: the distance of the correlated $p(x,y)$ and the uncorrelated $p(x)p(y)$. Mutual information characterizes how much information of one r.v. that another r.v. contains.
$$
I(X;Y) = D(p(x,y)||p(x)p(y))
$$
**Uncertainty is additive**: Venn diagram.

Any conditional versions of an information identity are true. e.g.,
$$
I(X,Y) = H(X)-H(X|Y) \Longrightarrow I(X,Y|Z) = H(X|Z)-H(X|Y,Z)
$$

### Jensen's inequality

definition of convexity: The chord is above the curve.

theorem:

1. $f(EX) \leq Ef(X)$.
   1. If $f$ is strictly convex, the equality holds at $X = EX$.
2. $D(p||q) \geq 0$.
   1. equality: $p(x)=q(x)$
   2. proof: $D(p||q) = -E\log(q(X)/p(X)) \geq -\log(E(q(X)/p(X))) = 0$
3. $I(X;Y)\geq 0$.
   1. equality: $X$ and $Y$ independent
4. $H(X)\leq \log|\mathscr{X}|$.
   1. equality: uniform distribution
   2. proof: $D(p||u) = \log|\mathscr{X}| - H(X) \geq 0$
5. $H(X|Y)\leq H(X)$.
   1. equality: $X$ and $Y$ independent
6. $H(X_1,X_2,\cdots,X_n) \leq \sum_{i=1}^n H(X_i)$.
   1. equality: $\{X_i\}$ independent

### Log sum inequality

log sum inequality: for $a_i,b_i\geq 0$,
$$
\sum_i a_i \log\frac{a_i}{b_i} \geq (\sum_ia_i) \log\frac{\sum_i a_i}{\sum_i b_i}
$$
proof: $f(x) = x \log x$ is convex. Construct a probability distribution $p(x_i) = b_i/\sum_i b_i$ for $X, x_i = a_i/b_i$. Then use the convexity property: $E(f(X)) \geq f(EX)$.

theorem:

1. $D(p||q) \geq 0$.
2. $ D(p||q) $ is convex in the pair $(p,q)$.
3. $H(p)$ is a concave function of $p$.
   1. proof: $D(p||u) = \log|\mathscr{X}| - H(X)$ is convex.
4. $I(X;Y)$ is a concave function of $p(x)$ for fixed $p(y|x)$.

### Data processing inequality

Data processing decreases the original information. Markov chain $X\rightarrow Y\rightarrow Z$,
$$
I(X;Y) \geq I(X;Z)
$$
sufficient statistics:

*TO BE SUPPLEMENTED*



### Fano's inequality

When $H(X|Y)$ is very small, we can predict $X$ from $Y$ precisely, because knowing $Y$ will help diminish the uncertainty of $X$. Naturally, the error probability is related to the remained uncertainty of $X$.

Suppose that we have an estimation method: $ \hat X = g(Y)$. The error probability is $p_e = P(\hat X \not= X)$. The correctness of the estimation is $I = I_{\{\hat X \not= X\}}$.
$$
H(X|Y) = H(I,X|Y) - H(I|X,Y) = H(I,X|Y) \\
= H(I|Y) + H(X|I,Y) \\
\leq H(I) + P(I = 1)H(X|I = 1,Y) + P(I = 0)H(X|I = 0,Y) \\
= H(p_e) + p_e H(X|I = 1,Y) \\
\leq H(p_e) + p_e \log(|\mathscr{X}| -1)
$$

So $p_e$ can be bounded away from 0,
$$
p_e \geq \frac{H(X|Y)-1}{\log(|\mathscr{X}| -1)}
$$

## Asymptotic equipartition property

### Weak law of large numbers

Khintchine's law: for i.i.d. r.v. $\{X_i\}$, $EX_i = EX < \infty$,
$$
\lim_{n\rightarrow +\infty} P(\left| \frac{1}{n}\sum_{i=1}^n X_i - EX \right|<\epsilon ) = 1,  \\
\frac{1}{n}\sum_{i=1}^n X_i \stackrel{P}{\longrightarrow} EX, n\rightarrow +\infty
$$

### AEP

key idea of AEP: There exists a set of long sequences $A_{\epsilon}^{(n)} \subset \mathscr{X}^n$, whose elements contribute most of the probabilities of occurrence. Its elements are almost equal probable, and the elements out of it are almost improbable.
$$
A_{\epsilon}^{(n)} = \{ (x_1,x_2,\cdots,x_n) \in \mathscr{X}^n \mid \left|-\frac{1}{n}\log p(x_1,x_2,\cdots,x_n) - H(X)\right| \leq \epsilon\}
$$
AEP theorem: i.i.d. r.v. $\{X_i\}$ are the samples of $X$, $X \sim p(x)$, then with weak law of large numbers we have
$$
-\frac{1}{n}\log p(X_1,X_2,\cdots,X_n) = -\frac{1}{n}\sum_{i=1}^n \log p(X_i) \\
\stackrel{P}{\longrightarrow} -E\log p(X) = H(X)
$$
explanation: $p(X_1,X_2,\cdots,X_n)$ is a statistic of $X$, representing the occurrence probability of the sequence $(X_1,X_2,\cdots,X_n)$. A similar example is $\frac{1}{n}\sum_{i=1}^n X_i$, which is a statistic representing the mean of the sequence. Note that $p(x)$ is a determinate function, no matter we know the specific form or not. AEP theorem tells us that **the probability of occurence of an observed sequence converges to something in probability**. Therefore, we define a typical set which includes all sequences that has a certain probability to appear. Naturally, it includes all observable sequences.

Following the definition of convergence in probability,
$$
\lim_{n\rightarrow +\infty} P(A_{\epsilon}^{(n)}) = 1
$$
So, for every small $\delta$, there exists a finite but sufficiently large $n$, such that $P(A_{\epsilon}^{(n)}) > 1-\delta$. We can choose $\delta = \epsilon$ for simplicity.

We can also estimate the number of elements in $A_{\epsilon}^{(n)}$ now that they have similar probability.
$$
1 \geq \sum_{x^n\in A_{\epsilon}^{(n)}} p(x^n) \geq 1-\epsilon \\

\Longrightarrow (1-\epsilon) 2^{n(H(X)-\epsilon)} \leq |A_{\epsilon}^{(n)}| \leq 2^{n(H(X)+\epsilon)}
$$

### Consequence of AEP: data compression

key idea of data compression: give shorter codes to the sequences with higher probability.

| set                                           | cardinality                 | length of codes (bits)                        |
| --------------------------------------------- | --------------------------- | --------------------------------------------- |
| $A_{\epsilon}^{(n)}$                          | $\leq 2^{n(H(X)+\epsilon)}$ | $n(H(X)+\epsilon) + 1 + 1$, with prefix 0     |
| $\mathscr{X}^n \backslash A_{\epsilon}^{(n)}$ | $\leq |\mathscr{X}|^n$      | $n \log |\mathscr{X}| + 1 + 1$, with prefix 1 |

Now we calculate the average length of the codes.
$$
E(l(X^n)) = \sum_{x^n\in \mathscr{X}^n} l(x^n)P(x^n) \\
= \sum_{x^n\in A_{\epsilon}^{(n)}} l(x^n)P(x^n) + \sum_{x^n\not\in A_{\epsilon}^{(n)}} l(x^n)P(x^n) \\
\leq (n(H+\epsilon) + 2)\sum_{x^n\in A_{\epsilon}^{(n)}}P(x^n) + (n \log |\mathscr{X}| + 2)\sum_{x^n\not\in A_{\epsilon}^{(n)}}P(x^n) \\
\leq (n(H+\epsilon) + 2) + (n \log |\mathscr{X}| + 2)\epsilon \\
= n(H + \epsilon\log |\mathscr{X}| + \epsilon) + 2+2\epsilon
$$
Therefore, there exists a one-to-one mapping that makes the average length of one sample converges to $H(X)$ for $n\rightarrow +\infty$.

### High probability set

Is the typical set small enough? Yes, it has essentially the same number of elements as the smallest set.

We define $B_{\delta}^n \subset \mathscr{X}^n, \lim_{n\rightarrow +\infty}P(B_{\delta}^n)  = 1$. Obviously $A_{\epsilon}^{(n)}$ satisfies the condition. We can find the minimum size of $B_{\delta}^n$, to prove that $A_{\epsilon}^{(n)}$ is nearly the smallest.

1. We consider $C = A_{\epsilon}^{(n)} \cap B_{\delta}^n$. Since $P(A_{\epsilon}^{(n)})$ and $P(B_{\delta}^n)$ are both nearly $1$, the two sets must largely overlap with each other. We can easily get $P(C)$ is nearly $1$.
2. The elements of $C$ have almost the same probability, because they are also elements of $A_{\epsilon}^{(n)}$.
3. Then we can estimate the minimum $|C|$, just as we estimate the minimum $|A_{\epsilon}^{(n)}|$.
4. Note that $C \subset B_{\delta}^n$. So we find the minimum $|B_{\delta}^n|$, which is similar to $|A_{\epsilon}^{(n)}|$.

## Data compression

### Concepts of codes

source code: $C: \mathscr{X}\rightarrow \mathscr{D}^*$

the extension of source code: $C^*: \mathscr{X}^* \rightarrow \mathscr{D}^*$ 

nonsingular code:  $C$ is injective.

uniquely decodable code: the extension $C^*$ is nonsingular (injective).

prefix code (instantaneous code): no codeword is a prefix of any other codeword.

### Kraft inequality

For any prefix codes over an alphabet of size $D$, if $l_i = l(x_i)$, then
$$
\sum_iD^{-l_i} \leq 1
$$
proof: Construct a D-ary tree. The codewords of a prefix code should be represented by the leaves of the tree. Assign every node a value $D^{-l}$, where $l$ is the depth of the node (the depth of the root is 0). Add all the leaf nodes that represent codewords to get a value less or equal to 1.

Conversely, given a set of codeword lengths that satisfy Kraft inequality, we can always construct such a tree, representing a prefix code.

Kraft inequality can be extended to a countable infinite set of codewords.
$$
\sum_i^{+\infty}D^{-l_i} \leq 1
$$

### Optimal codes

Find a prefix code that has the minimal expected length.

mathematical description: an optimization problem.
$$
\min_{C} E(l(X)) = \sum p_i l_i \\
\mathrm{s.t.} \sum_iD^{-l_i} \leq 1
$$
Use Lagrange multiplier method to find the optimal codeword lengths.
$$
l_i^* = -\log_D p_i \\
E(l(X)) = H_D(X)
$$
However, $l_i$ must be an integer. So strictly speaking, $l_i^* = \lceil -\log_D p_i \rceil$. Instead of finding an exact $E(l(X))$, we can find its bounds. Note that the upper bound of $l_i^*$ is guaranteed by the converse of Kraft inequality.
$$
-\log_D p_i \leq l_i^* = \lceil -\log_D p_i \rceil \leq -\log_D p_i+1 \\
H_D(X) \leq E(l(X)) \leq H_D(X)+1
$$
The fascinating part in information theory is the asymptotic property. The overhead of 1 bit can be spread out over many codewords.

Consider coding $n$ symbols together. We should find an optimal code $C_n: \mathscr{X}^n \rightarrow \mathscr{D}^*$. With the same optimization procedure, we have
$$
l^*(x_1,x_2,\cdots,x_n) = -log_D (p_1p_2\cdots p_n) = \sum_{i=1}^n \log_D p_i
$$
Still, $l^*(x_1x_2\cdots x_n)$ must be an integer.
$$
-log_D (p_1p_2\cdots p_n) \leq l^*(x_1,x_2,\cdots,x_n)  = \lceil -log_D (p_1p_2\cdots p_n) \rceil \leq -log_D (p_1p_2\cdots p_n) +1 \\
H_D(X^n) \leq E(l(X^n)) \leq H_D(X^n) +1 \\
H_D(X) \leq E(\frac{1}{n}l(X^n)) \leq H_D(X) +\frac{1}{n}
$$
The expected length of one codeword is asymptotically $H_D(X)$.

### Kraft inequality for uniquely decodable codes

Kraft inequality holds not only for prefix codes, but also for all uniquely decodable codes, as well as its converse. Therefore, though prefix codes are a subset of uniquely decodable codes, the optimal uniquely decodable code will not perform better than the optimal prefix code!

### Huffman codes

*TO BE SUPPLEMENTED*



## Channel capacity

mathematical model of discrete channel: $(\mathscr{X},p(y|x),\mathscr{Y})$, two finite sets and a probability transition matrix

$(M,n)$ code: (1) index set $\mathscr{M} = \{1,2,\dots,M\}$; (2) encoding function $x^n:\mathscr{M} \rightarrow \mathscr{X}^n$; (3) decoding function.

### Information channel capacity

Information channel capacity is the achievable maximum mutual information.
$$
C = \max_{p(x)} I(X;Y)
$$

### Symmetric channel

definition: All the rows of its probability transition matrix are the permutations of each other, as well as all the columns.

explanation: Exchanging two symbols results in the same channel.

channel capacity:
$$
I(X;Y) = H(Y) - H(Y|X) \\
= H(Y) - \sum_i p(x_i)H(Y|X = x_i) \\
= H(Y) - \sum_i p(x_i)H(r) \\
= H(Y) - H(r) \\
\Longrightarrow C = \max_{p(x)} I(X;Y) = \log |\mathscr{Y}| - H(r)
$$
where $r$ is a row of the probability transition matrix. $\forall x_i, H(Y|X = x_i) = H(r)$, because of symmetry of $\mathscr{X}$.

### Joint AEP

Construct the jointly typical set $A_{\epsilon}^{(n)}$:

1. It should be a subset of $B_{\epsilon}^{(n)}(X) \times C_{\epsilon}^{(n)}(Y)$, that is, the sequences $x^n$ and $y^n$ themselves should be typical.
2. jointly typical: the elements satisfy $\left|-\frac{1}{n}\log p(x^n,y^n) - H(X,Y)\right| \leq \epsilon$.

property:

1. $\lim_{n\rightarrow +\infty} P(A_{\epsilon}^{(n)}) = 1$
2. $|A_{\epsilon}^{(n)}| \leq 2^{n(H(X,Y)+\epsilon)}$
3. If $(\tilde X^n,\tilde Y^n)\sim p(x^n)p(y^n)$, where $p(x^n),p(y^n)$ are marginals of the distribution of $p(x^n,y^n)$, then $P((\tilde x^n,\tilde y^n)\in A_{\epsilon}^{(n)}) \approx 2^{-nI(X;Y)}$.
   1. proof: The marginal typical sequences $x^n, y^n$ distribute uniformly over their typical sets. Here we need to calculate the probability that a randomly chosen pair of the marginal typical sequences is jointly typical. So $P((\tilde x^n,\tilde y^n)\in A_{\epsilon}^{(n)}) = |A_{\epsilon}^{(n)}|/(|B_{\epsilon}^{(n)}(X)||C_{\epsilon}^{(n)}(Y)|)$.


### Channel coding theorem

#### Achievability

theorem: All rate $R$ below capacity $C$ is achievable.

proof:

For $(M,n)$ code, define rate $R = \frac{\log M}{n}$ bits per channel use. So, we deal with $(2^{nR},n)$ code.

A message $W$ is randomly chosen from the index set $\mathscr{M} = \{1,2,3,\dots,2^{nR}\}$. $W$ should be uniformly distribution, otherwise we can do data compression.

random code generation: Generate $x_i(w), 1\leq i\leq n, 1\leq w\leq 2^{nR}$. For all $w$ in the index set, the encoder produces a sequence $x^n(w) = x_1(w)x_2(w)\cdots x_n(w) \in \mathscr{X}^n$. The key point is that all $x_i(w)$ are randomly generated from a given probability distribution $p(x)$, and are i.i.d.

The code construction is symmetric, because all the codes are generated by the same operation. Without loss of generality, suppose that $W = 1$ is sent. The encoder produces $x^n(1)$, and the receiver gets a sequence $Y^n$ according to the transfer probability of the channel.
$$
Y_1 \sim p(y_1|x_1(1)) \\
Y^n \sim \prod_{i=1}^n p(y_i|x_i(1))
$$
typical set decoding: The receiver looks for $\hat w$ that satisfies $(x^n(\hat w),y^n)$ are jointly typical.

error analysis: Because of the randomness of code construction, we can only get the average error probability by calculating the expectation. There are two kinds of error. First kind is that the jointly typical sequence for received $y^n$ does not exist. But it is asymptotically impossible. When $n$ is very large, $x^n, y^n,(x^n,y^n)$ will all be typical because they are randomly drawn from $p(x,y)$. The second kind is that  $y^n$ is jointly typical with a code other than $x^n(1)$.
$$
P(E_2\cup E_3\cup \cdots \cup E_{2^{nR}}) \leq \sum_{i=2}^{2^{nR}}P(E_i)
$$
where $E_i = \{(x^n(i),y^n)\in A_{\epsilon}^{(n)} \}$. The advantage of random code generation is shown here: $x^n(i),i\not= 1$ is independant of the received $y^n$, because it is independent of $x^n(1)$. According to the property of joint AEP, $P(E_i) \approx 2^{-nI(X;Y)}, i\not= 1$. So, the error probability is less than approximately $2^{-n(I(X;Y)-R)}$. For all rate $R$ below $I(X;Y)$, the error probability is asymptotically 0.

Channel capacity is $C = \max_{p(x)} I(X;Y)$, so all rate $R$ below capacity $C$ is achievable. Note that the error prabability is an average because of random code generation. However, there exists at least one codebook below the average.

#### Converse part

converse part: Any rate $R$ above $C$ is not achievable.

proof:

We use Fano's inequality to bound the error probability from 0. The decoder uses $Y^n$ to guess $W$. Fano's inequality relates $p_e$, the error probability, and $H(W|Y^n)$, the remained uncertainty of $W$ when knowing $Y^n$.
$$
H(W|Y^n) \leq 1 + p_e nR \\
p_e \geq \frac{H(W|Y^n) - 1}{nR}
$$
Then, we prove that multiple uses of a DMC will not increase the capacity. Under the condition of $X^n$, all $Y_i$ are independent. $Y_i$ is also independent of $X_j, j\not= i$. 
$$
I(X^n;Y^n) = H(Y^n) - H(Y^n|X^n) \\
= H(Y^n) - \sum_{i=1}^n H(Y_i|X^n) \\
= H(Y^n) - \sum_{i=1}^n H(Y_i|X_i) \\
\leq \sum_{i=1}^n H(Y_i) - \sum_{i=1}^n H(Y_i|X_i) \\
= \sum_{i=1}^n I(Y_i;X_i) \\
\leq nC
$$
In fact, $W$ and $X^n$ are actually the same thing. Mathematically, we have Markov chain $W\rightarrow X^n\rightarrow Y^n\rightarrow \hat W$. So, $I(W;Y^n)\leq I(X^n;Y^n)\leq nC$. We find the largest amount of uncertainty in $W$ that $Y^n$ can reduce. 

Therefore, We can estimate the boundary of $p_e$ by calculating the $H(W|Y^n)$, the remained uncertainty of $W$.
$$
p_e \geq \frac{H(W|Y^n) - 1}{nR} \\
= \frac{H(W) - I(W;Y^n) - 1}{nR} \\
= \frac{nR - I(W;Y^n) - 1}{nR} \\
\geq \frac{nR - nC - 1}{nR} \\
= 1-\frac{C}{R}-\frac{1}{nR}
$$
When $R > C$, arbitrarily low error probility is not achievable.

### Feedback capacity

Feedback channel: The encoding function is $x_i(W,Y_{i-1}): \mathscr{M}\times \mathscr{Y} \rightarrow \mathscr{X}$.

Feedback does not improve the capacity.

proof:

We only need to consider the converse part of the channel coding theorem: Does $I(W;Y^n)\leq nC$ still hold? If yes, the channel coding theorem is also true for feedback channel.
$$
I(W;Y^n) = H(Y^n) - H(Y^n|W) \\
= H(Y^n) - \sum_{i=1}^n H(Y_i|Y_1,Y_2,\cdots,Y_{i-1},W)
$$
Because $X_i$ is a coding function of $(W,Y_{i-1})$, they are actually the same thing. $Y_i$ depends only on $X_i$,
$$
I(W;Y^n) = H(Y^n) - \sum_{i=1}^n H(Y_i|Y_1,Y_2,\cdots,Y_{i-2},X_i) \\
= H(Y^n) - \sum_{i=1}^n H(Y_i|X_i) \\
\leq \sum_{i=1}^nH(Y_i) - \sum_{i=1}^n H(Y_i|X_i) \\
= \sum_{i=1}^n I(Y_i;X_i) \\
\leq nC
$$

### Joint source channel coding theorem

theorem: If the source $V$ with satisfies AEP and $H(V) < C$, then there exists a source channel code with $p_e\rightarrow 0$. If the source has $H(V) > C$, arbitrarily low error probability is not achievable.

## Differential entropy

For continuous r.v. $X$ with probability density function $f(x)$, and support set $S$,
$$
h(X) = E \log\frac{1}{f(X)} = -\int_S f(x)\log f(x) dx
$$

### Examples of differential entropy

uniform distribution with $S = [0,a]$: $h(X) = \log a$

Gaussian distribution $X \sim N(0,\sigma^2)$: $h(X) = \frac{1}{2}\log (2\pi e\sigma^2)$

### AEP for continuous random variables

Construct the typical set $A_{\epsilon}^{(n)} = \{ x^n \in \mathscr{X}^n \mid \left|-\frac{1}{n}\log f(x^n) - h(X)\right| \leq \epsilon\}$

property:

1. $\lim_{n\rightarrow +\infty} P(A_{\epsilon}^{(n)}) = 1$, following the week law of large numbers.
2. $(1-\epsilon) 2^{n(h(X)-\epsilon)} \leq V(A_{\epsilon}^{(n)}) \leq 2^{n(h(X)+\epsilon)}$, where $V$ is the volume, the counterpart of cardinality.

### Relation to discrete entropy

Quantize the continuous r.v. $X$ to get discrete r.v. $X^{\Delta}$,
$$
P(X^{\Delta}= x_i) = \int_{i\Delta}^{(i+1)\Delta}f(x)dx = f(x_i)\Delta
$$
According to the mean value theorem, this quantization exists. Then calculate the entropy.
$$
H(X^{\Delta}) = -\sum_{i = -\infty}^{+\infty} f(x_i)\Delta\log(f(x_i)\Delta) \\
= -\sum_{i = -\infty}^{+\infty} f(x_i)\log(f(x_i)) \Delta - \log\Delta \\
\Longrightarrow H(X^{\Delta}) \longrightarrow h(X) - \log\Delta
$$
For n-bit quantization, $H(X^{\Delta}) \approx h(X) + n$. n-bit accuracy does not contain n-bit information.

### Joint and conditional differential entropy

Refer to the discrete case.

Joint Gaussian distribution: $X^n\sim N(0,K)$
$$
h(X^n) = \frac{1}{2}\log ((2\pi e)^n|K|)
$$

### Relative entropy and mutual information

$$
D(f(x)||g(x)) = \int f(x) \log \frac{f(x)}{g(x)} dx \\
I(X;Y) = D(f(x,y)||f(x)f(y)) = \int f(x,y)\log\frac{f(x,y)}{f(x)f(y)} dxdy
$$

Joint Gaussian: $I(X;Y) = h(X) + h(Y) - h(X,Y) = -\frac{1}{2}\log (1-\rho^2)$

Property:

1. $D(f||g) \geq 0$
2. $I(X;Y) \geq 0$ 
3. $h(X,Y) \leq h(X)$
4. chain rule $H(X_1,X_2,\cdots,X_n) = \sum_{i=1}^n h(X_i|X_1,X_2,\cdots,X_{i-1})$
5. $h(X+c) = h(X)$. Transition does not change the distribution.
6. $h(cX) = h(X) + \log |c|$. But scaling does.
7. $h(X^n) \leq \frac{1}{2}\log ((2\pi e)^n|K|)$. The joint Gaussian distribution maximizes the entropy over all distribution with the same covariance matrix.

## Gaussian channel

### Definition of Gaussian channel

$$
Y = X + Z, Z\sim \mathscr{N}(0,N)
$$

constraint: power constraint

information capacity of Gaussian channel:
$$
C = \max_{p(x):EX^2\leq P} I(X;Y) = \frac{1}{2}\log (1+\frac{P}{N}), X\sim \mathscr{N}(0,P)
$$
But we must consider discrete code.

### Sphere packing?

If a vector $x^n$ in $n$-dimension space is sent, the received vector is $Y^n = x^n + Z^n$ . We should consider the distribution of $Y^n$. It will distribute around $x^n$, with squared distance $\sum_{i=1}^n Z_i^2$. According to the law of large numbers,
$$
\frac{1}{n}\sum_{i=1}^n Z_i^2 \longrightarrow N
$$
So $Y^n$ will mostly distribute in a spherecal shell of radius $\sqrt{n(N-\epsilon)} < r < \sqrt{n(N+\epsilon)}$. So I cannot understand why the spheres of different $x^n$ cannot overlap.

### Gaussian channel coding theorem

Any codes with power constraint $P$ for Gaussian channel with noise power $N$ can achieve at most $C = \frac{1}{2}\log (1+P/N)$ bits per transmission with arbitrarily low error probability.

We only prove achievability. The procedure is similar to the channel coding theorem.

1. For $(2^{nR},n)$ code, the message is uniformly distributed over $\mathscr{M} = \{1,2,\cdots, 2^{nR}\}$.
2. random code generation
3. transmission
4. typical set decoding
5. error analysis

### Bandlimited channel

Consider a baseband signal with bandwidth $W$. According to Nyquist sampling theorem, the continuous-time signal can be represented by a discrete-time signal with sampling frequency $f_s = 2W$ without any loss of information. Higher sampling frequency will make the samples correlated. So, this bandlimited signal has only $2W$ degrees of freedom per second.

Assume that signal power is $P$ and noise power spectral density is $N_0/2$. So the noise power is $N_0 W$. If we sample the bandlimited noise with $f_s = 2W$, we will get an AWGN sequence whose samples are independent, just like sampling the signal. The energy per signal sample is $P/f_s$, and the energy per noise sample is $N_0W/f_s$. So the channel capacity is
$$
C = \frac{1}{2}\log (1+\frac{P}{N_0 W}) \quad\mathrm{bits/transmission} \\
C = W\log (1+\frac{P}{N_0 W}) \quad\mathrm{bits/second}
$$

### Parallel Gaussian channels

Under the constraint of total power, how to allocate power to parallel Gaussian channels with given noise in order to maximize the total channel capacity?

water filling method: allocate more power to the channels with lower noise

## Rate distortion theory

### Quantization

To quantize a continuous source $X$. Define distortion $d = E(X-\hat X(X))^2$. An optimal quantizer minimizes the distortion. 

Lloyd-Max quantization: The reconstruction value is at the centroid of the quantization interval, and the boundary is the mean of its neighboring reconstruction values.

### Rate distortion function

The general definition of distortion: how the symbol first encoded then decoded matches with the one source produced. Mostly, $\mathscr{X} = \hat{\mathscr{X}}$.
$$
d(x,\hat x): \mathscr{X} \times \hat{\mathscr{X}} \rightarrow \R^+
$$
information rate distortion function $R(D)$: the minimum mutual information under a certain limited distortion $D$.
$$
R(D) = \min_{p(\hat x |x):Ed(X,\hat X)<D} I(X;\hat X)
$$
$Ed(X,\hat X) = \sum_{x,\hat x} p(x)p(\hat x |x)d(x,\hat x)$ is the constraint on the distortion. $p(x)$ is determined by the source, and $p(\hat x |x)$ is to be optimized, $d(x,\hat x)$ is the measurement of distortion defined already.

theorem: A distortion as low as $D$ can be achieved by a rate higher than $R(D)$, but cannot be achieved by any lower rate. Proof is omitted.

A special case is the source coding theorem. Zero distortion can be achieved by a rate higher than $R(0) = H(X)$.

### Examples

Binary source

Gaussian source

### Multiple Gaussian sources

Under the constraint of total distortion, how to allocate allowed distortion to multiple Gaussian sources with given variance in order to minimize the total rate?

reverse water filling: allocate more allowed distortion to the sources with higher variance

