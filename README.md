## Computing Shintani fundamental domains

Here we give an algorithm (in Pari/GP) to obtain a TRUE fundamental domain from a SIGNED fundamental domain for the action of the totally positive units group of a NON-TOTALLY COMPLEX NUMBER FIELD. We also present some examples of Shintani domains in the folder `Examples`. This implementation is based in the manuscript:

A.Capuñay, "COMPUTING SHINTANI DOMAINS" -- International Journal of Number Theory (2024)


----------------------------------------------------------------------------------------------------------------
The SIGNED domains were established in the works of Diaz y Diaz, Espinoza and Friedman:

[DDF14] F. Diaz y Diaz and E. Friedman, "Signed fundamental domain for totally real number fields" (2014)  
[MR4105945](https://arxiv.org/abs/1303.3989)

[EF20] M. Espinoza and E. Friedman, "Twisters and Signed fundamental domains of number fields" (2020)  
[MR3198753](https://arxiv.org/abs/1903.07089)

Our implementation is also based in the description of rational cones by inequalities (or H-representation) and    
generators (or V-representation). For this we use the Fukuda-Prodon's paper:  

[FP96] Fukuda and Prodon, "Double description method revisited" (1996)  
[MR1448924](https://link.springer.com/chapter/10.1007/3-540-61576-8_77) 
 


## FILE DESCRIPTION:


1. In the file `SignedDomain.gp` we implement the signed domains given in [DDF14] (for totally real fields) and [EF20] (for non-totally complex fields). Which can be read in Pari/GP using the command

     `\r SignedDomain.gp`

2. Using `SignedDomain.gp`, we give in the file `ShintaniDomain.gp` our main algorithm to find a true fundamental domain from a signed one. This can be read using 

     `\r ShintaniDomain.gp`

So given as input an irreducible polynomial `p` (which defines a non-totally complex number field), the command in Pari/GP

 `F=fudom(p);`

return a Shintani fundamental domain with the following structure:

 $$F:=[F_1,F_2,F_3];$$
     
The first entry $F_1$ (i.e., $F[1]$) has the form

 $$[t, p, reg, disc, [r_1, r_2], U, T]$$

with 

$t =$   real computation time for $F$ in milliseconds (this depends on the number of negative cones in a signed domain and 
       also on the type of processor used)
       
$p =$  irreducible polynomial defining a non-totally complex number field $k := \text{the quotient ring }\mathbb{Q}[X]/(p)$ of degree $n$
       
$reg =$ Regulator of $k$ to $19$ decimals

$disc =$ Discriminant of $k$

$[r_1, r_2]=[\text{Number of real places}, \text{Number of complex places}]$ signature of $k$, so $n=r_1+2r_2$

$U =$   fundamental units of $k$. The Shintani domain corresponds to the action on $(\mathbb{R}_{+})^{r_1}\times(\mathbb{C}^{\ast})^{r_2}$ of the group generated by $U$ (for $r_1>0$ and rank of units $r=r_1+r_2-1>0$). The units in $U$, like all other elements of $k$, is given as a polynomial $g$ in $\mathbb{Q}[X]$ of degree at most $n$. The associated element of $k$ is the class of $g$ in $\mathbb{Q}[X]/(p)$
       
$T =$ number of semi-closed n-dimensional cones in the Shintani domain constructed. 


The second entry $F_2$ (i.e., $F[2]$) has the form

$$[C_1,C_2,...,C_T]$$

which is a list of the $T$ (semi-closed n-dimensional) cones in the Shintani domain. Here $T=F[1][7]$ is the last entry of $F_1$  described above. Each cone $C_j$ is given by $m$ linear inequalities ($m$ depending on the cone) giving $m$ closed or open half-spaces whose intersection is $C_j$. Thus, each $C_j$ has the form  

$$[v_1,v_2,...,v_m]$$

where $v_i=[w,1]$ or $[w,-1]$ and $w$ is an element of $k$ (depending on  $i$ and $j$). If $w$ is followed by $1$, then the corresponding (closed) half-space is the set of elements $x$ of $\mathbb{R}^n$ with $\text{Trace}(xw)\geq 0$. If $w$ is followed by $-1$, then the corresponding (open) half-space is given by $\text{Trace}(xw)>0$. Here Trace is the extension to $\mathbb{R}^n$ of the trace map from $k$ to $\mathbb{Q}$.

   The third entry `F3` of F (i.e., F[3]) has the form  

              [CC1,CC2,...,CCT]

where CCj is the closure in R^n of the cone Cj in `F2`. Each closed cone CCj is given here by a list of generators in k.



3. In the folder `Examples` we show several examples of explicit Shintani domains obtained using the `fudom(p)` command described in item 2. Here there exists 9 subfolders (called `ShintaniKnr`)

   `ShintaniK65`; `ShintaniK54`; `ShintaniK53`; `ShintaniK52`; `ShintaniK43`; `ShintaniK42`; `ShintaniK32`; `ShintaniK31`; `ShintaniK21`
   
Where each folder `ShintaniKnr` contains the fundamental domains for number fields of degree `n` (for n=2,3,4,5,6) with rank of units `r=r1+r2-1` (for 1<= r <=5 such that r1>0)

Each folder `ShintaniKnr` contains three files:  `fieldsKnr.gp` -- `ShintaniKnr.txt` -- `ShintaniKnr-ML.sage`

Where:
    
* The file `fieldsKnr.gp` contains a data of fields used to obtains Shintani domains which was download from https://www.lmfdb.org/

* The file `ShintaniKnr.txt` contains a data of explicit Shitani domains which can be read by Pari/GP using the command 

   `\r ShintaniKnr.txt`
   
  This returns a vector called `examples=[E1,E2,...,Eg]`, where each Ei=fudom(p) is a vector of size three which was described in item 2  with `p` an irreducible polynomial of degree `n` which defines a non-totally complex number field k. 

* The file `ShintaniKnr-ML.sage` can be read by SageMath using the command 

  `load('ShintaniKnr-ML.sage')`

this returns the same list of examples as the file `ShintaniKnr.txt` with the same structure.

   
## SOME REMARKS: 

(1) After uploading files `SignedDomain.gp` and `ShintaniDomain.gp`, the command in Pari/GP:  `ShintExamples(L)` returns a file with a list of examples of the calculated Shintani domains, where L=vector of irreducible polynomials of degree n (using r1>0 and rank r=r1+r2-1>0).

(2) The fundamental domains in the folder `ShintanK21` correspond to totally real quadratic fields which are widely known by number theorists. See for example Borevich-Shafarevich's Book "Number theory" (Chapter 5, Section 1.2).

(3) And the folder `ShintaniK32` which correspond to Shintani domains for totally real cubic fields are also known, see for example Diaz y Diaz and Friedman's work: [Real Cubic Shintani](https://www.sciencedirect.com/science/article/pii/S0022314X12000844)

(4) On the other hand, the folder `ShintaniK31` contains Shintani domains for complex cubic number fields, this is consistent with a recently published work: [Complex Cubic Shintani](https://www.worldscientific.com/doi/abs/10.1142/S1793042123300016)

(5) The remaining files: `ShintaniK42` - `ShintaniK43` - `ShintaniK52` - `ShintaniK53` - `ShintaniK54` - `ShintaniK65` contains Shintani domains (for a list of polynomials given) of non-totally complex `quartic`, `quintic` and `sextic` fields, which until now has not been considered of systemically.

(6) The main bottleneck is that the number of cones on a Signed Domain grows (this is `3^(r2)*(n-1)!` cones) when `n` grows. This number of cones is the input in our main algorithm to obtain a Shintani domain, so our implementation works well when `n<=5` and sometimes in sextic fields `n=6` when the negative cones in a Signed domains is small. However, it is possible trying to compute Shintani domains of number fields for `degree>6` if you are using a good processor. 

