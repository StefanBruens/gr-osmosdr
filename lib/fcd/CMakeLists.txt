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

add_library(fcd OBJECT
    fcd_source_c.cc
)

target_include_directories(fcd
   PRIVATE
   ${CMAKE_CURRENT_SOURCE_DIR})

if(ENABLE_FCD)
target_link_libraries(fcd ${GNURADIO_FCD_LIBRARIES})
target_include_directories(fcd PRIVATE ${GNURADIO_FCD_INCLUDE_DIRS})
endif(ENABLE_FCD)

if(ENABLE_FCDPP)
target_link_libraries(fcd ${GNURADIO_FCDPP_LIBRARIES})
target_include_directories(fcd PRIVATE ${GNURADIO_FCDPP_INCLUDE_DIRS})
endif(ENABLE_FCDPP)
