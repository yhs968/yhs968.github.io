---
layout: post
date:   2016-02-28
title:  "빈도주의 통계학의 문제점"
categories: jekyll update
---
<meta charset="UTF-8">
<!--Mathjax Config 설정-->
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  jax: ["input/TeX","input/MathML","output/HTML-CSS","output/NativeMML"],
  extensions: ["tex2jax.js", "mml2jax.js", "asciimath1jax.js", "MathMenu.js","MathZoom.js"],
  TeX: {
    extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
    equationNumbers: {autoNumber: "AMS"}
  },
  tex2jax: {
    inlineMath: [ ['$', '$'], ['\\(', '\\)'] ],
    displayMath: [ ['$$', '$$'], ["\\[", "\\]"] ],
    processEscapes: true,
  }
});
</script>
<!--Mathjax CDN 사용-->
<script type="text/javascript" async
            src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

## 빈도주의 통계학의 문제점
---
시작하기 전에, [ASA(American Statistical Associations)에서 공식적으로 발표한 p-value에 대한 경고](https://www.google.co.kr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwiVhtnTnrrLAhVBPqYKHXKLAd8QFggjMAA&url=https%3A%2F%2Fwww.amstat.org%2Fnewsroom%2Fpressreleases%2FP-ValueStatement.pdf&usg=AFQjCNHdDDwRYxvIG2R87NWf_Sa8bRsT8Q&sig2=JEff1wpb7NEONgIbYdCRwg&bvm=bv.116573086,d.dGY)를 읽어보자. p-value를 이용한 고전적인 빈도주의적 가설검정 과정에 굉장히 문제가 많음을 알 수 있다.

이 포스팅에서는 이러한 문제들이 왜 일어나고 있는지를 빈도주의 통계학의 몇가지 고전적인 도구(confidence interval과 p-value를 이용한 가설검정)들을 중심으로 파헤칠 것이다.

### 0. 빈도주의 통계학의 철학적 한계
<table border="1" style="width:100%">
  <tr>
    <td></td>
    <td>확률의 정의</td>
    <td>모수</td>
    <td>데이터</td>
  </tr>
  <tr>
    <td>빈도주의</td>
    <td>가상의 반복되는 실험에서의 발생 빈도</td>
    <td>고정</td>
    <td>변화</td>
  </tr>
  <tr>
    <td>베이지안</td>
    <td>가상의 반복되는 실험에서의 발생 빈도 + 추정값들에 대한 불확실성의 정도</td>
    <td>변화</td>
    <td>고정</td>
    </tr>
</table>
<br>
위 표는 빈도주의와 베이지안의 차이점을 요약한 것이다. 실제 결과에 영향을 주지 않는 철학적 차이로 보일지도 모르겠지만, 이 철학적 차이가 빈도주의 통계학에서 실질적으로 문제를 불러일으키게 된다.  
먼저, 베이지안들이 사용하는 확률의 정의와 빈도주의자들이 사용하는 확률의 정의를 살펴보자. 베이지안들이 사용하는 확률의 정의가 조금 이상해보일지도 모르겠지만, 다음 예를 통해 왜 확률을 저런 식으로 정의하는지 알 수 있다.
우리가 복권 하나를 샀다고 가정하고, 1등에 당첨될 확률이 0.000000001이라고 추정했다고 하자. 그런데, 이 추정값이 얼마나 정확한지를 하나의 수치로 나타낼 수 있을까?  
베이즈 통계에서는 확률에 대한 정의를 확장했기 때문에 확률의 개념을 이용해 손쉽게 추정의 정확도를 표현할 수 있다. 만약 추첨 결과를 이미 보았다면 '추정값에 대한 불확실성'은 0이라는 확률로 나타낼 수 있고, 결과가 발표되기 전이라면 [0,1] 사이의 임의의 값을 사용해 우리의 추정에 대한 확실함(믿음)의 정도를 나타낼 수 있다. 그러나 빈도주의 통계학에서는 추정값에 대한 불확실성을 확률로는 나타낼 수 없다. 확률의 정의 자체가 '사건'에 대한 것으로 한정되기 때문이다.

### 1. confidence interval vs credible interval
---
확률로 직접 추정에 대한 불확실성을 나타낼 수 없기에, 빈도주의 통계학에서 자주 사용하는 도구 중 하나로 신뢰구간(confidence interval)이라는 도구가 있다. 일반적으로 널리 알려진 신뢰구간에 대한 해석은 다음과 같다.  
<br>*"95% 확률로 모수가 항상 포함되는 구간"*<br>  
이 신뢰구간이 꽤 좁다면 추정치를 확률로 직접 표현하지는 못해도 우리의 추정치에 대해 확신을 가질 수 있을 것이라는 것이 빈도주의자들의 주장이다.  
위에서 말한 신뢰구간에 대한 해석이 정확하다면 빈도주의자들의 주장은 옳다. 그러나 안타깝게도 신뢰구간에 대한 위의 해석은 틀린 해석이다. 위 해석은 베이즈 통계에서 사용하는 credible interval(혹은 Bayesian confidence interval)에 대한 설명이다.

#### confidence interval에 대한 오해와 정확한 의미

모수가 고정되어있기 때문에 빈도주의 통계학에서 confidence interval의 정확한 해석은 다음과 같다.  
<br>***“(95% 신뢰구간의 경우)비슷한 종류의 데이터를 반복 샘플링해서 95% confidence interval을 구하면, 95%의 실험에서 모수가 그 구간에 포함된다.”***<br>  
**얼핏 보면 "95% 확률로 모수가 항상 포함되는 구간"과 같은 의미로 보일 수 있지만, 사실 그 구간과는 *전혀* 상관이 없다.**  
왜 그런지 수식을 통해 자세히 살펴보자. 빈도주의 통계학의 framework를 따라 모평균 $$\mu$$에 대한 추론을 한다고 하자. 그러면 일반적으로 모분산 $$\sigma$$를 알고 있을 때 $$(1-\alpha)\%$$ 신뢰구간은 중심극한정리에 의해 다음과 같이 구한다.

$$
\begin{eqnarray}
\bar{x}|\mu,\sigma\sim\mathcal{N}(\mu,\sigma^2/N) (중심극한정리) &\rightarrow& P\left(z_{\alpha/2}\le\frac{\bar{x}-\mu}{\sigma/\sqrt{N}}\le z_{1-\alpha/2}\right)\notag\\ &=&P(\bar{x}- z_{\alpha/2}\frac{\sigma}{\sqrt{N}}\le\mu\le \bar{x}+z_{\alpha/2}\frac{\sigma}{\sqrt{N}})\text{(표준정규분포의 성질에 의해)}\notag\\ &=&1-\alpha\notag\\ &=&0.95\qquad\text{ if }\alpha=0.05\notag\\
\end{eqnarray}
$$

여기서 확률 변수는 $$\bar{x}$$ 뿐이다. 따라서 $$\alpha=0.05$$일 때 위 식이 의미하는 바는 정확히 다음과 같다.

**“동일한 모집단에서 *표본 평균을 샘플링*하면 모평균 $$\mu$$가 구간 $$[\bar{x}- z_{0.05/2}\frac{\sigma}{\sqrt{N}}, \bar{x}+z_{0.05/2}\frac{\sigma}{\sqrt{N}}]$$ 에 포함될 확률이 0.95이다.”**

즉 100번 모집단에서 샘플링을 하면 100개의 *서로 다른* 신뢰구간이 형성되고, 그 중 95개의 구간이 모평균을 포함한다는 의미다. 좀 더 정리하면, 이 구간이 우리에게 줄 수 있는 최대한의 정보는 다음과 같다.

**“95%의 샘플에서는 이 구간 내에 모평균 $$\mu$$가 포함되고, 5%의 샘플에서는 이 구간 내에 모평균 $$\mu$$가 포함되지 않는다.”**

그러면, 내가 가진 *특정* 샘플 데이터를 통해 구간을 계산하면 모평균이 포함될 확률이 얼마일까? 굉장히 의외로 들릴지 모르겠지만, *0이거나 1이다.* 사실, 내가 가진 데이터는 이미 끝난 실험의 결과이기 때문에, 그 어떠한 불확실성도 개입할 여지가 없다. 고정된 모평균 $$\mu$$의 위치에 따라 포함되거나, 안 되거나 이미 결정이 끝난 상태이다. 다시 말해, 만약 모평균을 안다고 하면 이 구간이 *관찰이 끝난 특정 샘플* 을 본 뒤 모수에 대해 줄 수 있는 정보는 정확히 다음과 같다.  
<br>*“이 구간에는 모평균이 포함되어 있어”* 혹은 _“이 구간에는 모평균이 포함되어 있지 않아”_<br>  
그런데 문제는 모평균을 모른다는 점이다. 그러면 우리가 이 구간에서 얻을 수 있는 정보는 다음과 같이 수정된다.  
<br>_“이 구간에는 모평균이 포함되어 있을 수도 있고, 아닐 수도 있어.”_<br>  
**한마디로, 주어진 데이터를 가지고 신뢰구간을 계산해봤자 모평균에 대해 _아무_ 정보도 얻을 수 없다.**  
그러면 이번에는 분석을 위해 우리가 가진 **특정 샘플 데이터**를 가지고 모수를 추정한 뒤, confidence interval에 다음 질문을 해보자.

**"*이 샘플 데이터*를 가지고 신뢰구간을 계산했는데, 모평균 $$\mu$$가 어디쯤 있을까요?"**

알 수 있을리가 없다. 위에서도 살펴봤듯이, confidence interval은 모평균에 대해 아무 정보도 주지 못하기 때문이다. 설령 $$\bar{x}$$ 를 10000번 샘플링($$\bar{x}_1,\bar{x}_2,\bar{x}_3,...$$)하여 만든 10000개의 신뢰구간 중에 9999번 모평균이 포함된다고 해도, **내가 지금 가지고 있는 특정 샘플 데이터($$\bar{x}_i$$)를 바탕으로 신뢰구간을 만들면 모평균의 대략적인 위치나 추정의 신뢰도는 커녕 이 구간에 모평균이 포함되었는지 여부조차도 알 수 없다**는 것이다.

#### credible interval

베이지안 credible interval은 다음과 같이 구한다.

$$
\begin{eqnarray}
&& 1.\;사후분포\;p(\mu|\bar{x})\propto p(\mu)p(\bar{x}|\mu)\text{를 찾는다.}\notag\\ && 2.\;95\%\text{ credible interval}=\int_{\mu_{0.025}}^{\mu_{0.975}}p(\mu|\bar{x})d\mu\notag\\ &&=p(\mu_{0.025}\le\mu\le\mu_{0.975}|\bar{x})=0.95,\quad\mu_{0.025}\text{:0.025분위수, }\mu_{0.975}\text{0.975분위수}\notag\\
\end{eqnarray}
$$

위 구간이 credible interval이다. 식을 해석하면 다음과 같은 의미가 된다.  
<br>**"*샘플* 표본평균 $$\bar{x}$$ 가 주어졌을 때, 확률변수 $\mu$ 가 $$(\mu_{0.025},\mu_{0.975})$$ 에 포함될 확률이 95%이다."**<br>  

여기서는 데이터 $$\bar{x}$$ 가 고정되어있고 모수만 확률변수이기 때문에 credible interval은 항상 고정이다. 관찰값을 토대로 $$\mu$$가 포함될 확률이 95%인 고정된 구간을 찾은 것이다. **우리가 찾던 바로 그 구간이다. 이 구간이 좁다면 추정의 신뢰도가 높은 것이고, $$\mu$$ 의 위치도 대략적으로 추정해낼 수 있다.**

### 2. 빈도주의적 가설검정과 p-value의 문제점
---

#### 고전적인 빈도주의적 가설검정

우선 빈도주의 framework에서 자주 사용되는 p-value를 이용한 고전적인 가설검정에 대해 간단히 소개하고 넘어가겠다. 완전히 같은 과정을 p-value 대신 critical region(기각 영역)이라는 개념을 사용하여 수행할 수도 있지만, 따로 소개하지 않겠다.

1.  증명하고자 하는 가설(대립가설)을 $$H_1$$로, 그에 반대되는 가설(귀무가설, **null hypothesis**)을 $$H_0$$으로 놓는다.
2.  $$H_0$$가 맞다고 가정하고, 이를 검정하기 위한 검정통계량(test statistics)을 설정한다.
3.  검정 통계량(test statistic)의 분포에 대한 가정에 근거하여, p-value를 계산한다.
$$
\begin{eqnarray}
p-value &\triangleq& P(\text{current data is observed}\cup\text{more extreme data will be observed}|H_0=true)\notag\\
\end{eqnarray}
$$

1.  $$H_0$$를 부정하는데 “충분한”, 혹은 “유의미한(**statistically significant**)” 근거가 될 수 있는 threshold를 정한다. 일반적으로 0.05나 0.1을 사용한다.(사용자 마음이다.) 이 threshold를 유의수준(significance level)이라고 한다.
2.  만일 위에서 정한 threshold보다 p-value가 작다면, 이를 "통계적으로 유의미하다(statistically significant)"고 하며, $$H_0$$를 기각하기 위한 충분한 증거가 주어진 것으로 보고 $$H_0$$을 기각한다.
3.  $$H_0$$이 아니므로 자동으로 $$H_1$$가 맞는 가설이 된다. 검정 끝!

언뜻 말만 들으면 그럴듯해 보일지도 모르나 이 가설검정 프로세스의 신뢰성을 떨어뜨리는 두가지 문제가 있다. 1) p-value의 구조적 문제 2) 검정 프로세스 자체가 가지는 한계이다. p-value의 구조적 문제에 대해 먼저 살펴보자.

