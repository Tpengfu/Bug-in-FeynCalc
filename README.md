# Bug-in-FeynCalc
When I use TID to do HiggstoGluonGluon oneloop calculation, the result was wrong, and it was same with the calculation that I used Oneloop with oneloopsimplify which was not reconmmand by developer.    
  
Then I set $LimitTo4=True, the result of OneLoop with OneLoopSimplify was True(agree with my derivation) and the result of TID was still wrong.    

I  take apart the amplitude into pieces, and I found the one  which cause the problem, that is   

FeynAmpDenominator[PropagatorDenominator[Momentum[k,D]],PropagatorDenominator[Momentum[k,D]+Momentum[p1,D]],PropagatorDenominator[Momentum[k,D]+Momentum[p1,D]+Momentum[p2,D]]] Pair[LorentzIndex[mu,D],Momentum[k,D]] Pair[LorentzIndex[nu,D],Momentum[k,D]]   
  
in which "k" is loop monentum, and we set all mass to zero, that means p1.p1=0, p2.p2=0.

