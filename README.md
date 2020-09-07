LibGEOS.jl
==========
[![Build Status](https://travis-ci.org/JuliaGeo/LibGEOS.jl.svg?branch=master)](https://travis-ci.org/JuliaGeo/LibGEOS.jl)
[![Build Status](https://ci.appveyor.com/api/projects/status/github/JuliaGeo/LibGEOS.jl?svg=true&branch=master)](https://ci.appveyor.com/project/JuliaGeo/LibGEOS-jl/branch/master)
[![Coverage Status](https://coveralls.io/repos/github/JuliaGeo/LibGEOS.jl/badge.svg)](https://coveralls.io/github/JuliaGeo/LibGEOS.jl)

# WARNING

This version relies on having [GMT](https://github.com/GenericMappingTools/GMT.jl) installed and will use it to find the system libraries
needed for this package. This has the advantage of and saving you disk space. However, being a fork it may risk to go out of sync with time.

It would be nice if this solution could be integrated in the officially registered package as an install option but atm I don't know
how to implement that.

See also same solution for:

- [GDAL](https://github.com/joa-quim/GDAL.jl)
- [NetCDF](https://github.com/joa-quim/NetCDF.jl)
- [Proj4](https://github.com/joa-quim/Proj4.jl)

LibGEOS is a package for manipulation and analysis of planar geometric objects, based on the libraries [GEOS](https://trac.osgeo.org/geos/) (the engine of PostGIS) and JTS (from which GEOS is ported). This package wraps the [GEOS C API](https://geos.osgeo.org/doxygen/geos__c_8h_source.html).

Among other things, it allows you to parse [Well-known Text (WKT)](https://en.wikipedia.org/wiki/Well-known_text)

```julia
p1 = readgeom("POLYGON((0 0,1 0,1 1,0 0))")
p2 = readgeom("POLYGON((0 0,1 0,1 1,0 1,0 0))")
p3 = readgeom("POLYGON((2 0,3 0,3 1,2 1,2 0))")
```
![Example 1](examples/example1.png)

Add a buffer around them
```julia
g1 = buffer(p1, 0.5)
g2 = buffer(p2, 0.5)
g3 = buffer(p3, 0.5)
```
![Example 2](examples/example2.png)

and take the union of different geometries
```julia
polygon = LibGEOS.union(g1, g3)
```
![Example 3](examples/example3.png)

GEOS functionality is extensive, so coverage is incomplete, but the basic functionality for working with geospatial data is already available. I'm learning as I go along, so documentation is lacking, but if you're interested, you can have a look at the examples in the `examples/` folder, or the tests in `test/test_geo_interface.jl` and `test/test_geos_operations.jl`.

Installation
------------
1. At the Julia prompt, run 
  ```julia
  pkg> add https://github.com/joa-quim/LibGEOS.jl
  ```

2. Test that `LibGEOS` works by runnning
  ```julia
  pkg> test LibGEOS
  ```