#### 1. p-value의 신뢰성 문제 : coherence의 위반

**coherence란, 같은 데이터를 가지고 분석을 했다면, 분석 방법론이 조금 다르더라도 비슷한 결론에 이르러야 한다**는 통계학의 중요한 metaprinciple이다. 아마 우리 모두 이에 동의할 수 있을 것이다. 베이지안 가설검정 과정은 coherence를 만족한다.
그런데, 빈도주의적 가설검정에 사용되는 **p-value는 실험의 implicit assumption, 특히 stopping rule에 취약**한 탓에 coherence를 위반한다. 예제를 통해 살펴보자. 같은 동전을 던지는 실험을 2번 하되, stopping rule이 다르다고 가정하겠다.[2]  
    1. 첫번째 실험: 그냥 동전을 12번 던진다. 뒷면이 나오면 성공, 앞면이 나오면 실패로 간주한다. 뒷면이 3번, 앞면이 9번이 나왔다.  
    2. 두번째 실험: 뒷면이 3번 나올 때까지 동전을 던진다. 뒷면이 나오면 성공으로 간주한다. 12번째 시행에서 3번째 뒷면을 얻어 실험을 종료하였다.  
첫번째 실험은 단순한 Binomial 모델로, 두번째 실험은 Negative Binomial 모델로 모델링하는 것이 가장 자연스럽다. 그런데 동전이 fair하다는 가정을 null hypothesis로 p-value를 구해보면 **둘의 p-value는 매우 크게 차이가 난다**(첫번째 실험: 0.146, 두번째 실험: 0.0327). 어떤 stopping rule을 사용하느냐에 따라서 결론이 뒤집히는 것이다. **그런데, 실제로 결과를 generate한 확률 과정이나 결과 자체는 똑같다.** 과연 어느 결과가 맞다고 해야 할까?  
이러한 이유로, FDA(미국 식약처)는 베이지안 방법들을 더 권장하고 있다. 베이지안 가설검정은 확률과정에 대해 아무 정보를 주지 못하는 이러한 stopping rule의 영향을 받지 않음이 증명되어있으며, 기존의 빈도주의 방법에서 p-value가 왜 stopping rule에 취약한지도 규명되었다.[12]

