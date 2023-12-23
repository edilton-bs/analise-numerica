# Resumo final - Análise numérica

## Métodos numéricos para sistemas de alta dimensão

O objetivo é resolver sistemas $Ax=b$ onde $A$ é uma matriz de dimensão $n\times n$ e $b$ é um vetor de dimensão $n$.

A ideia é a seguinte:

$Ax=b \Rightarrow x = Cx + d$

$x^{0}, x^{1}, x^{2}, \dots, x^{k}, \dots$

$x^{k+1} = Cx^{k} + d$

**Teorema:** Seja $x^*$ a solução de $x = Cx + d$. Considere a sequência definida por $x^{k+1} = Cx^{k} + d$. Então:

1. A sequência $\{x^k\}_{k=0}^{\infty}$ converge para $x^*$ se, e somente se, $\rho(C) < 1$.
  
2. $\exists ||.|| \text{ tal que } || x^{*} - x^{k} || \leq \frac{||C||}{1 - ||C||}||x^{k} - x^{k-1}||$

### Método de Jacobi

Se eu tenho $Ax = b \Rightarrow x = Cx + d$, então, qual $C$ escolho tal que $\rho(C) < 1$?

Jacobi disse que:

$(D+M)x = b \Rightarrow Dx = -Mx + b \Rightarrow x = -D^{-1}Mx + D^{-1}b = C_Jx + d$

**Quando Jacobi converge?**

**Definição:** Uma matriz $A$ é estritamente diagonal dominante

a) por linhas se $|a_{ii}| > \sum_{j=1, j\neq i}^{n} |a_{ij}|, \forall i = 1, \dots, n$.

b) por colunas se $|a_{ii}| > \sum_{j=1, j\neq i}^{n} |a_{ji}|, \forall i = 1, \dots, n$.

**Teorema:** Se $A$ é estritamente diagonal dominante por linhas/colunas, então o método de Jacobi converge.

### Método de Gauss-Seidel

Jacobi faz:

$\begin{cases}x_1^{k+1} = \frac{-a_{12}}{a_{11}}x_2^k + \dots + \frac{-a_{1n}}{a_{11}}x_n^k + \frac{b_1}{a_{11}} \\x_2^{k+1} = \frac{-a_{21}}{a_{22}}x_1^k + \dots + \frac{-a_{2n}}{a_{22}}x_n^k + \frac{b_2}{a_{22}} \\\vdots \\x_n^{k+1} = \frac{-a_{n1}}{a_{nn}}x_1^k + \dots + \frac{-a_{n,n-1}}{a_{nn}}x_{n-1}^k + \frac{b_n}{a_{nn}}\end{cases}$

Seide faz:

$\begin{cases}x_1^{k+1} = \frac{-a_{12}}{a_{11}}x_2^{k+1} + \dots + \frac{-a_{1n}}{a_{11}}x_n^{k+1} + \frac{b_1}{a_{11}} \\x_2^{k+1} = \frac{-a_{21}}{a_{22}}x_1^{k+1} + \dots + \frac{-a_{2n}}{a_{22}}x_n^{k+1} + \frac{b_2}{a_{22}} \\\vdots \\x_n^{k+1} = \frac{-a_{n1}}{a_{nn}}x_1^{k+1} + \dots + \frac{-a_{n,n-1}}{a_{nn}}x_{n-1}^{k+1} + \frac{b_n}{a_{nn}}\end{cases}$

Seidel escrito de forma matricial:

$Ax = b \Rightarrow (L+D+U)x = b \Rightarrow (L+D)x = -Ux + b \\ \Rightarrow x = -(L+D)^{-1}Ux + (L+D)^{-1}b = C_Sx + d$

### Critério de Sassenfeld

Seja $Ax = b (A \in \mathbb{R}^{n \times n})$ um sistema linear.

$p_1 = \frac{|a_{12}| + |a_{13}| + \dots + |a_{1n}|}{|a_{11}|}$

$p_2 = \frac{|a_{21}|p_1 + |a_{23}| + \dots + |a_{2n}|}{|a_{22}|}$

$\vdots$

