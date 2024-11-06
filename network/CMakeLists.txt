include(CheckFunctionExists)

check_function_exists(accept4 HAVE_ACCEPT4)
if(NOT HAVE_ACCEPT4)
  set_source_files_properties(SocketsOps.cc PROPERTIES COMPILE_FLAGS "-DNO_ACCEPT4")
endif()

set(net_SRCS
  src/Acceptor.cc
  src/Buffer.cc
  src/Channel.cc
  src/Connector.cc
  src/EventLoop.cc
  src/EventLoopThread.cc
  src/EventLoopThreadPool.cc
  src/InetAddress.cc
  src/Poller.cc
  src/Socket.cc
  src/SocketsOps.cc
  src/TcpClient.cc
  src/TcpConnection.cc
  src/TcpServer.cc
  src/util.cc
  )

add_library(network ${net_SRCS})
target_link_libraries(network  glog)
target_include_directories(network PUBLIC
  ./include
  )


install(TARGETS  network DESTINATION  lib)


