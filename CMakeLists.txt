cmake_minimum_required(VERSION 3.10)

# Read src/unity.h file and get project version from it
set(UNITY_HEADER "src/unity.h")

project(cmock
    LANGUAGES   C
    DESCRIPTION "Mock and stub generator ."
)

target_sources(${PROJECT_NAME}
        PRIVATE
        src/cmock.c
)

target_include_directories(${PROJECT_NAME}
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src/
)

set_target_properties(${PROJECT_NAME}
    PROPERTIES
        C_STANDARD          11
        C_STANDARD_REQUIRED ON
        C_EXTENSIONS        OFF
        EXPORT_NAME         framework
)

target_compile_options(${PROJECT_NAME}
    PRIVATE
        # Clang
        $<$<C_COMPILER_ID:Clang>:
            -Wcast-align
            -Wcast-qual
            -Wconversion
            -Wexit-time-destructors
            -Wglobal-constructors
            -Wmissing-noreturn
            -Wmissing-prototypes
            -Wno-missing-braces
            -Wold-style-cast
            -Wshadow
            -Wweak-vtables
            -Werror
            -Wall
            $<$<VERSION_GREATER_EQUAL:$<C_COMPILER_VERSION>,8.0.0>:-Wextra-semi-stmt>
        >

        # GCC
        $<$<C_COMPILER_ID:GNU>:
            -Waddress
            -Waggregate-return
            -Wformat-nonliteral
            -Wformat-security
            -Wformat
            -Winit-self
            -Wmissing-declarations
            -Wmissing-include-dirs
            -Wno-multichar
            -Wno-parentheses
            -Wno-type-limits
            -Wno-unused-parameter
            -Wunreachable-code
            -Wwrite-strings
            -Wpointer-arith
            -Werror
            -Wall
        >

        # MSVC
        $<$<C_COMPILER_ID:MSVC>:
            /Wall
        >
)