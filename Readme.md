
# Boost filesystem and iostreams standalone

Boost filesystem and iostreams bundled as embeddable CMake module

Current version: **Boost 1.60**

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