$p_n = \frac{|a_{n1}| + |a_{n2}| + \dots + |a_{n,n-1}|p_{n-1}}{|a_{nn}|}$

$ p_i = \frac{\sum_{j=1}^{i-1} |a_{ij}| p_j + \sum_{j=i+1}^{n} |a_{ij}|}{|a_{ii}|}, \quad i = 2, 3, ..., n $

Se $p = \max p_i < 1$, então o método de Gauss-Seidel converge e $||x^* - x^k|| \leq \frac{p}{1-p}||x^k - x^{k-1}||_{\infty}$.

### Método SOR

$Ax = b$

Para Seidel:

$(L+D+U)x = b$

$(wL + wD + wU)x = wb$

$(wL + D)x = ((1-w)D-wU)x+wb$

$x = -(wL + D)^{-1}((1-w)D-wU)x+(wL + D)^{-1}wb$

$x^{k+1} = C_{SOR}x^k + d$

A ideia é que $w$ escolher para melhorar a velocidade do método de Seidel.


**Teorema:** A condição necessária para a convergência do método SOR é que $w \in (0,2)$.

**Teorema (Ostrowski):** Se $A$ é simétrica e positiva definida, então o método SOR converge para qualquer $w \in (0,2)$.

---

### Questões resolvidas com métodos iterativos

**QUESTÃO1b-LISTA2**

*Solução:*

Resolve usando o critério de Sassenfeld:

$p_i = \frac{\sum_{j=1}^{i-1} |a_{ij}| p_j + \sum_{j=i+1}^{n} |a_{ij}|}{|a_{ii}|}, \quad i = 2, 3, ..., n$

$p = \max p_i < 1$

Critério de parada: $\frac{p}{1-p}||x^k - x^{k-1}||_{\infty} < \epsilon$ (onde $\epsilon$ é a precisão desejada, e.g. $10^{-5}$)

**QUESTÃO4b-LISTA2**

*Solução:*

$\begin{pmatrix}
2 & 1 & -\frac{1}{2} \\
1 & 2 & 0 \\
\frac{1}{2} & 0 & 1 \\
\end{pmatrix}
\begin{pmatrix}
x_1 \\
x_2 \\
x_3 \\
\end{pmatrix}$
\=
$\begin{pmatrix}
1 \\
1 \\
1 \\
\end{pmatrix}$

Sistema Gauss-Seidel:

$\begin{cases}
x_1^{k+1} = \frac{-x_2^k}{2} + \frac{x_3^k}{4} + \frac{1}{2} \\
x_2^{k+1} = \frac{-x_1^{k+1}}{2}  + \frac{1}{2} \\
x_3^{k+1} = \frac{-x_1^{k+1}}{2} + 1 \\
\end{cases}$

Dado que $x^{0} = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$, vamos calcular $x^{1}$:

$\begin{cases}
x_1^{1} = \frac{-1}{2} + \frac{1}{4} + \frac{1}{2} = \frac{1}{4} \\
x_2^{1} = \frac{-1}{8} + \frac{1}{2} = \frac{3}{8} \\
x_3^{1} = \frac{-1}{8} + 1 = \frac{7}{8} \\
\end{cases}$

Logo $x^{1} = \begin{pmatrix} \frac{1}{4} \\ \frac{3}{8} \\ \frac{7}{8} \end{pmatrix}$

Agora, calculando o erro $|x-x^{1}|_{\infty}$

$|x-x^{1}|_{\infty} = \frac{p}{1-p}||x^0 - x^{1}||$

Sassenfeld:

$p_1 = \frac{|1| + |\frac{1}{2}|}{|2|} = \frac{3}{4}$

$p_2 = \frac{3}{8}$

$p_3 = \frac{3}{8}$

$p = \max(p1, p2, p3) = 3/4$

Calculando a norma:

$||x^0 - x^{1}|| = \max(|1 - \frac{1}{4}|, |1 - \frac{3}{8}|, |1 - \frac{7}{8}|) = \frac{3}{4}$

Logo:

$|x-x^{1}|_{\infty} = \frac{p}{1-p}||x^0 - x^{1}|| = \frac{\frac{3}{4}}{1-\frac{3}{4}}\frac{3}{4} = 1.25$

