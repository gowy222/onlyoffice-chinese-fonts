# onlyoffice-chinese-fonts
旨在解决onlyoffice-document-server中的中文字体名称显示问题<br>

## for onlyoffice 6.3.X
字体比较完美。已全部上传完毕。<br>
先进入docker容器。<br>

```
sudo docker exec -it oo6 /bin/bash
#进入容器后执行
cd /usr/share/fonts/
rm -rf *
cd /var/www/onlyoffice/documentserver/core-fonts/
rm -rf *
```
将所有的原来字体删除。<br>
再将所有字体全部下载到容器的`/usr/share/fonts`目录下。<br>
在容器内执行<br>
`
 /usr/bin/documentserver-generate-allfonts.sh
`
<br>
将浏览器缓存清空，即可正常使用。<br>
放效果图：
<img src=https://github.com/funggtopp/onlyoffice-chinese-fonts/raw/master/onlyoffice_chinesefonts.jpg></img>

## for onlyoffice 5.X
将字体文件单独下载到fonts目录。在fonts目录的上一目录中执行如下命令：
```
sudo docker cp ./fonts/ 容器名:/usr/share/fonts/truetype/
```
进入容器，会发现在truetype下又多了一个fonts目录。执行
```
fc-cache -f -v
documentserver-generate-allfonts.sh
```
刷新浏览器缓存，重新进入onlyoffice编辑器，在字体列表中应该能看到字体的中文名了。

*** 注意 *** ：建议不要删除容器里原来ｆｏｎｔｓ目录里的字体，可能会出现方框问题。