다음은 빈도주의/베이지안의 어떤 차이가 이런 현상을 만드는지에 대한 증명의 sketch이다. 다른 논의에 영향을 주지 않는 부분이니 관심이 없다면 *2. p-value의 해석상의 오류* 부분으로 넘어가길 바란다.

#### stopping rule이 bayesian/frequentist 가설검정에 주는 영향에 대한 증명
편의상 stopping rule을 $$\tau$$로 나타내겠다. $$\tau$$ 는 크게 다음의 2가지 종류로 나눌 수 있다.  
    1. *deterministic* : 정해진 횟수의 실험을 하면 실험을 멈춘다. 첫번째 실험에 해당한다.  
    2. *randomized* : 특정 확률로 실험을 멈춘다. 실험을 멈출 확률이 모수와 관련이 없는 경우 $$\tau$$ 는 *noninformative*하다고 한다.  
사실, likelihood function에는 우리가 평소에는 잘 생각하지 못하는 이러한 정보가 implicitly assumed되어 있다. 우리는 임의의 실험에 대해 likelihood function에 숨겨져있는 assumption을 다음과 같이 직접 드러낼 수 있다.  
$$likelihood=P(n,\mathbf{x}|\tau,\theta)$$  
여기서 n은 stopping 이후에 우리가 가지고 있는 모든 샘플의 크기이고, $$\mathbf{x}$$ 는 관찰된 n개의 데이터, $$\tau$$ 는 noninformative stopping rule이다.(**아닌 경우에는 베이즈 가설검정도 stopping rule의 영향을 받는다.**) 식을 한번 더 분해해보자.    
$$
\begin{eqnarray}
P(n,\mathbf{x}|\tau,\theta)&=&P(\mathbf{x}|\tau,\theta)P(n|\mathbf{x},\tau,\theta)\notag\\
&=&P(\mathbf{x}|\theta)P(n|\mathbf{x},\tau)\notag\\
&=&\text{given theta, x is observed, and then decide whether to continue according to the stopping rule}\notag\\
\end{eqnarray}
$$  
두번째 등호는 $$\mathbf{x}$$의 값 자체는 stopping rule에 독립적이고, noninformative stopping rule의 정의에 의해 $$P(n|\mathbf{x},\tau,\theta)=P(n|\mathbf{x},\tau)$$이기 때문이다. 그러면, 우리는 posterior 확률을 다음과 같이 보다 정확하게 나타낼 수 있다. $$\mathbf{x}$$ 가 결정된 뒤에 매번 실험을 계속할지를 결정하므로 $$\mathbf{x}$$ 와 $$n$$ 각각이 별도의 확률변수이다.  
그러면 각각 다른 stopping rule $$\tau_1, \tau_2$$에 대해 다음이 성립한다.  
$$
\begin{eqnarray}
P(n,\mathbf{x}|\tau_1,\theta)&=&P(\mathbf{x}|\theta)P(n|\mathbf{x},\tau_1)\notag\\
P(n,\mathbf{x}|\tau_2,\theta)&=&P(\mathbf{x}|\theta)P(n|\mathbf{x},\tau_2)\notag\\
\therefore P(n,\mathbf{x}|\tau_1,\theta)&\propto&P(n,\mathbf{x}|\tau_2,\theta)\notag\\
\end{eqnarray}
$$  
Binomial일때와 Negative Binomial일때를 생각해보면 쉽다. Binomial인 경우 n번의 시도 후에 반드시 실험이 끝나므로 $$P(n|\mathbf{x},\tau)=1$$ 이지만 Negative Binomial인 경우 마지막에 성공해야만 실험이 끝나므로 $$P(n|\mathbf{x},\tau)<1$$ 이다. 즉, stopping rule이 변하면 $$P(n|\mathbf{x},\tau)$$ 만 상수배만큼 변하는 것이다.
likelihood가 비례한다는 것은, stopping rule이 변해도 posterior odds는 변하지 않는다는 것을 의미한다. 즉,  
$$
\begin{eqnarray}
P(\theta)P(n,\mathbf{x}|\tau_1,\theta)&\propto& P(\theta)P(n,\mathbf{x}|\tau_2,\theta)\notag\\
P(\theta)P(n,\mathbf{x}|\tau_1,\theta)&=&c*P(\theta)P(n,\mathbf{x}|\tau_2,\theta)\notag\\
\frac{P(\theta_0)P(n,\mathbf{x}|\tau_1,\theta_0)}{P(\theta_1)P(n,\mathbf{x}|\tau_1,\theta_1)}&=&\frac{c*P(\theta_0)P(n,\mathbf{x}|\tau_2,\theta_0)}{c*P(\theta_1)P(n,\mathbf{x}|\tau_2,\theta_1)}\notag\\
\frac{P(\theta_0|n,\mathbf{x},\tau_1)}{P(\theta_1|n,\mathbf{x},\tau_1)}&=&\frac{P(\theta_0|n,\mathbf{x},\tau_2)}{P(\theta_1|n,\mathbf{x},\tau_2)}\notag\\
\end{eqnarray}
$$

