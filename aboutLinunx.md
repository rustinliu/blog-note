## 本地文件上传到服务器以及服务器文件下载到本地

* 使用SCP命令

  1. 从服务器复制文件到本地(服务器端操作)：

     ```sh
     scp root@192.168.1.100:/data/test.txt /home/myfile/
     补充：
     1. 多文件拷贝
     　　scp root@192.168.1.100:/data/\{test1.txt,test2.cpp,test3.bin,test.*\} /home/myfile/
     2. scp默认连接的远端主机22端口，如果ssh不是使用标准的22端口（以233为例）则使用-P（P大写）指定：
     　　scp -P 233 root@192.168.1.100:/data/test.txt /home/myfile/
     ```

  2. 从服务器复制文件夹到本地（服务器端操作）：

     ```sh
     scp -r root@192.168.1.100:/data/ /home/myfile/
     只需在前面加 -r 即可，就可以拷贝整个文件夹。
     ```

  3. 从本地复制文件到服务器（本地端操作）：

     ```sh
     scp /home/myfile/test.txt root@192.168.1.100:/data/
     补充：多文件拷贝
     scp /home/myfile/test1.txt test2.cpp test3.bin test.* root@192.168.1.100:/data/
     ```

  4. 从本地复制文件夹到服务器（本地端操作）：

     ```sh
     scp -r /home/myfile/ root@192.168.1.100:/data/
     ```

