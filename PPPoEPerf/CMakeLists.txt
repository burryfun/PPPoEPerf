add_executable(pppoe_perf main.cpp pppoe_worker.cpp networker.cpp)
INSTALL(TARGETS pppoe_perf
		DESTINATION /usr/bin PERMISSIONS OWNER_READ GROUP_READ WORLD_READ OWNER_WRITE OWNER_EXECUTE GROUP_EXECUTE WORLD_EXECUTE
		COMPONENT libraries
)
INSTALL(DIRECTORY DESTINATION /etc/pppoe_perf)
INSTALL(FILES conf.json conf_100.json conf_1000.json conf_5000.json conf_10000.json DESTINATION /etc/pppoe_perf)
target_link_libraries(pppoe_perf ${Boost_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} ${OPENSSL_LIBRARIES})