뒤에서 다시 살펴보겠지만, 베이지안 가설검정은 이 posterior odds의 크기를 이용해 가설검정을 하므로, stopping rule에 영향을 받는 항 $$P(n|\mathbf{x},\tau)$$ 은 고려되지 않는다. 따라서, 베이지안 가설 검정은 stopping rule에 immune하게 되는 것이다.
그러면 p-value에서는 왜 $$\tau$$ 가 문제가 되는지 수식을 통해 살펴보자.  
$$
\begin{eqnarray}
p-value &\triangleq& P(\text{current data is observed}\cup\text{more extreme data will be observed}|H_0=true)\notag\\
&=&P(n,\mathbf{x}|\tau,\theta)+\int{P(n,\mathbf{x}_{extreme}|\tau,\theta)d\mathbf{x}_{extreme}}\notag\\
&=&P(\mathbf{x}|\theta)P(n|\mathbf{x},\tau)+\int{P(\mathbf{x}_{extreme}|\theta)P(n|\mathbf{x}_{extreme},\tau)d\mathbf{x}_{extreme}}\notag\\
\end{eqnarray}
$$    
어디가 문제가 되는지 감이 올 것이다. p-value는 비율이 아니라 likelihood $$P(n,\mathbf{x}|\tau,\theta)$$ 의 값을 직접 사용한다. 따라서, $$\tau$$(stopping rule)가 변하면 $$P(n|\mathbf{x},\tau)$$ 가 변하고, 이에 따라 p-value도 변동하게 되는 것이다.

