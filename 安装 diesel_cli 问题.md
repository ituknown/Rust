### PgSQL

准备

```bash
# 清理旧版本 
cargo uninstall diesel_cli

# 重新安装 diesel_cli, 只启用 mysql 
cargo install diesel_cli --no-default-features --features postgres
```

配置动态库：

Linux：

```bash
export PQ_HOME=/Users/ituknown/pgsql_17_6
export LD_LIBRARY_PATH=$PQ_HOME/lib:$LD_LIBRARY_PATH
```

Mac：

```bash
export PQ_HOME=/Users/ituknown/pgsql_17_6
export DYLD_LIBRARY_PATH=$PQ_HOME/lib:$DYLD_LIBRARY_PATH
```

Windows：

```bash
# 配置环境变量
PQ_HOME = "D:\postgresql-18.0"

# PATH 添加: 
%PQ_HOME%\lib
%PQ_HOME%\bin
```

如果使用 rustc 编译，可以配置 RUSTFLAGS：

```bash
export PQ_HOME=/Users/ituknown/pgsql_17_6
export RUSTFLAGS="-L$PQ_HOME/lib"
```

### MySQL

准备

```bash
# 清理旧版本 
cargo uninstall diesel_cli

# 重新安装 diesel_cli, 只启用 postgres 
cargo install diesel_cli --no-default-features --features mysql
```

配置环境变量和动态库

```bash
export MYSQL_HOME=/Users/ituknown/mysql_8_4_6
export MYSQLCLIENT_VERSION=8.4.6
export MYSQLCLIENT_LIB_DIR=$MYSQL_HOME/lib

# 下面两个可以不配置
export MYSQLCLIENT_INCLUDE_DIR=$MYSQL_HOME/include
export DYLD_LIBRARY_PATH=$MYSQLCLIENT_LIB_DIR:$DYLD_LIBRARY_PATH
```