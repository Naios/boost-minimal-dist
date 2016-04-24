
# Boost filesystem and iostreams standalone

Boost filesystem and iostreams bundled and other core boost libraries as embeddable CMake module

Current boost version: **Boost 1.60**

Contains:

* boost::filesystem
* boost::iostreams
* boost::

*****

Extracted with the bcp tool:

`bcp filesystem iostreams LOCATION`
*****

Easiest way to embed the minimal distribution in your project as git submodule using CMake:

Shell:
```sh
git submodule add https://github.com/Naios/boost-minimal-dist.git
```

CMake:
```cmake
add_subdirectory(boost-minimal-dist)

# Makes boost::filesystem and boost::iostreams available for your project
target_link_libraries(YOUR_PROJECT boost-minimal-dist)
```
