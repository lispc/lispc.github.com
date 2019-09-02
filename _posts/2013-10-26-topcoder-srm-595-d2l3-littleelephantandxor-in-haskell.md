---
layout: post
title: "Topcoder SRM 595 D2L3 LittleElephantAndXor in Haskell"
description: ""
category: 
tags: []
---
{% highlight haskell %}
import Data.Char
pl [0,0,0] acc = acc
pl ll acc = 
    pl (map (flip quot 2) ll) $ zipWith ($) (map (\x -> \ls->(mod x 2):ls )ll) acc
    
getNumber :: Int -> Int -> Int -> Integer
getNumber a b c = 
    g aa bb cc l 
        where
            [aa,bb,cc]=pl [a,b,c] [[],[],[]]
            l = length aa
mo n = take (n-1) $ repeat 1
gnr :: [Int]->Integer->Integer
gnr [] acc = acc
gnr (x:xs) acc = gnr xs ((fromIntegral x)+2*acc) 
gn :: [Int]->Integer
gn xs = (gnr xs 0)+1
gnm xs = (gnr xs 0)
g :: [Int]->[Int]->[Int]->Int->Integer
g [] [] [] _ = 1
g (a@(ah:at)) (b@(bh:bt)) (c@(ch:ct)) l = 
        case (ah,bh,ch) of
        (0,0,0) -> g at bt ct ll
        (0,0,1) -> g at bt ml ll
        (0,1,0) -> g at ml ct ll
        (0,1,1) -> if l==1 then 2 else (g at bt ct ll)+((gn at)*(2^ll)) 
        (1,0,_) -> g b a c l
        (1,1,0) -> (gtor ct ll)+(g at bt ct ll) 
        (1,1,1) -> if l==1 then 4 else ((2^ll)^2)+((gn at)*(gn bt))+(goor at ct ll)+(goor bt ct ll)
        where
                ll = l - 1
                ml = mo l
gtor [] _  = 1
gtor (1:t) l = 2*((2^(l-1))^2)+2*(gtor t (l-1))
gtor (0:t) l = 2*(gtor t (l-1)) 
goor [] [] _ = 1
goor b@(bh:bt) c@(ch:ct) l =
    case (bh,ch) of
        (0,0) -> goor bt ct ll
        (0,1) -> (2^ll)*(gn bt)+(goor bt ct ll)
        (1,0) -> (goor bt ct ll)+(gtor ct ll)
        (1,1) -> (2^ll)^2+(goor bt ct ll)+(gtor ct ll)+(2^ll)*(gn bt)
        where ll=l-1
{% endhighlight %}
{% include JB/setup %}
