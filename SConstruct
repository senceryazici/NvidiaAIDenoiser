import os
PLATFORM = Platform()
DEBUG = ARGUMENTS.get("debug", 0)

CUDA_INCLUDE_PATH = "/usr/local/cuda/include"

ENV = Environment(CPPPATH = ['.', "./contrib/optix/include", "/usr/include", CUDA_INCLUDE_PATH
],
                  CCFLAGS="-std=c++11")

# Used for debbugging
if int(DEBUG):
    ENV.Append(CCFLAGS=' -ggdb3')

SOURCES = Glob("src/*.cpp")

LIBPATH = []
LIBPATH.append("./contrib/optix/lib64")

LIBS = []
LIBS.append("optix")
LIBS.append("OpenImageIO")

LINKFLAGS = []
LINKFLAGS.append("-Wl,-rpath=.")

program = ENV.Program(target="bin/Denoiser", source=SOURCES, LIBPATH=LIBPATH, LIBS=LIBS, LINKFLAGS=LINKFLAGS)
