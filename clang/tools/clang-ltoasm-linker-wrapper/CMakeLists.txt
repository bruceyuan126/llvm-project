set(LLVM_LINK_COMPONENTS BitWriter Core Object Support)

if(NOT CLANG_BUILT_STANDALONE)
  set(tablegen_deps intrinsics_gen)
endif()

add_clang_executable(clang-ltoasm-linker-wrapper
  ClangLtoAsmLinkerWrapper.cpp

  DEPENDS
  ${tablegen_deps}
  )

set(CLANG_LTOASM_LINKER_WRAPPER_LIB_DEPS
  clangBasic
  )

add_dependencies(clang clang-ltoasm-linker-wrapper)

target_link_libraries(clang-ltoasm-linker-wrapper
  PRIVATE
  ${CLANG_LTOASM_LINKER_WRAPPER_LIB_DEPS}
  )

install(TARGETS clang-ltoasm-linker-wrapper RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}")
