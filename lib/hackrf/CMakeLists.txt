# Copyright 2012 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Create linkable target
########################################################################

add_library(hackrf STATIC
    hackrf_source_c.cc
    hackrf_sink_c.cc
)

target_include_directories(hackrf
   PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${LIBHACKRF_INCLUDE_DIRS}
)

target_link_libraries(hackrf
   ${LIBHACKRF_LIBRARIES}
)

INCLUDE(CheckFunctionExists)
set(CMAKE_REQUIRED_LIBRARIES ${LIBHACKRF_LIBRARIES})
CHECK_FUNCTION_EXISTS(hackrf_device_list LIBHACKRF_HAVE_DEVICE_LIST)

if(LIBHACKRF_HAVE_DEVICE_LIST)
    message(STATUS "HackRF multiple device support enabled")
    add_definitions(-DLIBHACKRF_HAVE_DEVICE_LIST)
endif(LIBHACKRF_HAVE_DEVICE_LIST)
