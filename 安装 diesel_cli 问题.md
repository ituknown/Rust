### PgSQL

准备

```bash
# 清理旧版本 
cargo uninstall diesel_cli

# 重新安装 diesel_cli, 只启用 mysql 
cargo install diesel_cli --no-default-features --features postgres
```

配置 RUSTFLAGS（推荐）：

```bash
export PQ_HOME=/Users/ituknown/pgsql_17_6
export RUSTFLAGS="-L$PQ_HOME/lib"

# include 可以不配置
export RUSTFLAGS="$RUSTFLAGS -I$PQ_HOME/include"
```

或使用环境变量和动态库方式（不推荐）：

```bash
export PQ_HOME=/Users/ituknown/pgsql_17_6
export PQ_LIB_DIR=$PQ_HOME/lib
export PQ_INCLUDE_DIR=$PQ_HOME/include
export DYLD_LIBRARY_PATH=$PQ_LIB_DIR:$DYLD_LIBRARY_PATH
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