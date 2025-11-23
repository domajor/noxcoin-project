# Copyright (c) 2014-2024, The NoxCoin Project
# 
# All rights reserved.
# 
# Redistribution and use in source and binary forms, with or without modification, are
# permitted provided that the following conditions are met:
# 
# 1. Redistributions of source code must retain the above copyright notice, this list of
#    conditions and the following disclaimer.
# 
# 2. Redistributions in binary form must reproduce the above copyright notice, this list
#    of conditions and the following disclaimer in the documentation and/or other
#    materials provided with the distribution.
# 
# 3. Neither the name of the copyright holder nor the names of its contributors may be
#    used to endorse or promote products derived from this software without specific
#    prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY
# EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
# MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL
# THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
# SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
# PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
# INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF
# THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# Parts of this file are originally copyright (c) 2012-2013 The Cryptonote developers

# -------------------------------------------------------------------
# MiniUPnP
# -------------------------------------------------------------------
set(MINIUPNPC_INCLUDE_DIRS /usr/include/miniupnpc)
set(MINIUPNPC_LIBRARIES /usr/lib/x86_64-linux-gnu/libminiupnpc.so)

# Apply include dirs and library globally
include_directories(${MINIUPNPC_INCLUDE_DIRS})
link_libraries(${MINIUPNPC_LIBRARIES})

message(STATUS "Using system-installed MiniUPnP from ${MINIUPNPC_INCLUDE_DIRS} and ${MINIUPNPC_LIBRARIES}")

# -------------------------------------------------------------------
# Unbound (DNS Resolver)
# -------------------------------------------------------------------
find_package(Unbound REQUIRED)

if(NOT UNBOUND_INCLUDE_DIR OR NOT UNBOUND_LIBRARIES)
    message(FATAL_ERROR "Could not find libunbound. Install libunbound-dev.")
endif()

# Only attach to obj_rpc if it exists
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
