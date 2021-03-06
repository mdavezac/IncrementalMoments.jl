For scalars and small arrays,
[joshday/OnlineStats.jl](https://github.com/joshday/OnlineStats.jl) is likely a better
alternative.

[![Build Status](https://travis-ci.org/CryptaLabs/IncrementalMoments.jl.svg?branch=master)](https://travis-ci.org/CryptaLabs/IncrementalMoments.jl)
[![Coverage
Status](https://coveralls.io/repos/CryptaLabs/IncrementalMoments.jl/badge.svg)](https://coveralls.io/r/Cryptalabs/IncrementalMoments.jl)

# IncrementalMoments

Implements formulae to compute moments (Mₙ = 1/n Σ(m_i - μ)ⁿ) incrementally. These
formulae are taken from

   ___Simpler Online Updates for Arbitrary-Order Central Moments___
   Xiangrui Meng
   [arXiv](https://arxiv.org/abs/1510.04923) Oct 2015


The moments can be computed on scalars or arrays:

```julia
julia> using IncrementalMoments

julia> scalar = IncrementalMoment(Float64, 3)
IncrementalMoments.ScalarIncrementalMoment{Float64}([0.0,0.0,0.0],0)

julia> array = IncrementalMoment(Float64, (10,), 3)
IncrementalMoments.ArrayIncrementalMoment{Array{Float64,2}}([0.0 0.0 0.0; 0.0 0.0 0.0; … ; 0.0 0.0 0.0; 0.0 0.0 0.0],0)
```

The first argument is the underlying type that will hold the moments. The last argument is
the maximum order of the moments. In the case of arrays, the middle argument is the
dimension of arrays in the input stream.

Moments are updated with

```julia
julia> update!(scalar, 2.5)
IncrementalMoments.ScalarIncrementalMoment{Float64}([2.5,0.0,0.0],1)

julia> update!(array, 2.5 * ones(10))
IncrementalMoments.ArrayIncrementalMoment{Array{Float64,2}}([2.5 0.0 0.0; 2.5 0.0 0.0; … ; 2.5 0.0 0.0; 2.5 0.0 0.0],1)
```

Finally, specific moments can be extracted by applying `Base.mean`, `Base.var`, and
`StatsBase.moment` to the incremental moment objects.
