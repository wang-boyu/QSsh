include_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rdparty)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/botan)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOMOC_STRICT OFF)

set(QSshLib_src sftpchannel.cpp
                sshconnection.cpp
                sshkeypasswordretriever.cpp
                sftpdefs.cpp
                sshconnectionmanager.cpp
                sshlogging.cpp
                sftpfilesystemmodel.cpp
                sshcryptofacility.cpp
                sshoutgoingpacket.cpp
                sftpincomingpacket.cpp
                sshdirecttcpiptunnel.cpp
                sshpacket.cpp
                sftpoperation.cpp
                sshhostkeydatabase.cpp
                sshpacketparser.cpp
                sftpoutgoingpacket.cpp
                sshincomingpacket.cpp
                sshremoteprocess.cpp
                sftppacket.cpp
                sshinit.cpp
                sshremoteprocessrunner.cpp
                sshcapabilities.cpp
                sshkeycreationdialog.cpp
                sshsendfacility.cpp
                sshchannel.cpp
                sshkeyexchange.cpp
                sshchannelmanager.cpp
                sshkeygenerator.cpp)

set(QSshLib_hdr sftpchannel.h
                sshconnection.h
                sshkeygenerator.h
                sftpchannel_p.h
                sshconnection_p.h
                sshkeypasswordretriever_p.h
                sftpdefs.h
                sshconnectionmanager.h
                sshlogging_p.h
                sftpfilesystemmodel.h
                sshcryptofacility_p.h
                sshoutgoingpacket_p.h
                sftpincomingpacket_p.h
                sshdirecttcpiptunnel.h
                sshpacket_p.h
                sftpoperation_p.h
                sshdirecttcpiptunnel_p.h
                sshpacketparser_p.h
                sftpoutgoingpacket_p.h
                ssherrors.h
                sshpseudoterminal.h
                sftppacket_p.h
                sshexception_p.h
                sshremoteprocess.h
                ssh_global.h
                sshhostkeydatabase.h
                sshremoteprocess_p.h
                sshbotanconversions_p.h
                sshincomingpacket_p.h
                sshremoteprocessrunner.h
                sshcapabilities_p.h
                sshinit_p.h
                sshsendfacility_p.h
                sshchannel_p.h
                sshkeycreationdialog.h
                sshchannelmanager_p.h
                sshkeyexchange_p.h)

set(QSshLib_ui sshkeycreationdialog.ui)
qt5_wrap_ui(QSshLib_ui_moc ${QSshLib_ui})

add_library(qssh SHARED
    ${QSshLib_src}
    ${QSsshLib_hdr}
    ${QSshLib_ui_moc})
target_link_libraries(qssh Qt5::Core Qt5::Network Qt5::Widgets botan)
set_target_properties(qssh PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(qssh PROPERTIES VERSION ${PROJECT_VERSION_STRING} SOVERSION ${PROJECT_VERSION_MAJOR})
target_include_directories(qssh PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

add_library(qssh_static STATIC
    ${QSshLib_src}
    ${QSsshLib_hdr}
    ${QSshLib_ui_moc})
target_link_libraries(qssh_static Qt5::Core Qt5::Network Qt5::Widgets botan)
set_target_properties(qssh_static PROPERTIES OUTPUT_NAME "qssh")
set_target_properties(qssh_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)
target_include_directories(qssh_static PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
