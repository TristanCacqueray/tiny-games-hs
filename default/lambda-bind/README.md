# lambda-bind

The Haskell logo 3d render.

## Playing

- Slow version: `runhaskell lambda-bind.hs`
- Fast version: `ghc -O2 lambda-bind.hs && ./lambda-bind`
- Stack script: `stack script --resolver lts-20 --optimize lambda-bind.hs`

## Documentation

Here is the less-minified version with type annotations:

```haskell
#!/usr/bin/env -S stack script --resolver lts-20 --optimize
-- | lambda-bind expanded
-- Copyright 2023, Tristan de Cacqueray
-- SPDX-License-Identifier: CC-BY-4.0

import Control.Concurrent;import System.Posix.Internals;
w=100;q=0.4;n=min;c=cos;s=sin;
p=[(x/w*2-1,(y/20*2-1)*0.2)|y<-[0..20],x<-[0..w+1]];
main=go 0
-- main=go 0
go n= do
  puts $ "\ESCc" <> (u (n/6)<$>p)
  threadDelay 100000
  go (n+1)
u _(1.02,_)='\n'
u t(x,y)=m t 0(10*x,10*y,-5)
t=max 0;o=True
b h w(x,y,z)=sqrt(t(abs x-w)**2+t(abs y-h)**2+t(abs z-q)**2)

h :: (Float, Float, Float)->Float
h p@(x,y,z)=let
 -- >
 a=b 5q
 l=(x+3,y,z)
 i|y>=0=a(r(-1)l)|o=9
 j|y <0=a(r 1l)|o=9
 -- \
 k=a(r 1p)
 -- ,
 c|y>0=a(r(-1)p)|o=9

 -- mask
 m=b 5 2 (r 1 (x-6,y,z))
 -- lines
 g s=b 6 0.2 (r(pi/2)(x-1,y+s*q,z))
 e=max m (n (g 1) (g (-1)))
 in n(n i j)(n e(n k c))

r t (x,y,z)=(x*c t - y*s t, x*s t + y*c t, z);

m _ 20 _=' '
m t n(x,y,z)=let
 a=x*c(t)-z*s t
 b=x*s t+z*c t
 d=h(a,y,b)
 nz=h(a,y,b+q)-h(a,y,b-q)
 ny=h(a,y+q,b)-h(a,y-q,b)
 g|nz<0='o'|ny<0='>'|o='.'
 color|d<0.01=g|o=m t(n+1)(x,y,z+d)
 in color
```
