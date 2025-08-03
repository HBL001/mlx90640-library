# MLX90640 Library (C++ Wrapper for Melexis Driver)

This repository contains a wrapper around the official Melexis MLX90640 thermal camera driver. It is used by the DuoSight project to interface with the MLX90640 over I2C using a modern C++ I2cDevice abstraction and Linux ioctl calls.

---

## 📦 What This Library Does

- Provides low-level C bindings from Melexis (`MLX90640_API.c`)
- Implements a transport shim (`mlx90640Transport.cpp`) to redirect I2C calls through a C++ object
- Exposes public headers for integration into other C++ applications

Used in:

- `duosight/libduosight` core device abstraction
- `mlx90640-reader` CLI and Qt-based visualization applications

---

## 📁 Structure

```
mlx90640-library/
├── functions/           # Melexis API implementation (MLX90640_API.c)
├── headers/             # Melexis API headers
│   ├── MLX90640_API.h
│   └── MLX90640_I2C_Driver.h
├── mlx90640 driver.pdf # Official datasheet
├── README.md            # You're reading it
```

---

## 🛠️ How To Use as Submodule

To include this library inside another project (e.g. `duosight`):

```bash
git submodule add git@github.com:HBL001/mlx90640-library.git mlx90640-library
git submodule update --init --recursive
```

Make sure your CMakeLists.txt includes:

```cmake
# Include Melexis headers
target_include_directories(my_target PRIVATE
    ${CMAKE_SOURCE_DIR}/mlx90640-library/headers
)

# Link MLX90640_API.c directly or via your own wrapper
set(MELEXIS_SRC
    ${CMAKE_SOURCE_DIR}/mlx90640-library/functions/MLX90640_API.c
)
```

---

## 🔁 How to Update This Submodule

If you forked this repo (as `HBL001/mlx90640-library`) and want to pull in upstream changes:

```bash
cd mlx90640-library
git remote add upstream https://github.com/melexis/mlx90640-library.git
git fetch upstream
git merge upstream/master     # or main, depending on branch name

# Push changes to your fork
git push origin master        # or main
```

---

## 📜 License

This project inherits the license from the upstream Melexis project. Please consult `mlx90640-library/LICENSE` for terms.

(c) 2025 Highland Biosciences Ltd. Fork maintained by Dr Richard Day richard\_day\@highlandbiosciences.com


