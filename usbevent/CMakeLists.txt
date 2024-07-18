add_executable(usbevent)
target_sources(usbevent
    PRIVATE
        usbevent.c
)
target_link_libraries(usbevent PRIVATE PkgConfig::LIBUSB1)
