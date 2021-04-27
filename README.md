# CARPData.jl

This package reads `.dat` data files in a custom format for Capacitated Arc Routing Problem (CARP) instances and returns `Data` type:

```julia
struct Data
    name      ::String         # Instance name
    
    capacity  ::Int64          # Vehicles' capacity
    vehicles  ::Int64          # Number of vehicles
    
    vertices  ::Vector{Vertex} # List with all vertices
    edges     ::Vector{Edge}   # List with all edges (required or not)
    requireds ::Vector{Edge}   # List with required edges
    
    lb        ::Int64          # Known lower bound
    ub        ::Int64          # Known upper bound
end
```

where `Vertex` type:

```julia
struct Vertex
    id        ::Int64          # Sequential id, starting with 1
    
    edges     ::Vector{Edge}   # List with all incident edges (required or not)
    requireds ::Vector{Edge}   # List with required incident edges
end
```

and where `Edge` type:

```julia
struct Edge
    id        ::Int64          # Sequential id, starting with 1

    from      ::Vertex         # First vertex
    to        ::Vertex         # Second vertex
    
    cost      ::Int64          # Edge cost
    demand    ::Int64          # Edge demand (zero for depot)
end
```

Graph is undirected and depot is always vertex 1.

To install:
```julia
] add https://github.com/rafaelmartinelli/CARPData.jl
```

All classical CARP instances in the literature are preloaded:

- `kshs`: Kiuchi M, Shinano Y, Hirabayashi R, Saruwatari Y. An Exact Algorithm for the Capacitated Arc Routing Problem Using Parallel Branch and Bound Method. In: Abstracts of the 1995 Spring National Conference of the Operational Research Society of Japan. 1995, p. 28-9. In Japanese. (no link, for obvious reasons... 🙂)
- `gdb`: Golden BL, DeArmon JS, Baker EK. Computational Experiments with Algorithms for a Class of Routing Problems. Computers & Operations Research 1983;10(1):47-59. ([link](https://doi.org/10.1016/0305-0548(83)90026-6))
- `val` (or `bccm`): Benavent E, Campos V, Corberan A, Mota E. The Capacitated Arc Routing Problem: Lower Bounds. Networks 1992;22:669-90. ([link](https://doi.org/10.1002/net.3230220706))
- `egl`: Li LYO, Eglese RW. An Interactive Algorithm for Vehicle Routeing for Winter-Gritting. Journal of the Operational Research Society 1996;47:217-28. ([link](https://doi.org/10.2307/2584343))
- `beullens`: Beullens P, Muyldermans L, Cattrysse D, Oudheusden DV. A Guided Local Search Heuristic for the Capacitated Arc Routing Problem. European Journal of Operational Research 2003;147(3):629-43. ([link](https://doi.org/10.1016/S0377-2217(02)00334-X))
- `egl-large`: Brandão J, Eglese R. A Deterministic Tabu Search Algorithm for the Capacitated Arc Routing Problem. Computers & Operations Research 2008;35:1112-26. ([link](https://doi.org/10.1016/j.cor.2006.07.007))

See the [full list](https://github.com/rafaelmartinelli/CARPData.jl/tree/main/data).
There are some other instances (groups A and B), but I could not find their origin (if you know, please send me a message).

For example, to load `kshs1.dat`, you can do:
```julia
tsp = load(:kshs1)
```

Known issues:
- Instances with '-' do not load. For example: egl-s1-A.dat.

Related links:
- https://www.uv.es/belengue/carp.html
- http://dimacs.rutgers.edu/programs/challenge/vrp/carp/

For custom CARP files, you must use my custom instance format. Check `readme.txt` in the data directory for instructions.