#### 2. p-value의 해석상의 오류

p-value에 대한 대표적인 오해들에 대한 Wikipedia[5]의 정정 내용을 소개한다. p-value는 생각보다 유용한 지표가 아니다.

- **p-value는 귀무가설이 참일 확률도, 대립가설이 거짓일 확률도 아니다**.
$$
\begin{eqnarray}
p-value &\triangleq& P(\text{current data is observed}\cup\text{more extreme data will be observed}|H_0=true)\notag\\ &\ne&P(H_0=true|\text{current data is observed})\notag\\ &=&P(H_1=false|\text{current data is observed})\notag\\
\end{eqnarray}
$$ 식을 보면 명확하지만, **p-value는 그 구조상 가설들 자체에 대한 그 어떠한 확률도 제공할 수 없다.**

- **p-value가 작다고 해서 가설을 설정하고 있는 모수가 해당 모델에서 더 중요하다는 것은 아니다.**<br>둘이 상관이 없는 건 아니지만 p-value가 굉장히 낮다고 해서 중요도가 높은 factor인 것은 아니다. 하지만, 중요도가 높은 factor일수록 낮은 p-value를 얻기 위해 필요한 sample size가 작아지는 경향이 있다.

#### 3. 가설 기각에 실패한다면?

문제는 또 있다. 만약 $$H_0$$이 기각이 안되면 어떻게 할 것인가? $$H_1$$과 $$H_0$$의 자리를 바꾸어서 다시 검정을 하는 것을 생각해볼 수 있다. 그럼 **만약 둘 다 기각이 안 되면 어떻게 할 것인가?**
불가능할 것 같아보일 수 있지만 이 상황도 충분히 가능하다. 다음 예를 살펴보자.  
<br>*검사가 어떤 살인 사건의 용의자 A, 혹은 B를 기소하려고 한다. 범인은 둘 중 한명인 것이 확실하다.*<br>  
빈도주의적 가설 검정을 따른다면, 이 상황에서 B가 범인임을 확정하기 위해서는 $$H_0$$:(용의자 A가 범인)으로 설정하고 다음 증거를 찾아야 한다.  
<br>*“A가 범인이라면(B가 범인이 아니라면) 나올 수 없는 증거”*.<br>  
이 증거를 찾는데 성공하면 A는 범인이 아니므로 B가 범인인 것이다. 그런데, A는 사건 당시 알리바이가 없다. 그러면 A가 범인이라는 가설은 기각할 수 없다.
검사는 이번에는 $$H_0$$:(용의자 B가 범인)으로 설정하고 다음 증거를 모은다.  
<br>*“B가 범인이라면(A가 범인이 아니라면) 나올 수 없는 증거”*<br>  
그런데, B도 사건 당시에 알리바이가 없다. B가 범인이라는 가설을 기각하기에도 충분한 증거가 없는 것이다.
이런 상황에서는 어떻게 해야 할까? 각 가설들이 참일 증거들을 모아 가능성이 더 높은 가설을 채택하면 될 것이다. 그러나 이러한 지극히 상식적인 해답이 있음에도 불구하고 **p-value는 이러한 상황에서 아무런 해답도 주지 못한다.**

