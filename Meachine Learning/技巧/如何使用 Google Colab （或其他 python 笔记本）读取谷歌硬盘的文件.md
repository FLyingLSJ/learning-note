# 如何使用 Google Colab （或其他 python 笔记本）读取谷歌硬盘的文件

1. 存档和上传

   单独上传大量图像（或文件）需要很长时间，因为 Google Drive 必须为每个图像单独分配ID和属性。建议先归档数据集。

   一种可能的归档方法是将包含数据集的文件夹转换为“.tar”文件。 或者将文件压缩后上传谷歌硬盘

   ```
   tar -cvf dataset.tar~ / Dataset # 在 Linux 终端，将文件夹 Dataset 转化为 dataset.tar
   ```

2. 安装依赖包

   ```
   !pip install module # 安装一个包
   ```

   导入必要的库和方法

   ```
   import os
   from pydrive.auth import GoogleAuth
   from pydrive.drive import GoogleDrive
   # 以下两句代码在 Google Colab 才需要添加，其他平台忽略
   from google.colab import auth
   from oauth2client.client import GoogleCredentials
   ```

3. 授权 Google ADK

   必须授权 Google SDK 从 Colab 访问 Google 云端硬盘

   执行命令

   ```
   auth.authenticate_user（）
   gauth = GoogleAuth（）
   gauth.credentials = GoogleCredentials.get_application_default（）
   drive = GoogleDrive（gauth）
   ```

   收到如下所示的提示。点击链接获取密钥。将其复制并粘贴到输入框中，然后按Enter键。

   ![1545737274969](images/1545737274969.png)

   点击链接登陆后，进行授权。然后把一串字符复制到上面的框里，点击回车即可。

   ![1545737340245](images/1545737340245.png)

   对于其他的 jupyter notebook 可以查看 https://pythonhosted.org/PyDrive/quickstart.html  入门指南 

4. 获取您的文件ID

   把文件上传到 Google 云端以后，点击文件获取共享链接

   ![1545737668153](images/1545737668153.png)

5. 传输内容

从Google云端硬盘下载到Colab

执行以下命令。这里，**YOUR_FILE_ID**在上一步中获得，**DOWNLOAD.tar**是您要将文件另存为的名称（或路径）。

```
download = drive.CreateFile({'id':' YOUR_FILE_ID '})
download.GetContentFile(' DOWNLOAD.tar ')
```

![1545737952651](images/1545737952651.png)

下载下来后你可以用 pandas 进行读取或者进行其他操作。

当然，既然可以从 Google 云端下载文件到 Colab，也能从 Colab 上传文件到 Google 云端。

执行以下命令。这里，**FILE_ON_COLAB.txt** 是 **Colab** 上文件的名称（或路径），**DRIVE.txt **是您要将文件保存为（在Google云端硬盘上）的名称（或路径）。

```

```

![1545738383748](images/1545738383748.png)

我把刚才从云盘下载下来的 **result.csv** 文件以文件名 **result_upload.csv** 上传到云端

![1545739136552](images/1545739136552.png)

---

以上适合大文件时候使用，如果只是一个 csv 或者 txt 文件，则有更简单的方法。

1. Google Colab 模块

   Google Colab 具有内置文件模块，可以使用该模块上传或下载文件。通过执行以下命令导入它：

   ```
   from google.colab import files
   ```

2. 上传

   使用以下命令将文件上载到Google Colab （适用于小文件）：

   ```
   files.upload()
   ```

   ![1545740940816](images/1545740940816.png)

   执行完命令后，会出现一个窗口让你上传文件，因为我之前已经有一个 result.csv 文件了，现在它自动给我命名 result(1).csv

3. 下载

   使用以下命令从 Google Colab 下载文件：

   ```
   files.download(' example.txt ')
   ```

   此功能在**Google Chrome中**效果最佳。



参考资料

https://medium.freecodecamp.org/how-to-transfer-large-files-to-google-colab-and-remote-jupyter-notebooks-26ca252892fa