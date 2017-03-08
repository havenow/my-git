# 克隆远程仓库    
git clone ssh://git@github.com/username/project.git   
git clone git@github.com:username/project.git   
使用ssh协议，还是git开头的；使用http协议，是https开头的。    
github上面下载代码时，点击clone or download，弹出来的窗口可以选择使用ssh还是http协议   
选项是：Use HTTPS/Use SSH   

#添加远程仓库的链接    
git remote add origin git@github.com:username/project.git   

ssh协议对数据压缩比较大，传输速度比http协议快    

# 生成RSA密钥对    
ssh-Keygen -t rsa -C "your email"   
cd ~    
cd .ssh     
ls 可以看到：id_rsa 、id_rsa.pub(公钥) cat id_rsa.pub 显示公钥的内容   
在Github网站添加公钥，就可以使用SSH协议了。
