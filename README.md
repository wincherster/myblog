## 基于hexo&github搭建的个人博客源码


### git clone 到本地后，安装项目依赖

``` bash
  # 克隆仓库内容到本地
  git clone https://github.com/wincherster/myblog.git

  # 安装node包依赖
  npm install  # 或者 npm i
```

### 本地启动项目并预览

``` bash
  hexo serve  # 或者 hexo s
```
浏览器中输入 http://localhost:4000/ 预览效果

注意：报错信息如果是4000端口被占用，可在 _config.yml 文件中修改端口号


### 部署和上传

当编辑和添加文章完成后，可通过以下命令部署到git仓库

```bash
  hexo clean     # 清空本地缓存
  hexo generate  # 构建成静态文件
  hexo deploy    # 部署到git仓库

  # 或者使用简写操作

  hexo clean # 清空本地缓存
  hexo g -d  # 构建 + 部署
```

以上操作基本可以完成日常的更新和部署问题，如果遇到其他问题会维护到该README文件中。


