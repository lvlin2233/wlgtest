
    cmake_minimum_required(VERSION 3.6)
   #要求的cmake最低版本3.6
    include_directories(googletest/include)
   #添加库文件引用所需相对路径


    project(mygtest)
   #项目名称，此处取为mygtest
   add_executable(mygtest sample1_unittest.cc)
   #为项目添加主运行程序
    add_library(sample1 sample1.cc)
   #额外的引用文件
    target_link_libraries(mygtest sample1 
                                   ../googletest/lib/gtestd
                                   ../googletest/lib/gtest_maind
                                   )
    #链接库文件，为防止找不到文件的报错，添加了相对路径，注意：此处默认了是对debug模式的链接库
    #如果对release则应为gtest和gtest_main

    #这个必须放在project的后面，为设置不同模式下运行库模式
    IF(MSVC)
        message("run here")
        set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
        set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
    endif()
     