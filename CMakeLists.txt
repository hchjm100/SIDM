cmake_minimum_required(VERSION 3.30)
project(SIDM)

set(CMAKE_CXX_STANDARD 14)

# 1) Find MPI for C
find_package(MPI REQUIRED C)

# 2) Find GSL
find_package(GSL REQUIRED)

include_directories(codeSIDM3)
include_directories(input)

add_executable(SIDM
        codeSIDM3/accel.c
        codeSIDM3/allocate.c
        codeSIDM3/allvars.c
        codeSIDM3/allvars.h
        codeSIDM3/begrun.c
        codeSIDM3/check.C
        codeSIDM3/density.c
        codeSIDM3/domain.c
        codeSIDM3/doscatt.c
        codeSIDM3/driftfac.c
        codeSIDM3/endrun.c
        codeSIDM3/forcetree.c
        codeSIDM3/global.c
        codeSIDM3/gravtree.c
        codeSIDM3/gravtree_forcetest.c
        codeSIDM3/hydra.c
        codeSIDM3/init.c
        codeSIDM3/io.c
        codeSIDM3/longrange.c
        codeSIDM3/main.c
        codeSIDM3/ngb.c
        codeSIDM3/ngb_sidm.c
        codeSIDM3/peano.c
        codeSIDM3/pm_nonperiodic.c
        codeSIDM3/pm_periodic.c
        codeSIDM3/potential.c
        codeSIDM3/predict.c
        codeSIDM3/proto.h
        codeSIDM3/read_ic.c
        codeSIDM3/restart.c
        codeSIDM3/run.c
        codeSIDM3/sidm.c
        codeSIDM3/system.c
        codeSIDM3/tags.h
        codeSIDM3/timestep.c
        input/definitions.h
        input/functions.c
        input/functions.h
        input/io.c
        input/io.h
        input/routines.c
        input/routines.h
        input/spheric.c)

# Link your target with MPI (C interface) and GSL libraries
target_link_libraries(
        SIDM
        PRIVATE
        MPI::MPI_C         # From find_package(MPI ...)
        GSL::gsl           # From find_package(GSL ...)
        GSL::gslcblas      # GSL's CBLAS component
)