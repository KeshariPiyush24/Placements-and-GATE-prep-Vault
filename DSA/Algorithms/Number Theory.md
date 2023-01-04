# A number can have at most one prime factor that is greater than its square root.

**Proof:**

Let n be any natural number.

- Suppose for a contradiction that n has two or more prime factors, p and q, such that p > sqrt(n) and q > sqrt(n).
- Then p and q are both in the prime factorization of n. This means that n is a multiple of pq.
- Therefore, n >= pq.
- Since p > sqrt(n) and q > sqrt(n), we can also write pq > sqrt(n) * sqrt(n).
- Therefore, n >= pq > n.
- This is a contradiction, because pq cannot be both greater than and less or equal to n at the same time.
- Therefore, our supposition that n has two or more prime factors greater than sqrt(n) must be false.
  
A good question to demonstrate this -> https://leetcode.com/problems/distinct-prime-factors-of-product-of-array/solutions/2977286/large-prime-optimization/

# four-by-four pattern of prime number

All the prime numbers except 2 will of the form `4n - 1` or `4n + 1` (n is a natural number).

Because all the prime numbers except 2 are odd and all the odd numbers can be represented in the form of `4n - 1` and `4n + 1`.


# All integers can be represented in the form of `2x + 3y`

Proof -> https://math.stackexchange.com/a/4611210/969447