**QUESTÃO7-LISTA2**

Temos que pelo teorema de Ostrowski, o método SOR converge para qualquer $w \in (0,2)$ se $A$ é simétrica e positiva definida. Mas Seidel é SOR com $w=1$, então Seidel também converge.



## Interpolação polinomial

Supondo que temos $(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)$ no plano cartesiano.

Queremos encontrar um polinômio $p(x)$ tal que $p(x_i) = y_i$, $i = 1, 2, \dots, n$.

Lagrange:

$P(x_i) = y_i$, $i = 1, 2, \dots, n$

Polinômio interpolador de Lagrange:

$P(x) = \sum_{i=1}^n ( \prod_{j=1, j \neq i}^n \frac{x-x_j}{x_i-x_j} y_i )$

Exemplo:

$p(x) = \frac{(x-x_4)(x-x_2)(x-x_3)}{(x_1-x_2) (x_1-x_3) (x_1-x_4)} y_1 + \frac{(x-x_1)(x-x_3)(x-x_4)}{(x_2-x_1) (x_2-x_3) (x_2-x_4)} y_2 + \frac{(x-x_1)(x-x_2)(x-x_4)}{(x_3-x_1) (x_3-x_2) (x_3-x_4)} y_3 + \frac{(x-x_1)(x-x_2)(x-x_3)}{(x_4-x_1) (x_4-x_2) (x_4-x_3)} y_4$

**Como estimar o erro?**

**Teorema (Erro de interpolação):** Seja $f(x)$ uma função diferenciável em $[a, b]$ e $P(x)$ o polinômio interpolador de Lagrange de $f(x)$ nos pontos $x_1, x_2, \dots, x_n$ em $[a, b]$. Então, se $f \in C^{n}([a, b])$, então $\forall x \in [a, b]$, $\exists \xi_x \in [\min_{x_i}, \max_{x_i}]$ tal que:

$|f(x) - P(x)| = \frac{f^{(n)}(\xi_x)}{n!} \prod_{i=1}^n (x-x_i)$

*Exemplo:* Função seno intervalo $[0, \pi /2]$. Qual a máxima distância entre a função e o polinômio interpolador de Lagrange de grau 1 ?

$p(x) = \frac{(x-x_2) \sin(x_2)}{x_1 - x_2} + \frac{(x-x_1) \sin(x_1)}{x_2 - x_1} = \frac{2 x}{\pi}$

$|\sin(x) - p(x)| = |\sin(x) - \frac{2 x}{\pi}| = | \frac{sin''(\xi_x)}{2!} x (x - \frac{\pi}{2}) | \leq \frac{\pi^2}{32}$

**Pensar em quais pontos escolher do intervalo $[a, b]$ para minimizar o erro.**

$\max_{x \in [a,b]}|f(x) - P(x)| = \max_{x \in [a,b]}|\frac{f^{(n)}(\xi_x)}{n!} \prod_{i=1}^n (x-x_i)| = \max_{x \in [a,b]}|\frac{f^{(n)}(\xi_x)}{n!}| \max_{x \in [a,b]}|\prod_{i=1}^n (x-x_i)|$

Quais valores $(x_i, y_i)$ escolher tal que $\max_{x \in [a,b]}|\prod_{i=1}^n (x-x_i)|$ seja mínimo? Por que queremos que seja mínimo? Porque assim o erro será menor. (*minimax problem*)

*Polinômio de Chebyshev*

$T_n(x) = \cos(n \arccos(x))$

Raízes de $T_n(x)$: $r_i = \cos(\frac{2i-1}{2n}\pi)$, $i = 1, 2, \dots, n$

**Teorema:** Sejam $x_1, x_2, \dots, x_n$ em $[-1, 1]$. Então, $\max_{x \in [-1, 1]}|\prod_{i=1}^n (x-r_i)| = \frac{1}{2^{n-1}} \leq \max_{x \in [-1, 1]}|\prod_{i=1}^n (x-x_i)|$

Todo $x \in [a, b]$ pode ser escrito como $x = \frac{a+b}{2} + \frac{b-a}{2} y$, $y \in [-1, 1]$.

