https://stackoverflow.com/questions/12996380/uniform-distribution-fitting-in-matlab

uniform distribution fitting in matlab
Ask Question
Asked 7 years, 8 months ago
Active 4 years ago
Viewed 5k times

2


1
I have a data set and would like to fit them to uniform distribution and calculate goodness of fit with Matlab. However, I found that uniform is not included in function 'fitdist'. Is there any method to do uniform distribution fitting in Matlab?

matlab distribution model-fitting
share  improve this question  follow 
asked Oct 21 '12 at 8:58

Tao Liu
3511 silver badge66 bronze badges
I was just wondering if my answer was any use to you? If not, please let me know why and perhaps I can improve it. Cheers. – Colin T Bowers Oct 24 '12 at 0:05
add a comment
4 Answers
Active
Oldest
Votes

6


When you say you would like to fit the dataset to the uniform, I'm assuming that what you mean is that you would like to estimate the parameters of a uniform distribution that best fit your dataset.

This is actually quite an interesting question. I'm not surprised that fitdist was no help as the uniform distribution is a bit of a special case. For example, it can be shown that under some circumstances, the maximum likelihood estimate of the parameters of a uniform distribution does not exist, and under other circumstances, has no unique solution.

So, what to do? Well, a uniform distribution has two parameters, a and b, which define the lower and upper bound of the density. Let X denote your dataset (say, a column vector of observations). A naive estimator of a and b is:

a = min(X);
b = max(X);
Of course these estimates will over-estimate (for a) and under-estimate (for b) the true parameters almost surely, since it is unlikely that a random sample drawn from the density will fall right on the boundary.

For the case where it is known that a is 0, the minimum variance unbiased estimator of b is:

b = max(X) + (max(X) / length(X))
This estimator is related to the famous German Tank Problem. For the general case, I don't actually know any estimation theory (although I'm sure there must be some). My first guess would be to use the naive min/max estimator, but subtract and add the average distance between the observations in your dataset, ie:

a = min(X) - c;
b = max(X) + c;
where

c = (max(X) - min(X)) / length(X)
As for goodness-of-fit, hopefully someone else on SO knows something, as I'd need to do a fair bit of research myself to answer that. Good Luck!

share  improve this answer  follow 
answered Oct 21 '12 at 10:30

Colin T Bowers
14.9k66 gold badges4545 silver badges7373 bronze badges
add a comment

2


Further to Colin's answer, goodness of fit for uniform distribution can be calculated using a Pearson's chi-squared test.

If you have access to the Matlab stats toolbox you can perform this fairly simply by using the chi2gof function. Example 3 in the documentation shows how to apply it to a uniform distribution.

share  improve this answer  follow 
answered Apr 3 '13 at 22:07

Alan
3,07511 gold badge1414 silver badges2020 bronze badges
add a comment

2


Transform your variable to a normal distributed variable and use "kstest". So if you have a variable X that is uniform from a to b make the following code

X_uni=(X-a)/(b-a); %Uniform 0,1 variable

X_norm=norminv(X_uni); % transform to normal distributed variable
[h,P]=kstest(X_norm) ; %P is the test statistic
share  improve this answer  follow 
edited Apr 26 '15 at 22:24
answered Apr 26 '15 at 22:10

Peter Pallesen
2122 bronze badges
add a comment

1


Just to expand of Alan answer, to know how to properly used Pearson's chi-squared test

Setting Parameters
N=100; % sample size
a=0; % lower boundary
b=1; % higher boundary
Sample N uniformly distributed values between a and b. And in the second line add some bais to make it not uniform if you want to test the code.

x=unifrnd(a,b,N,1);
%x(x<.9) = rand(sum(x<.9),1);
Using chi2gof
As described here, with chi2gof, you can't use the 'cdf of the hypothesized distribution' and need to specified the bins, the edges and the expected values.

nbins = 10; % number of bin
edges = linspace(a,b,nbins+1); % edges of the bins
E = N/nbins*ones(nbins,1); % expected value (equal for uniform dist)

[h,p,stats] = chi2gof(x,'Expected',E,'Edges',edges)
Using chi2cdf
With this function you need to supply the chi-squared test statistic, $\displaystyle \chi ^{2}$ which can be computed with the function histogramm:

h = histogram(x,edges);
chi = sum((h.Values - N/nbins).^2 / (N/nbins));
k = nbins-1; % degree of freedom
chi2cdf(chi, k)
Note, that if you don't use the edges to compute the number of value per bins, histogramm will choose them from the lower value to the highest and therefore the final score will be different than with chi2gof

At the end, you want to use the p value to answer the question "Can I safely reject the null hypothesis (i.e. x is not a coming from a uniform distribution) ? ". Yes, you can safely say that x is not coming from a uniform distribution if p is lower than a significant level (alpha).
