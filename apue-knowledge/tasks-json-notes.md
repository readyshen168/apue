# 编译 APUE C 文件指南

1. 打开需要编译的 c 文件，按下 Cmd+shift+B 开始编译
2. 容易出现问题的地方：
   a. 找不到 apue.h 文件，源于路径设置错误，`-I../include`，可以使用绝对路径/Users/ready/Downloads/apue.3e/include,
   也可以通过增加 options.cwd 字段来设置 vscode 任务的工作目录为当前待编译源文件的所在目录

   b. 链接阶段找不到 err_quit 和 err_sys 这两个符号。这两个函数定义在 APUE 的库 libapue.a 里。

   1. 先编译 APUE 库
      cd ../lib
      make
   2. 编译时链接 APUE 库:
      -L../lib -lapue  
      此时应当已经增加了 options.cwd 字段(见 a)

3. 按下 Cmd+shift+B 后相当于执行：clang -g -Wall -Wextra -std=c17 -I../include -L../lib -lapue -o ls1 ls1.c