Então:

$\frac{b-a}{2} \max_{x \in [-1,1]} |\prod_{i=1}^n (x-r_i)| = \frac{b-a}{2} \frac{1}{2^{n-1}} = \frac{(b-a)}{2^n} \leq \frac{(b-a)}{2^n} \max_{x \in [-1, 1]}|\prod_{i=1}^n (x-x_i)| = \max_{x \in [a,b]}|\prod_{i=1}^n (x-x_i)|$

onde $r_i = \cos(\frac{2i-1}{2n}\pi)$, $i = 1, 2, \dots, n$. (raízes de $T_n(x)$)

## Métodos numéricos para EDOs

Métodos numéricos para EDOs

$\begin{cases}x'(t) = f(x,t) \\x(t_0) = x_0\end{cases}$

Dado o intervalo $[t_0, T=t_N]$, particionamos o intervalo em $N$ subintervalos de tamanho $h = \frac{t_N-t_0}{N}$.

$\{ x_n \}_{n=0}^{N} \approx \{ x(t_n) \}_{n=0}^{N}$

$x_n = \mu(t_n, x_{n-1}, h)$

**Def: convergência**

$\lim_{h \to 0} ||x_n - x(t_n)|| = 0$

**Def: ordem de convergência**

$\max_{n=1,...,N} ||x_n - x(t_n)|| \leq C h^p$

### Método de Euler

$x_n = x_{n-1} + h f(t_{n-1}, X_{n-1})$

### Método do Trapézio (ou de Heun)

$x_n = x_{n-1} + \frac{h}{2} (f(t_{n-1}, x_{n-1}) + f(t_n, x_n))$

**Teorema (de convergência Local-Global)**

Seja o método numérico: $x_{k+1} = x_k + h \phi(t_k,x_k,h)$ para $x'(t) = f(t,x(t))$.

Se:

1. $\exists C: || x(t_{k+1}) - (x(t_k) + h \phi(t_k,x(t_k),h)) || \leq C h^{p+1}$
  
2. $\exists \tilde{L}$ : $|| \phi(t_k,y_1,h) - \phi(t_k,y_2,h) || \leq \tilde{L} ||y_1-y_2||$
  

Então: $\max_{n} ||x(t_n) - x_n|| \leq \frac{C}{\tilde{L}} (e^{\tilde{L}(T-t_0)}-1) h^p$

### Método de Runge-Kutta

Como é a tabela de Butcher associada ao método de Runge-Kutta de ordem 4?

$\begin{array}{c|cccc} 0 & 0 & 0 & 0 & 0 \\ \frac{1}{2} & \frac{1}{2} & 0 & 0 & 0 \\ \frac{1}{2} & 0 & \frac{1}{2} & 0 & 0 \\ 1 & 0 & 0 & 1 & 0 \\ \hline & \frac{1}{6} & \frac{1}{3} & \frac{1}{3} & \frac{1}{6} \end{array}$

- A primeira linha (de cima para baixo) apenas diz que $k_1 = F(t_n, x_n)$.

- A segunda linha diz que $k_2 = F(t_n + \frac{h}{2}, x_n + \frac{h}{2}k_1)$.

- A terceira linha diz que $k_3 = F(t_n + \frac{h}{2}, x_n + \frac{h}{2}k_2)$.

- A quarta linha diz que $k_4 = F(t_n + h, x_n + hk_3)$.

- A última linha diz que $x_{n+1} = x_n + h(\frac{1}{6}k_1 + \frac{1}{3}k_2 + \frac{1}{3}k_3 + \frac{1}{6}k_4)$.

### A-estabilidade

A estabilidade diz quão bem meu método reage a erros de arredondamento.

Para determinar se um método numérico é A-estável, ele é frequentemente testado em uma equação diferencial ordinária (EDO) linear simples, que tem a forma $y' = \lambda y$, onde $\lambda$ é um número complexo, com a condição de que a parte real de $\lambda$ seja negativa. Essa EDO é uma espécie de "teste padrão" para avaliar a estabilidade de métodos numéricos. Vamos detalhar isso um pouco mais:

