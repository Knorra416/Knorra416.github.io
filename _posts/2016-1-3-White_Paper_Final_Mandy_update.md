---
layout: default
title: Smarter SEM Bidding Optimizing Paid Search Through Dominant Game Theory Strategies
author: Fred Askham, Mike Broom, Alex Knorr, Jeff van Geete
status: publish
published: true
output: 
  pdf_document:
  latex_engine: xelatex
mainfont: Times New Roman
fontsize: 12pt
header-includes:
    - \usepackage{fancyhdr}
---
 
**Executive Summary**
  
   The Internet Advertising Bureau (IAB) reported that paid search makes up $29.2 billion of digital marketing industry's $60 billion in annual revenue. Such a large, profitable, and efficient channel rightly deserves the attention of every marketing firm. However, many Search Engine Marketing (SEM) programs are run without quantitative optimization systems.  This is because most of market solutions for SEM bid optimization are technically complicated are capital-intensive investments.  
 
   To solve for this, a new SEM bid optimization system was developed by digital marketing agency, IMM, that is as effective as many available optimization systems, and utilizes current technology stacks in such a way that it can be made accessible to even small self-service marketing operations. 
 
   The system works by utilizing Nash Equilibrium's game theory: the game is solved with a single dominant strategy that produces the best outcome.  This allows SEM brands and agents to identify and to optimize to keyword value with impressive results. Early experiments conducted by the developer, IMM, have shown the system's efficacy with results showing increases in client sales of **12.68%**, increases in click volumes of **18.83%**, and an overall reduction in cost per conversion of **4.30%**.
 
**Introduction**
  
   Third party tools provide many ways to optimize SEM bids, but the industry has not adopted a consistent methodology for optimization. Google Adwords, for example, provides an estimated bid to reduce impressions lost to position. While this optimization makes sense for increasing volume, it does not take into account how the value of a bid might change based on individual firms' revenues and costs. According to Digital Marketing Depot, the major differentiator between SEM bidding optimization systems at this point is the frequency with which the system will alter a campaign's bids (Digital Marketing Depot, 2015). This leaves significant room in the market for an SEM bid optimization system that addresses the individual considerations of a client's/brand's business. IMM developed a wholly different and unique approach to SEM optimization that utilizes the well-established economic principals of game theory. This paper seeks to explain the methodology and value of this new system, developed by IMM, for optimizing SEM bids with the goal of driving maximum value for a client. 
 
**Background**
  
   In second-price auctions (SPA) an Nash Equilibrium (NE) with a dominant strategy exists. This means that all players in the game will chose one strategy no matter how many iterations occur (Papayoanou, 2010). SEM bids take place through a second-price auction system and in a game theory setting these auction types have a single, NE strategy: to bid one's own value (Garrat, Walker, & Wooders, 2011).  In an application to SEM bidding this implies that if a bid is placed at the clients measured value for a keyword then their SEM media buying will be fully optimized. A winning bid will pay the second price, and thus be profitable for the client, a losing bid would be for inventory above their maximum value and attempting to win at this level would result in negative profit. This NE strategy drives the this newly developed optimization system.    
 
**IMM's Solution**
  
   IMM's solution provides optimal bid amounts at the keyword level. The system utilizes historical keyword data to determine a client's value for each keyword which is then used to optimize bids.   
 
   When IMM implemented an experiment of this system for a large client, sales from the campaign increased by 12.68%, clicks increased by 18.83%, and cost per conversion decreased by 4.3%. (The associated total media cost of running the campaign increased by 7.28%). This optimization process can be repeated at any cadence with updated information making it scalable to any level of service.
 
![plot of chunk unnamed-chunk-1](/figures/unnamed-chunk-1-1.png)
 
   These results are across Broad, Exact, and Phrase keyword types. The experiment was conducted for two weeks and was run in Google Adwords using a 50% split (a.k.a an "A/B Test") with our current keyword bids. The optimized bids are based on standard data available from platforms such as Google Adwords and Bing. The bid suggestions provided by this model can not only set the benchmark of keyword bid amounts, but can also be used in coordination with an existing bid platform to analyze the effectiveness of bids relative to true agency value. 
 
**Conclusion**
  
   Current market offerings for bid optimization do not account for agency and client revenue-per-sale. This revenue is the maximum value a firm can expect to receive for a conversion, and thus an NE-based approach to bid optimization includes these to ensure bids maximize value to agency and client. IMM's solution increased conversions by 12.68% and decreased cost per conversion by 4.3%. Bid optimization based on NE can be used as a stand-alone system, or in tandem with other systems to adjust current bidding methods to account for maximum value. The robust theory behind the system coupled with our initial results speak for themselves on the efficacy of our solution.
 
**References**
  
Digital Marketing Depot. (2015). Enterprise Paid Media Campaign Management Platforms 2015: A Marketer's Guide. Third Door Media Inc.
 
Garrat, R., Walker, M., & Wooders, J. (2011). Behavior in second-price auctions by highly experienced eBay buyers and sellers. Economic Science Association, 44-57. 
 
Papayoanou, P. (2010). Game Theory for Business: A Primer in Strategic Gaming. Probabilistic Publishing.
 
 
 
 
