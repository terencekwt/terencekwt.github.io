---
title: "The Efficient Frontier"
subtitle: "Deriving Markowitz's equation"
author: Terence Tam
date: 2015-06-07 12:00:00
layout: post
header-img: "img/post-bg-06.jpg"
---

We all have to deal with 401K allocation some point in our life right? Often times, we are very indecisive in choosing the best subset from a basket of securities that will give us the highest return in the long run, yet minimizing the risk. The efficient frontier by Markowitz can help us decide by showing us the minimum risk for each level of expected return and vice versa.

Let's say you have three funds to choose from. Security $A$ tracks the S&P500, Security $B$ tracks the NASDAQ and prices of the technology sector, and Security $C$ is an indicator of the energy sector. Given we have historical records (daily stock price, daily % return) of these securities, we could find the variance and the covariance for these stocks. The variance of one stock would be the fluctuating price of that particular stock, where a higher variance would indicate the stock has a greater volatility, thus a higher risk because the %return is not guaranteed or fixed. Covariances, on the other hand, indicates how much two stocks follow similar movements. For instance, two stocks both from U.S. market would go down if the broader U.S. market is on a downward trend.

In our example, let's say the four securities takes on four random variables. Then the expected % return for the securities are

$$ \bar{Z} = \begin{pmatrix} E(A) \\ E(B) \\ E(C) \\ E(D) \end{pmatrix} = \begin{pmatrix} 14 \\ 12 \\ 15 \\ 7 \end{pmatrix}$$

where 14 stands for 14% average expected return for stock $A$, 12% for stock $B$, and so on.

Then, we can also define the sets of weights for the portfolio

$$ W = \begin{pmatrix} w_A \\ w_B \\ w_C \\ w_D \end{pmatrix} $$

such that $w_A+w_B+w_C+w_D=$ 1

The total average expected return of a portolio $P$ would be the weighted sum

$$E(P) = W^{T}\bar{Z}$$

The variance of the portfolio $P$ will be

$$Var(P) =  Var(W^{T}\bar{Z}) = W^{T}Var(\bar{Z})W = W^{T}\Sigma W$$

where $\Sigma$ is the variance-covariance matrix of vector $\bar{Z}$.

The objective here is to minimize the porfolio variance given a porfolio mean $\bar{Z}$, and subject to the weights add up to 1. Our optimization problem could be defined as follows:

$$ \min_{W} W^{T}\Sigma W$$

$$ s.t. 1^{T}W = 1, E(P) = W^{T}\bar{Z}$$

From here, we would use the Lagrangian method to solve the min (I can derive this in another post). Also, from the lagrangian equations we can derive the relationship between $\sigma_p$ and $\mu_p$, which turns out to be a hyperbola of the form

$$ \sigma_p^2 = \frac{B\mu_p^2 - 2C\mu_p + A}{D}$$

where 

$$ A = \mu^T\Sigma^{-1}\mu; B=1^T\Sigma^{-1}1, C=1^T\Sigma^{-1}\mu, D= AB - C^2 $$


Let's run a simple R program to generate the efficient frontier for our particular choices of securities.


{% highlight r %}
zbar <- c(14, 12, 15, 7)
S <- matrix(c(185, 86.5, 80, 20, 86.5, 196, 76, 13.5, 80, 76, 411, -19, 20, 13.5, -19, 25), 4)
S
{% endhighlight %}



{% highlight text %}
##       [,1]  [,2] [,3]  [,4]
## [1,] 185.0  86.5   80  20.0
## [2,]  86.5 196.0   76  13.5
## [3,]  80.0  76.0  411 -19.0
## [4,]  20.0  13.5  -19  25.0
{% endhighlight %}

Let's calculate the coefficient, and find the min-variance


{% highlight r %}
#unity vector
unity <- rep(1, length(zbar))
#inverse of S
S_inv <- solve(S)

#standard deviation for each tock
stddevs <- sqrt(diag(S))

#calculate the coefficients
A <- t(unity) %*% S_inv %*% unity
B <- t(unity) %*% S_inv %*% zbar
C <- zbar %*% S_inv %*% zbar
D <- A*C-B^2

#plot efficient frontier (0 - 30% expected return range)
mu <- seq(1:300)/10
minvar <- (A*mu^2 - 2*B*mu + C)/D
minstd <- sqrt(minvar)

plot(minstd,mu, 'l', main="The Efficient Frontier of n Assets", xlab="Standard Deviation (%)",
     ylab="Expected Return (%)", col="blue")
points(stddevs, zbar, col="red", pch="*")
{% endhighlight %}

![plot of chunk unnamed-chunk-2](/figures/unnamed-chunk-2-1.svg) 
