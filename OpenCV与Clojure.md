# OpenCV与Clojure
#技术栈/兴趣爱好/Lisp

## 环境配置
- IDE：Intellij
	- Plugins: Cursive
- 初始化项目
	- 创建Leiningen项目
	- 配置project.clj
	- 启动一次：在项目根目录执行命令`lein run`
	- 启动后持续监听文件变化，自动执行：`lein auto run`
		- 比使用IDE的run方便
		- 暂时没想要用debug模式
### project.clj 必要配置
``` clojure
(defproject opencv_jvm "0.1.0-SNAPSHOT"
  :java-source-paths ["java"] 
  :main HelloLeiningen
  :plugins [[lein-auto "0.1.3"]]
  :auto {:default {:file-pattern #"\.(java)$"}}
  :repositories [["vendredi" "https://repository.hellonico.info/repository/hellonico/"]]
  :dependencies [[org.clojure/clojure "1.11.1"]
                 [opencv/opencv "3.3.1"]
                 [opencv/opencv-native "3.3.1"]]
  )
```
### 必要文件结构
``` shell  
$ tree .

├── java
│   └── HelloLeiningen.java
├── project.clj
└── resources
    └── hello.png
```