1. **Escolha de $\lambda$**: A razão pela qual escolhemos $\lambda$ com a parte real negativa é que isso garante que a solução exata da EDO decresce exponencialmente com o tempo. Em termos físicos, isso representa um sistema que está se estabilizando com o tempo, como um sistema que retorna ao equilíbrio após ser perturbado.

2. **Aplicação do Método Numérico**: Quando aplicamos um método numérico a essa EDO, queremos que a solução numérica reflita esse comportamento de decaimento exponencial. Se o método for capaz de manter esse comportamento de decaimento exponencial independente do tamanho do passo de tempo escolhido, então ele é considerado A-estável.

3. **Por que Usar um Teste Simples?**: A EDO $y' = \lambda y$ é usada porque é uma das formas mais simples de EDO linear, e ainda assim captura a essência do que se busca em termos de estabilidade. É uma forma de isolar a propriedade de estabilidade do método de outros fatores mais complexos que podem aparecer em EDOs mais complicadas.

4. **Significado da A-estabilidade**: Se um método é A-estável, significa que ele pode lidar eficientemente com problemas de estabilidade numérica, que são comuns em EDOs rígidas. Em outras palavras, um método A-estável não permitirá que erros numéricos cresçam de forma descontrolada, mesmo para passos de tempo grandes.

*Exemplo de como calcular a região de estabilidade para o método de Euler*

$y' = \lambda y$

$y_{n+1} = y_n + h \lambda y_n = (1 + h \lambda) y_n$

$y_n = (1 + h \lambda)^n y_0$

$R(h \lambda) = 1 + h \lambda$

Região de estabilidade: $|R(z)| < 1$

$|1 + z| < 1$

*Exemplo de como calcular a região de estabilidade para a regra do trapézio*

$y' = \lambda y$

$y_{n+1} = y_n + \frac{h}{2} (f(t_n, y_n) + f(t_{n+1}, y_{n+1}))$

$y_{n+1} = y_n + \frac{h}{2} (\lambda y_n + \lambda y_{n+1})$

$[1 - \frac{h}{2} \lambda] y_{n+1} = [1 + \frac{h}{2} \lambda] y_n$

$y_{n+1} = \frac{1 + \frac{h}{2} \lambda}{1 - \frac{h}{2} \lambda} y_n$

$R(h \lambda) = \frac{1 + \frac{h}{2} \lambda}{1 - \frac{h}{2} \lambda}$

Região de estabilidade: $S = \{ z \in \mathbb{C} : |R(z)| < 1 \}$

$S = \{ z \in \mathbb{C} : |\frac{1 + \frac{s}{2}}{1 - \frac{s}{2}}| < 1 \}$

$S = \{ z \in \mathbb{C} : |1 + \frac{s}{2}| < |1 - \frac{s}{2}| \}$

$S = \{ z \in \mathbb{C} : |2 + s| < |2 - s| \}$

A região é todo o semiplano complexo esquerdo ao eixo imaginário (Método A-estável).


Resumindo:

Seja:

$x'(t) = \lambda x(t)$ $\lambda \in \mathbb{C} = \{ \ z \in \mathbb{C} \ | \ Re(z) \leq 0 \ \}$ e seja $\{x_n\}_{n = 0}^{\infty}$ um método que quando aplicado a equação linear satisfaz $x_{n+1} = R(\lambda h) x_n$

Então:

**Definição:** A região de estabilidade do método é $S = \{ z \in \mathbb{C} \ | \ |R(z)| \leq 1 \ \}$ (é o conjunto de valores complexos que garante que a solução do método é estável)

**Definição (A-estabilidade):** Um método é A-estável se sua região de estabilidade satisfaz $S \supseteq \mathbb{C}^{-}$. (Ou seja, se a região de estabilidade contém todo o semiplano esquerdo)


## Solução numérica de EDPs

Estamos analisando a equação do calor:

$\frac{\partial u}{\partial t} = c \frac{\partial^2 u}{\partial x^2}$

Condições iniciais:

$u(x,0) = f(x)$

Condições de fronteira:

