# ginlibs
基于gin框架日常开发中的脚手架

## 日志
使用样例
```
// 本地global 包，定义全局的变量
package global

import "github.com/hetao19/ginlibs/logger"
var (
  Logger *logger.Logger
)
```

```
// 下载lumberjack日志切割pkg
go get github.com/natefinch/lumberjack
```

```
package main

import (
  "github.com/hetao19/ginlibs/logger"
  "gopkg.in/natefinch/lumberjack.v2"
  "global"
)

func main() {
  global.Logger.Infof("%s gin programmer")
  ...
}

func init() {
  err := setLogger()
  if err != nil {
    log.Fatalf("init.setupLogger err: %v\n", err)
  }
}

func setLogger() error {
  global.Logger = logger.NewLogger(&lumberjack.Logger{
    Filename: "./logs/app.log",
    MaxSize: 600,  // megabytes
    MaxAge: 10,    // days
    LocalTime: true,
    Compress: true,  // disable by default
  }, "", log.LstdFlags).WithCaller(2)
  return nil
}
```
