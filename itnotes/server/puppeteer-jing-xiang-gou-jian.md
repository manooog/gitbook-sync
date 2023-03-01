# puppeteer 镜像构建

puppeteer 是headless chrome，可作为自动化框架和爬虫框架。

在用作爬虫框架的时候，其具备爬取 SPA 的能力，因此是我用得比较多的一个工具。同时，我也是重度的 Docker 用户，在半年前，puppeteer 没有自己的官方镜像。那时候我为了在 Docker 环境下使用 puppeteer，曾自己制作了镜像。

不过，在当时我并没有完全理解 puppeteer 文档提到的 sandbox 模式，对于 Docker 镜像与宿主机共享文件夹的用户权限问题也不理解。这就导致了一些与程序无关的问题，程序逻辑正确，但无法部署。

我先简单描述一下遇到的问题，制作镜像的部分放在第三章。

### 01 用户角色问题

Docker 镜像默认使用 root 用户执行程序，如果宿主机也是 root 用户，那么一般不会遇到文件共享时的权限问题。

举个例子。

进入`/home/root` 目录，启动容器：

```bash
docker run --rm -t ubuntu:slim bash touch 
```
