---
layout: post
title: "How to do LRU cache in Haskell"
description: ""
category: 
tags: []
---
<pre><code>import qualified Data.Map as M
import qualified Data.PQueue.Min as PQ
fib 0 = 1
fib 1 = 1 
fib n = (fib (n-1))+(fib(n-2))
maxsize = 1000 
type FKey = Int 
type FVal = Int
type MyF = FKey->FVal
type TimeStamp = Int
type Cache = (M.Map FKey (FVal,TimeStamp), M.Map TimeStamp FKey,TimeStamp) 
cacheWithLimitSpace f (m,q,lastt) k =
    case M.lookup k m of
        Just (r,oldt) -> --(((M.insert k (r,(t+1)) m),q),r)
            let newt = lastt+1 in
            let newm = M.insert k (r,newt) m in
            let newq = M.insert newt k (M.delete oldt q) in
            ((newm,newq,newt),r)
        Nothing -> 
            let r = f k in
            if (M.size m) &lt; maxsize
                then 
                    let newt = lastt+1 in
                    let newm = M.insert k (r,newt) m in--),q,t+1),r)
                    let newq = M.insert newt k q in
                    ((newm,newq,newt),r)
                else 
                    let newt = lastt+1 in
                    let ((_,invalidKey),q') = M.deleteFindMin q in
                    let newm = M.insert k (r,newt) (M.delete invalidKey m) in
                    let newq = M.insert newt k q' in
                    ((newm,newq,newt),r)
tint=35
main = do
    print $ fib tint
    print $ fib tint
    let (c,r1) = cacheWithLimitSpace fib (M.empty, M.empty, 0) tint
    print r1
    let (_,r2) = cacheWithLimitSpace fib c tint
    print r2
</code></pre>

{% include JB/setup %}
