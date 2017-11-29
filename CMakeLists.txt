# CMakeの最低限必要なバージョン
cmake_minimum_required(VERSION 3.0)

# デバッグ時に値を 1 にする
set(CMAKE_VERBOSE_MAKEFILE 0)

# プロジェクトの名前。CXXはC++の意味なのでそのままにする。
project(g5_project CXX)

# コンパイラに渡す設定
set(CMAKE_CXX_FLAGS "-Wall -Wextra -std=gnu++11")
set(CMAKE_CXX_FLAGS_DEBUG "-g3 -O0")
set(CMAKE_CXX_FLAGS_RELEASE "-O2 -s -DNDEBUG")
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "-g3 -Og")
set(CMAKE_CXX_FLAGS_MINSIZEREL "-Os -s -DNDEBUG")

# pkg-configで見つけるものはここに書く。不要なら省く。
find_package(PkgConfig)

# <CMakeListsの中の識別子> REQUIRED（「必須」） <ライブラリ名>
# ライブラリ名：libXXXのXXXの部分
# 識別子_INCLUDE_DIRS、識別子_LIBRARIES
pkg_check_modules(OPENCV REQUIRED opencv)
pkg_check_modules(GST_APP REQUIRED gstreamer-app-1.0)

# ヘッダの参照先（-I オプション）をここに書く
include_directories(
  ${OPENCV_INCLUDE_DIRS}
  ${GST_APP_INCLUDE_DIRS}
)

# 出力される実行ファイル名を target 変数で指定する
set(target g5_project_bin)

# コンパイルする .cpp ファイルをここに書く
# ヘッダファイルは自動で調べてくれるので入れなくてよい
add_executable(${target}
  pin_roller_detector.cpp
  g5/groove_detector.cpp
)

# 実行ファイルを作るときにリンクするライブラリ（-l オプション）をここに書く
target_link_libraries(${target}
  pthread
  redox
  hiredis
  ev
  ${OPENCV_LIBRARIES}
  ${GST_APP_LIBRARIES}
)
