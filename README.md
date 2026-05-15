# Thesis
~May 2026.

## Vibe Coding
Vibe coding results *seem* impressive on the surface. Anyone can wish something into existence in a few conversation turns. **No programming knowledge necessary.**

What is vibe coding exactly? (https://www.technologyreview.com/2025/04/16/1115135/what-is-vibe-coding-exactly/)

**MIT Technology review wrote:**

> The people most likely to benefit from vibe coding fall into two camps, says Tobin South, an AI security researcher at the MIT Media Lab. One is people like Karpathy, who already have a good grasp of coding and know how to fix any errors if anything goes seriously wrong if they’re using it to build anything important; the other is absolute amateurs with little to no coding experience. “I’d define vibe coding as having a vision that you can’t execute, but AI can,” he says.

**They continue:**

> Ultimately, while vibe coding can help make a vague idea for a website or a game into a reality, it can’t make it reliable or secure. But there are already plenty of existing tools to do this, helping you with everything from creating databases to adding authentication measures. So while you can’t vibe-code real, valuable, secure, robust apps into existence, it can be a useful place to start so long as you’re careful, says South.

***I completely reject the premise of vibe coding.***

However, I see serious potential in AI-assisted development.

There is a 3rd option missing from mainstream rhetoric.

> Can AI assist me with creating *"...real, valuable, secure, robust apps..."?*

## The Problem

MIT Technology review forgot something. ***Performance***

Modern software runs at roughly 1/1000th of what commodity silicon permits.

[Leiserson et al. (2020)](https://doi.org/10.1126/science.aam9744) called this *"plenty of room at the top."* Their paper has many fantastic ideas, proposals, and demonstrations on how modern software can be optimized.

One statement stood out to me:

> "Indeed, simple code tends to be slow, and fast code tends to be complicated. To create a world where it is easy to write fast code, application **programmers must be equipped with the knowledge and skills to performance-engineer their code**, and productivity tools to assist must be improved considerably."

Interesting. *"...Programmers must be equipped with the knowledge and skills to performance-engineer..."* and *"...productivity tools to assist must be improved considerably."*

New software development *typically* means using an established framework, copying an algorithm, or using a well known method, function, or command to accomplish a goal. A lot of today's software is built on the foundation of developer convenience, stack overflow patterns, and google searches.

Do career programmers build new apps from scratch in C? Rust? Assembly? Not usually.

There is rarely a business case for spending months developing a custom C kernel if you can accomplish the same goal in in one line of Python. Low-level work is already solved for most development. The industry moved to higher level languages decades ago.

Making *software faster* is not making *fast software*.

Fast software typically requires balancing expertise, complex codebases, potential security risks, and high development cost.

It's faster to ship high level code. It's even faster to vibe code.

**What if quality fast code could be shipped just as quickly as vibe code?**

## Matrix Multiplication

[Leiserson et al. (2020)](https://doi.org/10.1126/science.aam9744) demonstrated software performance gains in their paper:

> To illustrate the potential gains from performance engineering, consider the simple problem of multiplying two 4096-by-4096 matrices. Let us start with an implementation coded in Python, a popular high-level programming language. Here is the four-line kernel of the Python 2 code for matrix-multiplication:
> 
> for i in xrange(4096):
> 
>  for j in xrange(4096):
> 
>   for k in xrange(4096):
> 
>    C[i][j] += A[i][k] * B[k][j]
> 
> The code uses three nested loops and follows the method taught in basic linear-algebra classes. It turns out, however, that this naïve code leaves much of the performance available on modern computers “on the table.” The code takes about 7 hours on a modern computer to compute the matrix product, as shown by the first row (version 1) in [Table 1](https://www.science.org/doi/10.1126/science.aam9744#), achieving only 0.0006% of the peak performance of the machine. (Incidentally, Python 3 requires about 9 hours for the same computation.)

>| **Version** | **Implementation** | **Running time (s)** | **GFLOPS** | **Absolute speedup** | **Relative speedup** | **Fraction** <br>**of peak (%)** |
| --- | --- | --- | --- | --- | --- | --- |
| 1   | Python | 25,552.48 | 0.005 | 1   | —   | 0.00 |
| 2   | Java | 2,372.68 | 0.058 | 11  | 10.8 | 0.01 |
| 3   | C   | 542.67 | 0.253 | 47  | 4.4 | 0.03 |
| 4   | Parallel loops | 69.80 | 1.969 | 366 | 7.8 | 0.24 |
| 5   | Parallel divide and conquer | 3.80 | 36.180 | 6,727 | 18.4 | 4.33 |
| 6   | plus vectorization | 1.10 | 124.914 | 23,224 | 3.5 | 14.96 |
| 7   | plus AVX intrinsics | 0.41 | 337.812 | 62,806 | 2.7 | 40.45 |

> *Each version represents a successive refinement of the original Python code. “Running time” is the running time of the version. “GFLOPS” is the billions of 64-bit floating-point operations per second that the version executes. “Absolute speedup” is time relative to Python, and “relative speedup,” which we show with an additional digit of precision, is time relative to the preceding line. “Fraction of peak” is GFLOPS relative to the computer’s peak 835 GFLOPS. See Methods for more details.*

**Their best (v7, AVX-2 hand-tuned, 2017 hardware): 0.41s, 337.8 GFLOPS, 40.45% of single-FMA peak on an 18-core 2.9 GHz Haswell-EP.**

62,806x faster than Python, while using 40.45% of the hardware potential. Impressive.

I wonder if I can even come close.

## ***c*** (299,792,458 m/s)

The speed of light in vacuum. The universal speed limit. No entity in our universe can move faster.

Signal propagation operates below this speed. Any operation in a classical computer cannot physically happen faster.

Even quantum entanglement operates at or below ***c***. Countless other physical constraints limit classical computers well before we approach the speed of light. (Heat, power, quantum tunneling, the dimensions of atoms themselves.)

I can't improve hardware, but I can improve software.

How close can I get to the limits of hardware?
