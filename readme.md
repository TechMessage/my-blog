# 基于hexo个人博客

> 博客部署到gitpage, url地址:https://techmessage.github.io/

## 写文章

```

//1

hexo new "文章的标题"   // 生成一个md文件，在source/_posts下

图片放到到images下， 引用路径  /images/xxx.jpg


//2 
写完后
hexo g -d             // 自动生成html,然后部署到gitpage


//3 
hexo clean            //部署完之后清除生成的public下的文件


```