$u(0,t) = a(t) \\u(L,t) = b(t)$

**Ideia:** Particionar o espaço e o tempo (Grid, ou uma malha de um plano com eixos x e t, espaçados de tamanho $\Delta x$ e $\Delta t$) [Ver foto do quadro]

$U^i_j \approx u(x_j, t_i)$

Queremos que: $\lim_{\Delta x, \Delta t \rightarrow 0} | u(x_j, t_i) - U^i_j | = 0$

### Método FTCS (Forward in Time, Centered in Space)

$\frac{U^{i+1}_j - U^i_j}{\Delta t} = c \frac{U^i_{j+1} - 2 U^i_j + U^i_{j-1}}{\Delta x^2}$

$U^{i+1}_j = U^i_j + \frac{c \Delta t}{\Delta x^2} (U^i_{j+1} - 2 U^i_j + U^i_{j-1})$

Faz sentido que:

$\frac{U^{i+1}_j - U^i_j}{\Delta t} = c \frac{U^i_{j+1} - 2U^i_j + U^i_{j-1}}{\Delta x^2}$

Temos agora que resolver essa equação para cada ponto $(x_j, t_i)$, mas temos que ter cuidado com as condições de fronteira e iniciais.

Mexendo na equação, temos que:

$U^{i+1}_j = c \frac{\Delta t}{\Delta x^2} U^i_{j+1} + (1 - 2c \frac{\Delta t}{\Delta x^2}) U^i_j + c \frac{\Delta t}{\Delta x^2} U^i_{j-1}$

Definimos: $V = c \frac{\Delta t}{\Delta x^2}$

$U^{i+1}_j = V U^i_{j+1} + (1 - 2V) U^i_j + V U^i_{j-1}$

Vamos colocar as condições de fronteira e iniciais:

* $U^0_j = f(x_j) = f(j \Delta x)$
  
* $U^i_0 = a(t_i) = a(i \Delta t)$
  
* $U^i_N = b(t_i) = b(i \Delta t)$
  

Se eu quero obter, por exemplo, $U^1_1$, $(x_1, t_1)$, eu preciso de $U^0_1$, $U^0_2$ e $U^0_0$.

$U^1_1 = V U^0_2 + (1 - 2V) U^0_1 + V U^0_0$

E assim vou fazendo para todos os pontos.

Mas, vamos pensar de forma vetorial:

*Definindo:* $U^i = \begin{bmatrix} U^i_0 & U^i_1 & \cdots & U^i_N \end{bmatrix}^T$

$U^{i+1} = \begin{bmatrix} 1-2V & V & 0 & \cdots & 0 & 0 \\V & 1-2V & V & \cdots & 0 & 0 \\0 & V & 1-2V & \cdots & 0 & 0 \\\vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\0 & 0 & 0 & \cdots & 1-2V & V \\0 & 0 & 0 & \cdots & V & 1-2V \end{bmatrix} U^i + \begin{bmatrix} a(i \Delta t) \\ 0 \\ 0 \\ \vdots \\ 0 \\ b(i \Delta t) \end{bmatrix}$

$U^0 = \begin{bmatrix} f(\Delta x) \\ f(2 \Delta x) \\ \vdots \\ f((N-1) \Delta x) \end{bmatrix}$

$\begin{cases} U^{i+1} = AU^i + b \\U^0 = f \end{cases}$

A matriz $A$ precisa ter autovalores menores que 1 para que a solução não exploda

**Estabilidade:** $V = c \frac{\Delta t}{\Delta x^2} \leq \frac{1}{2}$

### Método BTCS (Backward in Time, Centered in Space)

$\frac{U^{i+1}_j - U^i_j}{\Delta t} = c \frac{U^{i+1}_{j+1} - 2 U^{i+1}_j + U^{i+1}_{j-1}}{\Delta x^2}$

$-U^{i+1}_{j-1} + (1 + 2 \frac{c \Delta t}{\Delta x^2}) U^{i+1}_j - U^{i+1}_{j+1} = U^i_j$

*Pensar em como fazer esses métodos de forma matricial.*

---

### Questões resolvidas com métodos numéricos para EDPs

