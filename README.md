# Bug-in-FeynCalc  

*  <summary>Mathematica 11.3</summary>    
```11.3.0 for Microsoft Windows (64-bit) (March 7, 2018)```
*  <summary>FeynCalc 9.2.0</summary> 
  ```9.2.0```
*  <summary>Did you try to reinstall FeynCalc (stable version) using the automatic installer to make sure that you have the latest bugfixes?</summary>    
  ```Yes```
  *  <summary>oneloop calculation "k" is loop monentum, and we set all mass to zero, that means p1.p1=0, p2.p2=0  p1.p2=p1p2  </summary>    
```$LimitTo4 = False;  
wt = FeynAmpDenominator[PropagatorDenominator[Momentum[k, D]], 
   PropagatorDenominator[Momentum[k, D] + Momentum[p1, D]], 
   PropagatorDenominator[
    Momentum[k, D] + Momentum[p1, D] + Momentum[p2, D]]] Pair[
   LorentzIndex[mu, D], Momentum[k, D]] Pair[LorentzIndex[nu, D], 
   Momentum[k, D]]  
worng2 = wt // OneLoopSimplify[#, k] & // OneLoop[k, #] & // 
   PaVeReduce // ChangeDimension[#, D] &
   
   ```

*  <summary>we expect to get the answers </summary> 


When I use TID to do HiggstoGluonGluon oneloop calculation, the result was wrong, and it was same with the calculation that I used Oneloop with oneloopsimplify which was not reconmmand by developer.    
  
Then I set $LimitTo4=True, the result of OneLoop with OneLoopSimplify was True(agree with my derivation) and the result of TID was still wrong.    

I  take apart the amplitude into pieces, and I found the one which cause the problem, that is   

```FeynAmpDenominator[PropagatorDenominator[Momentum[k,D]],PropagatorDenominator[Momentum[k,D]+Momentum[p1,D]],PropagatorDenominator[Momentum[k,D]+Momentum[p1,D]+Momentum[p2,D]]] Pair[LorentzIndex[mu,D],Momentum[k,D]] Pair[LorentzIndex[nu,D],Momentum[k,D]]```
  
in which "k" is loop monentum, and we set all mass to zero, that means p1.p1=0, p2.p2=0.

## four differnt ways

1. $LimitTo4=False (default) , use Oneloop with oneloopsimplify 
2. $LimitTo4=False (default) , use TID  
#### 3. $LimitTo4=True,             use Oneloop with oneloopsimplify 
4. $LimitTo4=True,             use TID

## we found only the thrid way gave the right answers(agreed with my derivation)

