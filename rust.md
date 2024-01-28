```bash
rustup update
# 升级 Rust

rustup self uninstall
# 卸载 Rust

rustup doc
# 查看离线文档

rustc main.rs
# 编译rs源文件
# Windows中会生成 .pdb 文件, 包含调试信息
./main
# 运行main二进制程序

```

```bash
cargo new [project_name]
# 在当前目录下创建新项目

cargo build 
# 构建项目

cargo run
# 构建并运行项目

cargo check
# 编译项目但不运行 

cargo build --release
# 生成运行更快的可执行文件
```