**QUESTÃO1-LISTA5b**

*Solução:*

A estabilidade para o método FTCS é dada por:

$V = c \frac{\Delta t}{\Delta x^2} \leq \frac{1}{2}$

Dado que $\Delta t = 0.06$ e $c = \pi^2$, temos que:

$V = \pi^2 \frac{0.06}{\Delta x^2} \leq \frac{1}{2}$

$\Delta x \geq \sqrt{\frac{2 \pi^2}{0.06}}$


## Simulação estocástica

Tipos de problemas que podem ser resolvidos com simulação estocástica:

1. $\int_a^b f(x) dx$; $\int \int_R f du dv$, $f(x)$ é uma função conhecida, mas não é possível calcular a integral analiticamente.
  
2. Calcular áreas de figuras geométricas complexas. Qual proporção de uma área está afetada por um fenômeno?

**Lei dos grandes números:** Seja $X_1, X_2, ..., X_n$ uma sequência de variáveis aleatórias independentes e identicamente distribuídas, com média $\mu$ e variância $\sigma^2$. Então, para qualquer $\epsilon > 0$:

$\lim_{n \rightarrow \infty} P \left( \left| \frac{X_1 + X_2 + ... + X_n}{n} - \mu \right| < \epsilon \right) = 1$

**Teorema do limite central:**

$P(|\frac{S_N - \mu}{\frac{\sigma}{\sqrt{N}}}| \leq a) \rightarrow \int_{-a}^a \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^2}{2}} dx$

Exemplo, se $a=3$, o resultado é $0.9973$.

**Distribuição uniforme:** $X \sim U(a,b)$

$\begin{cases} f(x) = \frac{1}{b-a} & a \leq x \leq b \\ 0 & \text{caso contrário} \end{cases}$

$u = (b-a)y + a$, onde $y \sim U(0,1)$, sabemos como gerar uma uniforme [a,b] a partir de uma uniforme [0,1].

Fórmula para calcular o número de amostras necessárias para obter uma precisão $\epsilon$ e um nível de confiança de $99\%$, por exemplo:

$n \geq \frac{z^2 \sigma^2}{\epsilon^2} = \frac{9p(1-p)}{\epsilon^2}$

E se eu não souber o valor de $\sigma^2$? Uso $p(1-p)$, onde $p$ é a proporção de sucessos.


### Questões resolvidas com simulação estocástica

1)  Um ponto $x$ e um ponto $y$ são selecionados ao acaso (i.e. conforme a distribuição uniforme) no intervalo
$[0, 2]$ e $[2, 3]$, respectivamente. Use o método de simulação Monte Carlo para calcular aproximadamente a
probabilidade de que os três segmentos $[0, x]$, $[x, y]$ e $[y, 3]$ possam formar um triângulo.

*Solução:* 



```matlab
# Método para checar se os segmentos formam um triângulo
def can_form_triangle(a, b, c):
    # Agora a, b, c são os comprimentos dos segmentos de linha
    return a + b > c and a + c > b and b + c > a

# Simulação de Monte Carlo para estimar a probabilidade de formação de um triângulo
def monte_carlo_triangle_simulation(n):
    count = 0
    for _ in range(n):
        # Gera dois pontos x e y de acordo com as condições do problema
        x = random.uniform(0, 2)
        y = random.uniform(2, 3)
        # Calcula os comprimentos dos segmentos de linha
        segment1 = x  # [0, x]
        segment2 = y - x  # [x, y]
        segment3 = 3 - y  # [y, 3]
        # Checa se esses segmentos podem formar um triângulo
        if can_form_triangle(segment1, segment2, segment3):
            count += 1
    return count / n

# Número de simulações
num_simulations = 100000

# Realiza a simulação
probability = monte_carlo_triangle_simulation(num_simulations)
probability
```

2) Considere o problema de calcular usando Monte Carlo a área interior da elipse $40x^2 + 25y^2 + y + \frac{9}{4} - 52xy + 14x$
em $0 \leq x, y \leq 1$:

- Implemente uma função Matlab para calcular a área, gerando $N = 10^4$ números pseudo-aleatórios.

