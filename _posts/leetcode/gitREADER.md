一定要注意,如果你在创建github仓库时，初始化了一个readme.md文件,远程仓库不是空的，则需要先将远程仓库与本地仓库同步,使用命令: git pull --rebase origin master.将远程文件拉回本地仓库,然后再执行:git push origin master,就能成功了.

 总结：其实只需要进行下面几步就能把本地项目上传到Github

     1、在本地创建一个版本库（即文件夹），通过git init把它变成Git仓库；
    
     2、把项目复制到这个文件夹里面，再通过git add .把项目添加到仓库；
    
     3、再通过git commit -m "注释内容"把项目提交到仓库；
     4、在Github上设置好SSH密钥后，新建一个远程仓库，通过git remote add origin https://github.com/guyibang/TEST2.git将本地仓库和远程仓库进行关联；
    5、最后通过git push -u origin master把本地仓库的项目推送到远程仓库（也就是Github）上；（若新建远程仓库的时候自动创建了README文件会报错，解决办法看上面）。
————————————————
版权声明：本文为CSDN博主「小·幸·运」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/vir_lee/article/details/80464408

经过查资料发现是因为我们在本地新建库后，与远程仓库的内容不一致导致的（远程仓库有一些内容本地没有）。

为此在向远程库推送的时候，要先进行pull同步远程仓库，让本地新建的库和远程库进行同步。
正确步骤：

git init              //初始化仓库
git add .             //添加到本地暂存区  或用 git add  (文件name)
git commit -m “first commit”           //提交到本地仓库
git remote add origin  远程仓库地址    //添加远程仓库 
git pull origin master                 //把远程仓库master分支拉取到本地仓库master分支
git push -u origin master              //把本地仓库的master分支推送到远程仓库master分支