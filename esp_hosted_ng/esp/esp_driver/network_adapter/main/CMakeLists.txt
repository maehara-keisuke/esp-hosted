set(COMPONENT_SRCS "app_main.c" "slave_bt.c" "cmd.c" "stats.c")
set(COMPONENT_ADD_INCLUDEDIRS "./include")

if(CONFIG_ESP_SDIO_HOST_INTERFACE)
    list(APPEND COMPONENT_SRCS sdio_slave_api.c)
else(CONFIG_ESP_SPI_HOST_INTERFACE)
    list(APPEND COMPONENT_SRCS spi_slave_api.c)
endif()


register_component()

target_compile_definitions(${COMPONENT_LIB} PRIVATE)

# Add directory of protocomm_priv.h to include paths
idf_component_get_property(protocomm_dir protocomm COMPONENT_DIR)
target_include_directories(${COMPONENT_LIB} PRIVATE "${protocomm_dir}/src/common")
