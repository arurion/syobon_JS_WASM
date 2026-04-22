cmake_minimum_required(VERSION 3.10)
project(ShobonWASM)

add_executable(game main.cpp)
set_target_properties(game PROPERTIES SUFFIX ".js")


target_compile_options(game PRIVATE
    "-std=gnu++98"      # 2007年当時のC++98標準を使用する
    "-fpermissive"      # 昔のルーズな文法（型の暗黙変換など）をエラーではなく「警告」で許容する
    "-Wno-everything"   # 大量に出る「警告」を全部ミュートして、本当の「エラー」だけを表示させる
)

set_target_properties(game PROPERTIES LINK_FLAGS 
    "-O3 -sWASM=1 -sEXPORTED_FUNCTIONS=['_malloc','_free'] -sEXPORTED_RUNTIME_METHODS=['ccall','cwrap'] -sALLOW_MEMORY_GROWTH=1 --no-entry"
)