#### 4. p-value에 의한 overconfidence 문제

**p-value를 이용한 빈도주의적 가설검정에 대한 일반적인 통념은, 이 가설검정 과정이 굉장히 *보수적이고 안정적인* 검정 과정이라는 것이다.** 이것은 p-value를 이용한 가설검정에서는 1) 일단 주장하고자 하는 가설이 아니라고 가정하고 2) 반대 주장의 근거를 모아보았음에도 불구하고 반대 주장을 도저히 받아들일 수 없을 때만 원래 주장을 받아들이는 것처럼 보이기 때문이다.  
**그러나, 사실은 정반대다.** p-value는 순전히 귀무가설을 기각하는 증거만 보기 때문에, 근거가 굉장히 부족함에도 불구하고 귀무가설의 기각 가능성만 보고 결정을 내리는 경향이 있다. 다시 말해, p-value를 낮추는 데만 집중하다 보면 False Negative의 발생 확률이 낮아지지만, 반대급부로 False positive의 발생 확률이 올라가는 것을 제어할 수가 없다. 실제로 귀무가설의 posterior 확률이 꽤 높은데도 불구하고 p-value가 굉장히 낮게 나오거나 결론이 뒤바뀌는 사례가 다수 보고되었다.[2][5] t-test의 정확성을 시뮬레이션한 한 연구에서는 p-value가 0.05일때 잘못된 결론을 내릴 확률이 *최소한* 30% 이상임이 보고되었다.[11]
위에서 사용한 예제를 재활용해보자. 검사는 먼저 B를 범인으로 의심하여 $$H_0$$:(A가 범인)으로 설정하여 조사를 하던 중, A가 사건 발생 30분 전에 사건 장소에서 1시간 걸리는 회사에서 막 나오는 것을 봤다는 증언을 확보한다. A가 범인이 아닐 가능성이 높아진 것이다. 이를 토대로 검사는 A가 범인이라는 가설을 기각하고, B가 범인일 것이라고 확정짓는다.  
여기까지 보면 별 문제가 없어보이지만, 다음 정보를 추가해보자.  
<br>*“A는 피해자와 원한 관계에 있었다.”*<br>  
이 정보는 A가 범인이라는 사실을 기각하는데 도움이 되는 증거는 아니다. 대신 이 정보는  
<br>*“A가 범인이라면 나올법한 증거”*<br>  
에 해당한다. 여러분이 검사라면 A에 대해 주어진 이 상반된 정보를 고려하여 사실 관계를 좀 더 명확하게 판단한 후에 신중하게 결정을 내릴 것이다. 하지만 빈도주의적 가설 검정은 그렇지 않다. "A가 범인이라면 나올수 없는 증거"에만 기반하여 B를 범인으로 판정한다. 사실은 추가적으로 정보가 필요한 상황인데 말이다.  

