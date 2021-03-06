# List the header files
set(HEADERS png.h
            pngconf.h
)


# List the source files
set(SRCS png.c
         pngerror.c
         #pnggccrd.c
         pngget.c
         pngmem.c
         pngpread.c
         pngread.c
         pngrio.c
         pngrtran.c
         pngrutil.c
         pngset.c
         pngtrans.c
         #pngvcrd.c
         pngwio.c
         pngwrite.c
         pngwtran.c
         pngwutil.c
)

# List the include paths
xmake_import_search_paths(ZLIB)

# Declaration of the library
xmake_create_static_library(PNG png ${HEADERS} ${SRCS})

if (NOT WIN32)
    xmake_add_to_property(PNG COMPILE_FLAGS "-w")
else()
    xmake_add_to_property(PNG COMPILE_FLAGS "/W0")
    xmake_add_to_list_property(PNG COMPILE_DEFINITIONS "_CRT_SECURE_NO_DEPRECATE")
endif()

xmake_project_link(PNG ZLIB)

if (DEFINED FREEIMAGE_CPP_FLAGS)
    xmake_add_to_list_property(PNG COMPILE_DEFINITIONS "${FREEIMAGE_CPP_FLAGS}")
endif()

set_target_properties(png PROPERTIES FOLDER "LibsExtern/freeimage")

#make variable available for parent scope
get_directory_property(hasParent PARENT_DIRECTORY)
if(hasParent)
	set(GLOBAL_LIBRARIES "${GLOBAL_LIBRARIES};png" PARENT_SCOPE)
endif()	