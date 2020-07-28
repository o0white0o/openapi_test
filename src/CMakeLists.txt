cmake_minimum_required(VERSION 3.13)

set(PROJECT_NAME documentation)

set(SPEC_PUBLIC_FILE  ${CMAKE_CURRENT_SOURCE_DIR}/main.yaml)

set(SOURCES
    ${SPEC_PUBLIC_FILE}
    commons.yaml
    images.yaml
    legacy.yaml
    persons.yaml
    )

set(DOC_NAME api)
set(DOC_PUBLIC_FILE   ${CMAKE_CURRENT_BINARY_DIR}/${DOC_NAME}_public.html)

set(OUTPUT_FILES
    ${DOC_PUBLIC_FILE}
    )

set(GEN_TOOL_CMD ${NPX} redoc-cli bundle --output)

add_custom_command(
  OUTPUT  ${OUTPUT_FILES}

  COMMAND ${GEN_TOOL_CMD} ${DOC_PUBLIC_FILE}  ${SPEC_PUBLIC_FILE}

  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  DEPENDS ${SOURCES}
)

add_custom_target(${PROJECT_NAME} ALL
                  SOURCES ${SOURCES}
                  DEPENDS ${OUTPUT_FILES}
                  )

install(FILES ${OUTPUT_FILES}
        DESTINATION ./server/app/static
        )
