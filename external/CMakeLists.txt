# Copyright (c) 2014-2024, The Noxcoin Project
# All rights reserved.
# Parts of this file are originally copyright (c) 2012-2013 The Cryptonote developers

cmake_minimum_required(VERSION 3.10)
project(NoxcoinExternals)

# -------------------------------------------------------------------
# MiniUPnP
# -------------------------------------------------------------------
# Try to use system-installed MiniUPnP
find_path(MINIUPNPC_INCLUDE_DIR miniupnpc/miniupnpc.h)
find_library(MINIUPNPC_LIBRARY NAMES miniupnpc)

if(MINIUPNPC_INCLUDE_DIR AND MINIUPNPC_LIBRARY)
    message(STATUS "Using system-installed MiniUPnP from ${MINIUPNPC_INCLUDE_DIR} and ${MINIUPNPC_LIBRARY}")
    include_directories(${MINIUPNPC_INCLUDE_DIR})
    link_libraries(${MINIUPNPC_LIBRARY})
else()
    # Fallback to internal submodule
    message(STATUS "Using internal MiniUPnP submodule")
    add_subdirectory(miniupnp)
endif()

# -------------------------------------------------------------------
# Unbound (DNS Resolver)
# -------------------------------------------------------------------
find_package(Unbound QUIET)

if(NOT UNBOUND_INCLUDE_DIR OR NOT UNBOUND_LIBRARIES)
    message(FATAL_ERROR "Could not find libunbound. Install libunbound-dev.")
endif()

# Attach Unbound only if obj_rpc target exists
if(TARGET obj_rpc)
    target_include_directories(obj_rpc PUBLIC ${UNBOUND_INCLUDE_DIR})
    target_link_libraries(obj_rpc PUBLIC ${UNBOUND_LIBRARIES})
endif()

# -------------------------------------------------------------------
# Other external libraries
# -------------------------------------------------------------------
add_subdirectory(db_drivers)
add_subdirectory(easylogging++)
add_subdirectory(qrcodegen)
add_subdirectory(randomx EXCLUDE_FROM_ALL)
add_subdirectory(supercop EXCLUDE_FROM_ALL)  # Ensure submodule is included

# -------------------------------------------------------------------
# Optional: Helper to show all external libs
# -------------------------------------------------------------------
message(STATUS "MiniUPnP: ${MINIUPNPC_INCLUDE_DIR} / ${MINIUPNPC_LIBRARY}")
message(STATUS "Unbound: ${UNBOUND_INCLUDE_DIR} / ${UNBOUND_LIBRARIES}")
