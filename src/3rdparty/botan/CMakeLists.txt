set(BOTAN_VERSION_MAJOR 1)
set(BOTAN_VERSION_MINOR 10)
set(BOTAN_VERSION_PATCH 2)
set(BOTAN_VERSION_STRING ${BOTAN_VERSION_MAJOR}.${BOTAN_VERSION_MINOR}.${BOTAN_VERSION_PATCH})

set(BotanLib_hdr botan.h)  #HEADERS += $$PWD/botan.h

#INCLUDEPATH *= $$PWD/..

# if(USE_SYSTEM_BOTAN)                     # equals(USE_SYSTEM_BOTAN, 1) {
#     add_definitions(-Duse_system_botan)  #     DEFINES += use_system_botan
#     find_package(PkgConfig)              #     CONFIG += link_pkgconfig
#     pkg_search_module(BOTAN botan-1.10)  #     PKGCONFIG += botan-1.10
# else(USE_SYSTEM_BOTAN)                   # } else {
    set(BotanLib_src botan.cpp)  # SOURCES += $$PWD/botan.cpp

    add_library(botan SHARED
        ${BotanLib_src}
        ${BotanLib_hdr})
    target_link_libraries(botan Qt5::Core)
    set_target_properties(botan PROPERTIES CLEAN_DIRECT_OUTPUT 1)
    set_target_properties(botan PROPERTIES VERSION ${BOTAN_VERSION_STRING} SOVERSION ${BOTAN_VERSION_MAJOR})
    target_include_directories(botan PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

    add_library(botan_static STATIC
        ${BotanLib_src}
        ${BotanLib_hdr})
    target_link_libraries(botan_static Qt5::Core)
    set_target_properties(botan_static PROPERTIES OUTPUT_NAME "botan")
    set_target_properties(botan_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)
    target_include_directories(botan_static PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

    #CONFIG += exceptions

    #DEPENDPATH += .

    add_definitions(-DBOTAN_DLL=)        # DEFINES += BOTAN_DLL=

    #unix:DEFINES += BOTAN_TARGET_OS_HAS_GETTIMEOFDAY BOTAN_HAS_ALLOC_MMAP \
    #BOTAN_HAS_ENTROPY_SRC_DEV_RANDOM BOTAN_HAS_ENTROPY_SRC_EGD BOTAN_HAS_ENTROPY_SRC_FTW \
    #BOTAN_HAS_ENTROPY_SRC_UNIX BOTAN_HAS_MUTEX_PTHREAD BOTAN_HAS_PIPE_UNIXFD_IO
    if(UNIX)
        add_definitions(-DBOTAN_TARGET_OS_HAS_GETTIMEOFDAY
                        -DBOTAN_HAS_ALLOC_MMAP
                        -DBOTAN_HAS_ENTROPY_SRC_DEV_RANDOM
                        -DBOTAN_HAS_ENTROPY_SRC_EGD
                        -DBOTAN_HAS_ENTROPY_SRC_FTW
                        -DBOTAN_HAS_ENTROPY_SRC_UNIX
                        -DBOTAN_HAS_MUTEX_PTHREAD
                        -DBOTAN_HAS_PIPE_UNIXFD_IO)

        #unix:*-g++* {
        if(CMAKE_COMPILER_IS_GNUCXX)
          #QMAKE_CFLAGS += -fPIC -fpermissive -finline-functions -Wno-long-long
          set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC -fpermissive -finline-functions -Wno-long-long")
          #QMAKE_CXXFLAGS += -fPIC -fpermissive -finline-functions -Wno-long-long
          set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -fpermissive -finline-functions -Wno-long-long")
        #}
        endif(CMAKE_COMPILER_IS_GNUCXX)
    endif(UNIX)

    #*linux*:DEFINES += BOTAN_TARGET_OS_IS_LINUX BOTAN_TARGET_OS_HAS_CLOCK_GETTIME \
    #BOTAN_TARGET_OS_HAS_DLOPEN BOTAN_TARGET_OS_HAS_GMTIME_R BOTAN_TARGET_OS_HAS_POSIX_MLOCK \
    #BOTAN_HAS_DYNAMICALLY_LOADED_ENGINE BOTAN_HAS_DYNAMIC_LOADER

    #macx:DEFINES += BOTAN_TARGET_OS_IS_DARWIN
    if(APPLE)
        add_definitions(-DBOTAN_TARGET_OS_IS_DARWIN)
    endif(APPLE)

    #*g++*:DEFINES += BOTAN_BUILD_COMPILER_IS_GCC
    #*clang*:DEFINES += BOTAN_BUILD_COMPILER_IS_CLANG
    #*icc*:DEFINES += BOTAN_BUILD_COMPILER_IS_INTEL

    #CONFIG(x86_64):DEFINES += BOTAN_TARGET_ARCH_IS_X86_64

    #win32 {
    #DEFINES += BOTAN_TARGET_OS_IS_WINDOWS \
    #BOTAN_TARGET_OS_HAS_LOADLIBRARY BOTAN_TARGET_OS_HAS_WIN32_GET_SYSTEMTIME \
    #BOTAN_TARGET_OS_HAS_WIN32_VIRTUAL_LOCK BOTAN_HAS_DYNAMICALLY_LOADED_ENGINE \
    #BOTAN_HAS_DYNAMIC_LOADER BOTAN_HAS_ENTROPY_SRC_CAPI BOTAN_HAS_ENTROPY_SRC_WIN32 \
    #BOTAN_HAS_MUTEX_WIN32
    if(WIN32)
        add_definitions(-DBOTAN_TARGET_OS_IS_WINDOWS
                        -DBOTAN_TARGET_OS_HAS_LOADLIBRARY
                        -DBOTAN_TARGET_OS_HAS_WIN32_GET_SYSTEMTIME
                        -DBOTAN_TARGET_OS_HAS_WIN32_VIRTUAL_LOCK
                        -DBOTAN_HAS_DYNAMICALLY_LOADED_ENGINE
                        -DBOTAN_HAS_DYNAMIC_LOADER
                        -DBOTAN_HAS_ENTROPY_SRC_CAPI
                        -DBOTAN_HAS_ENTROPY_SRC_WIN32
                        -DBOTAN_HAS_MUTEX_WIN32)
        #msvc {
        if(MSVC)
            #QMAKE_CXXFLAGS_EXCEPTIONS_ON = -EHs
            set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -EHs")


            #QMAKE_CXXFLAGS += -wd4251 -wd4290 -wd4250
            set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -wd4251 -wd4290 -wd4250")

            #DEFINES += BOTAN_BUILD_COMPILER_IS_MSVC BOTAN_TARGET_OS_HAS_GMTIME_S _SCL_SECURE_NO_WARNINGS
            add_definitions(-DBOTAN_BUILD_COMPILER_IS_MSVC
                            -DBOTAN_TARGET_OS_HAS_GMTIME_S
                            -D_SCL_SECURE_NO_WARNINGS)
        #} else {
        else(MSVC)
            #QMAKE_CFLAGS += -fpermissive -finline-functions -Wno-long-long
            set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fpermissive -finline-functions -Wno-long-long")

            #QMAKE_CXXFLAGS += -fpermissive -finline-functions -Wno-long-long
            set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive -finline-functions -Wno-long-long")
        #}
        endif(MSVC)

        #LIBS += -ladvapi32 -luser32
        target_link_libraries(botan advapi32)
        target_link_libraries(botan user32)
        target_link_libraries(botan_static advapi32)
        target_link_libraries(botan_static user32)

    #}
    endif(WIN32)

    #linux*|freebsd* {
    #LIBS += -lrt $$QMAKE_LIBS_DYNLOAD
    #}

# endif(USE_SYSTEM_BOTAN)                  # }
