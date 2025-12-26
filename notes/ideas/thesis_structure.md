# Thesis Structure

## Around the subject
**Keywords**
Price process modelling · Price process description · Price discovery · Data-driven modelling

**Problems to be solved** 
	- Systematic overfitting due to the adaptative nature of the markets and the process of researching new models "by hand"

    - New models are super slow to be found, require a lot of human brain and may be hard to implement

    - Market participants don't really like black boxes as risks is usually considered as a direct function of the market

    - Most of the time, the models rely on strong hypothesis that may not be verified in the real world

    - Most of the industry has built its system product by product because of the differences in models, can we unify it ? 

## Potential structures

**Natural Plan**
1. The classical approach : stochastic processes
2. Improving parameters estimation by using data techniques
3. Discarding stochastic models for data learned ones

**Constructivist Plan**
(Model construction by hypothesis additivity : start from purely microstructure (100% true) then add hypothesis about efficient markets and arbitrage (mostly true) then add time series modelling)
1. Market Microstructure, no arbitrage (transactions system)
2. Modelling Price as a function of time (not trivial to go from orderbook to time series)
3. Then, apply data learning

---

## Foreword & Introduction
    - If Markets are efficient => this thesis is pointless. Fortunately they are not, here is why.
    - What is systematic overfitting, why is it a problem, why is it still here ? 
    - Why do we care about giving a description of the price processes ? 
    - There are only two things in operating the market : pricing and execution. Pricing can be deterministic, or an expected value if you assume some randomness. (Example : a portfolio is just a low variance underlying)

--- 

## Thesis Writing
    - This thesis is also about management : do not forget the consequences on management (e.g no more traders but only sales and bot executors ?)
    - Do not forget : Acknowledgements, Declaration on the use of AI
    - References indexation at the bottom of the page
    - APA references by preference
    - Do not forget : check that the thesis answers every point on evaluation table
