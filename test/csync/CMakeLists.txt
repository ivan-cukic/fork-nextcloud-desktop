project(tests)

set(TORTURE_LIBRARY torture)

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_BINARY_DIR}
  ${CMOCKA_INCLUDE_DIR}
)

include_directories(${CHECK_INCLUDE_DIRS})
# create test library
add_library(${TORTURE_LIBRARY} STATIC torture.c cmdline.c)
target_link_libraries(${TORTURE_LIBRARY} ${CMOCKA_LIBRARIES} ${CSYNC_LIBRARY})

set(TEST_TARGET_LIBRARIES ${TORTURE_LIBRARY} Qt5::Core ocsync)

# create tests

# std
add_cmocka_test(check_std_c_alloc std_tests/check_std_c_alloc.c ${TEST_TARGET_LIBRARIES})
add_cmocka_test(check_std_c_jhash std_tests/check_std_c_jhash.c ${TEST_TARGET_LIBRARIES})
add_cmocka_test(check_std_c_str std_tests/check_std_c_str.c ${TEST_TARGET_LIBRARIES})


# csync tests
add_cmocka_test(check_csync_exclude csync_tests/check_csync_exclude.cpp ${TEST_TARGET_LIBRARIES})
add_cmocka_test(check_csync_util csync_tests/check_csync_util.cpp ${TEST_TARGET_LIBRARIES})
add_cmocka_test(check_csync_misc csync_tests/check_csync_misc.cpp ${TEST_TARGET_LIBRARIES})

# vio
add_cmocka_test(check_vio vio_tests/check_vio.cpp ${TEST_TARGET_LIBRARIES})
add_cmocka_test(check_vio_ext vio_tests/check_vio_ext.cpp ${TEST_TARGET_LIBRARIES})

# sync
add_cmocka_test(check_csync_update csync_tests/check_csync_update.cpp ${TEST_TARGET_LIBRARIES})

# encoding
add_cmocka_test(check_encoding_functions encoding_tests/check_encoding.cpp ${TEST_TARGET_LIBRARIES})