### 빈도주의적 가설검정은 우리가 원하는 답을 주지 않는다.

사실 논리적으로 빈도주의적 가설 검정의 문제를 하나하나 따져보지 않아도, 우리의 실제 목표가 무엇인지를 생각해보면 빈도주의적 가설검정이 우리가 원하는 답과는 거리가 멀다는 점을 바로 알 수 있다. 우선 빈도주의 가설검정의 순서를 다시 살펴보자.

1.  증명하고자 하는 가설을 $$H_1$$로, 그에 반대되는 가설을 $$H_0$$으로 놓는다.
2. $$
p-value \triangleq P(\text{current data is observed}\cup\text{more extreme data will be observed}|H_0=true)
$$를 계산한다.
3.  유의 수준 $$\alpha\%$$ 을 정한다.
4.  $$p-value<\alpha$$ 이면 $$H_0$$을 기각한다.
5.  $$H_0$$이 아니므로 자동으로 $$H_1$$가 맞는 가설이 된다.

과정을 쭉 살펴보길 바란다. **“주어진 가설을 가지고 해당 가설에 반대되는 데이터를 관측할 확률”** 을 구한 뒤 각 가설의 실현 확룰이 얼마인지는 한마디도 해주지 않는다. 우리가 정작 원하는 것은 *각 가설이 맞을 확률*이 아닌가? 다음으로 베이지안 가설 검정을 살펴보자.

1.  증명하고자 하는 가설을 $$H_1$$로, 그에 반대되는 가설을 $$H_0$$으로 놓는다.
2.  $$
P(H_1|\text{current data is observed})$$ 와 $$P(H_0|\text{current data is observed})$$ 를 계산한다.
3.  $$
P(H_0|\text{current data is observed})>P(H_1|\text{current data is observed})$$ 이면 $$H_0$$를, 아니면 $$H_1$$을 채택한다. 즉, $$\text{posterior odds}=\frac{p(H_1|\text{current data})}{p(H_0|\text{current data})}=\frac{p(H_1)}{p(H_0)}\frac{p(\text{current data}|H_1)}{p(\text{current data}|H_0)}=\text{prior odds}*\text{Bayes factor}$$ 가 얼마나 큰지를 판정한다.

정확히 우리가 알고자 하는 **“주어진 데이터를 가지고 더 확실한 가설을 채택”** 하는 자연스러운 검정과정이다. 베이지안 통계를 사용하면 posterior $$
P(H_1|\text{current data}), P(H_0|\text{current data})
$$ 를 직접 계산하여 이러한 검정과정을 자연스럽게 따라갈 수 있지만, 빈도주의 통계에서는 어떤 방법을 쓰더라도 가설에 대한 확률을 출력하는 것이 불가능하다. 확률의 정의를 "*사건*의 발생 빈도"로 제한하는 철학적 한계 때문이다.

## 빈도주의에서 베이지안으로
---

### 지금까지 빈도주의 통계학으로도 잘 해왔다?

*   **사용해왔던 모델이 단순하면 그럴 수 있다.** weakly prior를 사용하는 경우 confidence interval과 credible interval이 (거의) 일치하는 경우가 있기는 하다. 대표적으로 빈도주의 측면에서 가우시안 분포만을 사용하여 분석을 했다면, 이는 uniform prior에 가우시안 likelihood를 적용한 것과 같다. 이런 분포들을 분석에 사용했다면 빈도주의 통계학으로도 (수치적으로는) 같은 결과가 나올 수 있지만, 조금만 실제 모델이 변하면 잘못된 결론을 낼 위험성이 있으며, 이러한 오류의 가능성은 결코 낮지 않다.[11]  
* **p-value를 이용한 가설검정 과정은 거의 재앙에 가깝다. 같은 데이터에서 전혀 다른 결론을 낼 수가 있는 굉장히 위험한 procedure이다.** 빈도주의 통계학을 통해 얻은 결과들이 베이지안 분석에서는 부정되는 경우가 많다. 실제로 FDA(미국 식품의약국)는 베이지안 검증법을 권장하고 있으며 일부 medical journal에서는 p-value를 검증 도구로 쓰는 것이 아예 금지되었다.[2][10] 일부 학자들은 빈도주의 통계학을 더이상 가르치지 않는 것만이 잘못된 결과들을 양산해내고 있는 현 상황에 대한 타결책이라고 주장하고 있다[9]. 개인적으로도 **빈도주의적 가설검증을 한 실험의 결과들은 일단 의심해볼 것을 권하고 싶다.**

