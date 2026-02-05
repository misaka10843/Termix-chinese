# Termix-chinese

修复Termix的蹩脚中文

我不知道Termix的作者是怎么想的，crowdin虽然有简体中文和繁体中文，但是并不会创建简体中文的文件，并且繁体中文还是机翻

<img width="1862" height="875" alt="屏幕截图 2026-02-05 102658" src="https://github.com/user-attachments/assets/8a7ef2b1-a235-4080-91bf-61d3200b37fe" />

也就是说根本就不能提交简体中文的翻译文本，那还不如直接通过替换前端文件来修复中文问题

## 如何使用

首先先打开最新的一次编译[actions](https://github.com/misaka10843/Termix-chinese/actions/workflows/main.yml)

进入最新一次编译之后点击Linux Build下载最新的汉化编译包

<img width="1376" height="834" alt="屏幕截图 2026-02-05 112956" src="https://github.com/user-attachments/assets/1c4a5907-b981-48e3-88f2-cc5137a4f7d9" />

修改docker compose暴露其前端文件夹

```yml
services:
  termix:
    image: ghcr.io/lukegus/termix:latest
    container_name: termix
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - ./data:/app/data
      - ./html:/app/html # 这一行映射前端文件夹
    environment:
      - PUID=1000
      - PGID=10
      - PORT=8080
```

然后将下载的Linux Build压缩包中的所有文件解压进映射出来的前端文件夹后即可


