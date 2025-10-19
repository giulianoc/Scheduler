
# Copyright (C) Giuliano Catrambone (giuliano.catrambone@catrasoftware.it)

# This program is free software; you can redistribute it and/or 
# modify it under the terms of the GNU General Public License 
# as published by the Free Software Foundation; either 
# version 2 of the License, or (at your option) any later 
# version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

# Commercial use other than under the terms of the GNU General Public
# License is allowed only after express negotiation of conditions
# with the authors.

SET (SOURCES
	Scheduler.cpp
	SchedulerErrors.cpp
	Times.cpp
	Scheduler2.cpp
	Times2.cpp
)

SET (HEADERS
	SchedulerErrors.h
	Scheduler.h
	Times.h
	Scheduler2.h
	Times2.h
)

include_directories("${ERROR_INCLUDE_DIR}")
include_directories("${PTHREAD_INCLUDE_DIR}")
include_directories("${DATETIME_INCLUDE_DIR}")

if(APPLE)
	link_directories("${ERROR_LIB_DIR}")
	link_directories("${PTHREAD_LIB_DIR}")
	link_directories("${DATETIME_LIB_DIR}")
endif()

add_library (Scheduler SHARED ${SOURCES} ${HEADERS})

if(APPLE)
	target_link_libraries(Scheduler PRIVATE Error)
	target_link_libraries(Scheduler PRIVATE PThread)
	target_link_libraries(Scheduler PRIVATE Datetime)
endif()

install (TARGETS Scheduler DESTINATION lib)
install (FILES ${HEADERS} DESTINATION include)