### 그럼, 베이지안 방법만 써야 하나?

그렇지는 않다. EM 알고리즘, Monte Carlo 방법들, MLE 추정 등 빈도주의 통계학에서 나온 유용한 도구들이 많고, 가설검정에 관한 빈도주의자들의 철학 자체에는(방법론은 문제투성이지만) 나름대로의 장점이 있다. 통계학의 2가지 중요한 metaprinciple들을 살펴보자.

1.  **coherence: 같은 데이터를 사용했다면, 분석 방법이 조금 다르더라도 비슷한 결과가 나와야 한다.**
    * 위에서 살펴보았듯이, 이것은 베이지안 관점만이 가지는 장점이다.
2.  **calibration: 반복된 실험에서 동일한 결과를 복원할 수 있어야 한다.**
    *   이것은 본래 빈도주의 관점만이 가지는 장점이다.(잘 모르겠다면 둘의 철학적 차이에 대해 다시 생각해보길 바란다.) 베이지안 credible interval은 현재 주어진 데이터만 사용하여 만들어지기는 하지만, 모든 데이터를 한번에 소진하여 만든 one-shot 구간이기 때문에 반복된 실험에서의 복원력은 보장되지 않는다.

우리는 일반적으로 두 property가 모두 만족되기를 바란다. 따라서, 한번의 실험으로 바로 베이즈 추론을 하는 것은 바람직한 procedure가 아니라고 주장할 수 있다. 이런 경우에는 베이지안 툴을 사용하여 분석한 후, 빈도주의 방법론처럼 반복된 실험에서 동일한 결과를 복원할 수 있는지 체크하는 방법이 쓰인다. [7] 이것을 Bayesian calibration이라고 부른다.

하지만 크게 보면 빈도주의 통계학은 베이즈 통계학의 special case로 취급할 수 있으며, 베이즈 통계의 유용성은 많은 분야에서 증명되어왔다. 합리적이고 비판적인 지식인으로써 우리는 빈도주의 통계학이 지니는 문제점들을 명확하게 인식하고, 그 도구들을 베이지안 framework와 결합하여 보다 나은 결과를 얻을 수 있도록 해야 할 것이다.

## 참고자료

* * *

[1] Probabilistic Machine Learning, Kevin Murphy(2012), 6.6.3절<br>
[2] Probabilistic Machine Learning, Kevin Murphy(2012), 6.6.2절<br>
[3] Frequentism and Bayesianism III: Confidence, Credibility, and why Frequentism and Science do not Mix [http://jakevdp.github.io/blog/2014/06/12/frequentism-and-bayesianism-3-confidence-credibility/](http://jakevdp.github.io/blog/2014/06/12/frequentism-and-bayesianism-3-confidence-credibility/)<br> *저자는 물리학자인 것으로 보인다.<br>
[4] [https://en.wikipedia.org/wiki/Confidence_interval#Misunderstandings](https://en.wikipedia.org/wiki/Confidence_interval#Misunderstandings)<br>
[5] [https://en.wikipedia.org/wiki/P-value#Misunderstandings](https://en.wikipedia.org/wiki/P-value#Misunderstandings)<br>
[6] P values and Statistical Practice, Andrew Gelman, _Epidemiology_, Volume 24, Number 1, Jan.2013<br>
[7] Michael I. Jordan’s Lecture Note for “Stat260: Bayesian Modeling and Inference”, Lecture Note 11.Confidence Intervals and Hypothesis Testing<br>
[8] Probabilistic Machine Learning, Kevin Murphy(2012), 6.6.4절<br>
[9] It is Time to Stop Teaching Frequentism to Non-statisticians, William M. Briggs(2012) [http://arxiv.org/abs/1201.2590](http://arxiv.org/abs/1201.2590)<br>
[10] http://www.scientificamerican.com/article/scientists-perturbed-by-loss-of-stat-tools-to-sift-research-fudge-from-fact/<br>
[11] http://rsos.royalsocietypublishing.org/content/1/3/140216<br>
[12] Stopping Rules and Their Irrelevance for Bayesian Inference: Online Appendix to "A Practical Soluton to the Pervasive Problems of p-values", to appear in Psychonomic Bulletin and Review, Eric-Jan Wagenmakers