- Quantas amostras são, ao menos, necessárias para você calcular essa área com um erro $< 10^{-4}$

*Solução:*

a) Implementação da função para calcular a área da elipse usando o método de Monte Carlo:

```matlab
function area = monte_carlo_ellipse_area(N)
    count_inside = 0;
    for i = 1:N
        % Gerar pontos (x, y) dentro do quadrado [0,1]x[0,1]
        x = rand();
        y = rand();
        % Verificar se o ponto está dentro da elipse
        if (40*x^2 + 25*y^2 + y + 9/4) <= (52*x*y + 14*x)
            count_inside = count_inside + 1;
        end
    end
    % A área do quadrado é 1, então a área da elipse é proporcional ao
    % número de pontos dentro da elipse em relação ao número total de pontos
    area = count_inside / N;
end

% Número de pontos pseudoaleatórios
N = 10^4;

% Cálculo da área pelo método de Monte Carlo
area_estimate = monte_carlo_ellipse_area(N);
fprintf('A área estimada da elipse é: %f\n', area_estimate);
```

b) Cálculo do número de amostras necessárias para obter um erro menor que $10^{-4}$:

$n \geq \frac{z^2 \sigma^2}{\epsilon^2} = \frac{9p(1-p)}{10^{-8}}$

Onde $p$ é a proporção de pontos dentro da elipse calculada na simulação anterior.

3) Suponha que você está no ponto de ônibus às 10:00 horas da manhã. Sabendo que o ônibus chega ao ponto em algum tempo uniformemente distribuído entre 10:00 e 10:30 da manhã; use simulação Monte Carlo para determinar a probabilidade de que, se às 10:15 o ônibus não chegou ainda, você tenha que esperar ao menos 10 minutos adicionais.

*Solução:*

```matlab
% Número de simulações
N = 1000000;

% Gerar tempos de chegada do ônibus entre 0 e 30 minutos (10:00 - 10:30)
chegadas = 30 * rand(N, 1);

% Contar chegadas entre 10:15 (15 minutos) e 10:25 (25 minutos)
chegadas_10_15_a_10_25 = chegadas(chegadas > 15 & chegadas <= 25);

% Probabilidade condicional do ônibus chegar entre 10:15 e 10:25,
% dado que não chegou até as 10:15
probabilidade_monte_carlo = length(chegadas_10_15_a_10_25) / (N - sum(chegadas <= 15));

% Exibir a probabilidade
disp(['A probabilidade calculada por Monte Carlo é aproximadamente: ', num2str(probabilidade_monte_carlo)]);
```

4) $M$ dados honestos são lançados simultaneamente. Os dados que mostraram o número 6 são retirados do jogo, e com os dados restantes se repete o jogo (ou seja, os dados restantes se lançam novamente e aqueles que mostraram o número 6 são retirados do jogo). O jogo continua até que todos os dados sejam retirados. Qual o número médio de lançamentos necessários para acabar o jogo?

*Solução:*

```matlab
% Número de simulações
numSimulacoes = 100000;
% Número inicial de dados
M = 6; % Substitua com o valor de M fornecido na questão
% Contador para o total de lançamentos em todas as simulações
totalLancamentos = 0;

% Loop sobre o número de simulações
for i = 1:numSimulacoes
    dadosRestantes = M;
    lancamentos = 0;
    % Continue até que todos os dados sejam retirados
    while dadosRestantes > 0
        % Lançar todos os dados restantes
        lancamentosDados = randi(6, dadosRestantes, 1);
        % Contar quantos dados mostraram o número 6
        seis = sum(lancamentosDados == 6);
        % Retirar esses dados do jogo
        dadosRestantes = dadosRestantes - seis;
        % Incrementar o contador de lançamentos
        lancamentos = lancamentos + 1;
    end
    % Adicionar ao total de lançamentos
    totalLancamentos = totalLancamentos + lancamentos;
end

% Calcular o número médio de lançamentos necessários
mediaLancamentos = totalLancamentos / numSimulacoes;

% Exibir o resultado
disp(['O número médio de lançamentos necessários é: ', num2str(mediaLancamentos)]);
```


