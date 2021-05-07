# Redis

​	本个代码仓库用来学习redis操作,存放笔记.

---

## Redis安装

- ### Redis服务端

  #### 下载

  ```shell
  wget -c https://download.redis.io/releases/redis-6.2.3.tar.gz?_ga=2.249914884.346692040.1620308015-1712615265.1620308015
  ```

  推荐用msi安装

  ```shell
  wget -c https://github.com/tporadowski/redis/releases
  ```

  

  #### 安装

  ##### bin

  ```shell
  cd redis-6.2.3 && make && make install
  ```

  

  ##### msi

  直接下一步

  

  #### 启动

  ```shell
  cp redis-server.exe /usr/bin
  
  #指定配置
  redis-server.exe redis.windows.conf
  ```

  

- ### Redis客户端

  #### 自带客户端

  ```shell
  #自带的
  redis-cli
  ```

  #### go操作

  1. ##### 链接数据库

     API文档,所有以Dial开头

  2. ##### 操作数据库

     Do()函数[推荐],Send()函数.

  3. ##### Reply Helpers

     相当于类型断言.根据使用的具体数据类型,选择调用
  
  ---
  
  代码实现
  
  ```go
  package main
  
  import (
  	"fmt"
  	"github.com/gomodule/redigo/redis"
  )
  
  func main() {
  	//1.链接数据库
  	conn, err := redis.Dial("tcp", "127.0.0.1:6380")
  	if err != nil {
  		fmt.Println("redis.Dial() err", err)
  		return
  	}
  	defer conn.Close()
  	//2.操作数据库
  	reply, err := conn.Do("set", "itcast", "itheima")
  	if err != nil {
  		fmt.Println("conn.Do() err:", err)
  		return
  	}
  
  	//3.回复助手类函数.断言类型
  	r, e := redis.String(reply, err)
  	fmt.Println(r, e)
  }
  ```
  
  

