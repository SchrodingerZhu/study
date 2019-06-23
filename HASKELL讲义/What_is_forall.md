

Let's start with a code example:
```haskell
foob :: forall a b. (b -> b) -> b -> (a -> b) -> Maybe a -> b
foob postProcess onNothin onJust mval =
    postProcess val
    where
        val :: b
        val = maybe onNothin onJust mval
```
This code doesn't compile (syntax error) in plain Haskell 98. It requires an extension to support the forall keyword.

Basically, there are 3 different common uses for the forall keyword (or at least so it seems), and each has its own Haskell extension: `ScopedTypeVariables, RankNTypes/Rank2Types, ExistentialQuantification`.

The code above doesn't get a syntax error with either of those enabled, but only type-checks with ScopedTypeVariables enabled.

## Scoped Type Variables:

Scoped type variables helps one specify types for code inside where clauses. It makes the `b` in `val :: b` the same one as the `b` in `foob :: forall a b. (b -> b) -> b -> (a -> b) -> Maybe a -> b`.

A confusing point: you may hear that when you omit the forall from a type it is actually still implicitly there. This claim is correct, but it refers to the other uses of forall, and not to the ScopedTypeVariables use.

## Rank-N-Types:

Let's start with that `mayb :: b -> (a -> b) -> Maybe a -> b` is equivalent to `mayb :: forall a b. b -> (a -> b) -> Maybe a -> b`, except for when `ScopedTypeVariables` is enabled.

This means that it works for every a and b.

Let's say you want to do something like this.
```haskell
ghci> let putInList x = [x]
ghci> liftTup putInList (5, "Blah")
([5], ["Blah"])
```
What must be the type of this liftTup? It's `liftTup :: (forall x. x -> f x) -> (a, b) -> (f a, f b)`. To see why, let's try to code it:
```haskell
ghci> let liftTup liftFunc (a, b) = (liftFunc a, liftFunc b)
ghci> liftTup (\x -> [x]) (5, "Hello")
    No instance for (Num [Char])
    ...
ghci> -- huh?
ghci> :t liftTup
liftTup :: (t -> t1) -> (t, t) -> (t1, t1)
```
"Hmm.. why does GHC infer that the tuple must contain two of the same type? Let's tell it they don't have to be"
```haskell
-- test.hs
liftTup :: (x -> f x) -> (a, b) -> (f a, f b)
liftTup liftFunc (t, v) = (liftFunc t, liftFunc v)

ghci> :l test.hs
    Couldnt match expected type 'x' against inferred type 'b'
    ...
```
Hmm. so here GHC doesn't let us apply liftFunc on v because v :: b and liftFunc wants an x. We really want our function to get a function that accepts any possible x!
```haskell
{-# LANGUAGE RankNTypes #-}
liftTup :: (forall x. x -> f x) -> (a, b) -> (f a, f b)
liftTup liftFunc (t, v) = (liftFunc t, liftFunc v)
```
So it's not liftTup that works for all x, it's the function that it gets that does.

## Existential Quantification:

Let's use an example:
```haskell
-- test.hs
{-# LANGUAGE ExistentialQuantification #-}
data EQList = forall a. EQList [a]
eqListLen :: EQList -> Int
eqListLen (EQList x) = length x

ghci> :l test.hs
ghci> eqListLen $ EQList ["Hello", "World"]
2
```
How is that different from Rank-N-Types?
```haskell
ghci> :set -XRankNTypes
ghci> length (["Hello", "World"] :: forall a. [a])
    Couldnt match expected type 'a' against inferred type '[Char]'
    ...
```
With Rank-N-Types, forall a meant that your expression must fit all possible as. For example:
```haskell
ghci> length ([] :: forall a. [a])
0
```
An empty list does work as a list of any type.

So with Existential-Quantification, foralls in data definitions mean that, the value contained can be of any suitable type, not that it must be of all suitable types.
