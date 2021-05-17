---
lab:
    az204Title: 'Lab 04: 构造多语言数据解决方案'
    az020Title: 'Lab 04: 构造多语言数据解决方案'
    az204Module: 'Module 04: 开发使用 Cosmos DB 存储的解决方案'
    az020Module: 'Module 04: 开发使用 Cosmos DB 存储的解决方案'
    type: '答案要点'
---

# 实验室 04：构造多语言数据解决方案
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 可能会在开发此培训内容之后发生更改。这些更改可能会导致实验室说明和步骤不相符。

我们发现社区进行了必要更改时，Microsoft 将会更新此培训课程。但由于云更新频繁，在此培训内容更新前 UI 可能已更改。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录到实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名：**Admin**

-   密码：**Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

-   Visual Studio Code

### 练习 1：在 Azure 中创建数据库资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，浏览到 Azure 门户 ([portal.azure.com](https://portal.azure.com))。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：你第一次登录 Azure 门户时会为你提供门户导览。选择 **“开始使用”**，以跳过导览并开始使用门户。

#### 任务 2：创建 Azure SQL 数据库服务器资源

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“SQL 服务器”**。

1.  在 **“SQL 服务器”** 边栏选项卡中，找到 SQL 服务器实例列表。

1.  在 **“SQL 服务器”** 边栏选项卡中，选择 **“新建”**。

1.  在 **“创建 SQL 数据库服务器”** 边栏选项卡中，查看边栏选项卡中的选项卡，如 **“基本”**、**“网络”** 和 **“其他设置”**。

    > **备注**：每个选项卡都代表创建新 Azure SQL 数据库服务器的工作流中的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

    1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 下拉列表设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“PolyglotData”**，然后选择 **“确定”**。
    
    1.  在 **“服务器名称”** 文本框中，输入 **polysqlsrvr*[yourname]***。
    
    1.  在 **“位置”** 下拉列表中，选择 **“(美国)美国东部”**。
    
    1.  在 **“服务器管理员登录名”** 文本框中，输入 **“testuser”**。
    
    1.  在 **“密码”** 文本框中，输入 **“TestPa55w.r”**。
    
    1.  在 **“确认密码”** 文本框中，再次输入 **“TestPa55w.rd”**。

    1.  选择 **“下一步: 网络”**。

1.  在 **“网络”** 选项卡中，执行以下操作：

    1.  在 **“允许 Azure 服务和资源访问此服务器”** 部分，选择 **“是”**。
    
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建 SQL 数据库服务器。

    > **备注**：在当前实验室中，我们仅创建 Azure SQL 逻辑服务器。我们将在稍后的实验室中创建 Azure SQL 数据库实例。

    > **备注**：等待创建任务完成，再继续本实验室。

#### 任务 3：创建 Azure Cosmos DB 帐户资源

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“Azure Cosmos DB”**。

1.  在 **“Azure Cosmos DB”** 边栏选项卡中，找到 Azure Cosmos DB 实例列表。

1.  在 **“Azure Cosmos DB”** 边栏选项卡中，选择 **“新建”**。

1.  在 **“创建 Azure Cosmos DB 帐户”** 边栏选项卡中，查看边栏选项卡中的选项卡，如 **“基本”**、**“网络”** 和 **“标记”**。

    > **备注**：每个选项卡代表创建新 Azure Cosmos DB 帐户的工作流中的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 列表设置为其默认值。
    
    1.  在 **“资源组”** 部分，从列表中选择 **“PolyglotData”**。
    
    1.  在 **“AccountName”** 文本框中，输入 **“polycosmos*[yourname]”***。
    
    1.  在 **API** 下拉列表中，选择 **“核心(SQL)”**。

    1.  在 **“应用免费层折扣”** 部分，选择 **“不应用”**。
    
    1.  在 **“位置”** 下拉列表中，选择 **“(美国)美国东部”** 区域。
    
    1.  在 **“帐户类型”** 部分，选择 **“非生产”**。
    
    1.  在 **“多区域写入”** 部分，选择 **“禁用”**。
    
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建 Azure Cosmos DB 帐户。

    > **备注**：等待创建任务完成，再继续本实验室。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 **polycosmos*[yourname]*** Azure Cosmos DB 帐户。

1.  在 **“Azure Cosmos DB 帐户”** 边栏选项卡中，找到边栏选项卡中的 **“设置”** 部分，然后选择 **“密钥”** 链接。

1.  在“密钥”窗格中，将值记录在 **“主连接字符串”** 文本框中。你稍后将在本实验室中使用此值。

#### 任务 4：创建 Azure 存储帐户资源

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡中，找到 Storage 实例列表。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“新建”**。

1.  在 **“创建存储帐户”** 边栏选项卡中，查看边栏选项卡中的选项卡，如 **“基本”**、**“高级”** 和 **“标记”**。

    > **备注**：每个选项卡代表创建新的 Azure 存储帐户的工作流中的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 列表设置为其默认值。
    
    1.  在 **“资源组”** 部分，从列表中选择 **“PolyglotData”**。
    
    1.  在 **“存储帐户名称”** 文本框中，输入 **“polystor*[yourname]”***。
    
    1.  在 **“位置”** 下拉列表中，选择 **“(美国)美国东部”** 区域。
    
    1.  在 **“性能”** 部分中，选择 **“标准”**。
    
    1.  在 **“帐户类型”** 下拉列表中，选择 **“StorageV2 (常规用途 v2)”**。
    
    1.  在 **“复制”** 下拉列表中，选择 **“本地冗余存储(LRS)”**。
        
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建存储帐户。

    > **备注**：等待创建任务完成，再继续本实验室。

#### 回顾

在本练习中，创建了多语言数据解决方案所需的所有 Azure 资源。

### 练习 2：导入并验证数据

#### 任务 1：上传映像 Blob

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 “**polystor*[yourname]***” 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择边栏选项卡中 **“Blob 服务”** 部分中的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“+ 容器”**。

1.  在 **“新建容器”** 中执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **“images”**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“Blob (仅限 Blob 匿名读取访问)”**。
    
    1.  选择 **“创建”**。

1.  返回 **“容器”** 部分，选择新创建的 **images** 容器。

1.  在 **“容器”** 边栏选项卡中，找到边栏选项卡中的 **“设置”** 部分，然后选择 **“属性”** 链接。

1.  在“属性”窗格中，将值记录在 **“URL”** 字段中。你稍后将在本实验室中使用此值。

1.  在边栏选项卡中找到并选择 **“概述”** 链接。

1.  在边栏选项卡中，选择 **“上传”**。

1.  在 **“上传 Blob”** 弹出窗口中，执行以下操作：
    
    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。
    
    1.  在 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\04\\Starter\\Images**，全选 42 个单独的 **.jpg** 图像文件，然后选择 **“打开”**。
    
    1.  确保 **“如果文件已存在，则覆盖”** 已选中，然后选择 **“上传”**。

    > **备注**：等待所有 Blob 上传完成，然后再继续本实验室。

#### 任务 2：上传 SQL .bacpac 文件

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 **“polystor*[yourname]*”** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择边栏选项卡中 **“Blob 服务”** 部分中的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“+ 容器”**。

1.  在 **“新建容器”** 弹出窗口中，执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **“databases”**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“专用(非匿名访问)”**。
    
    1.  选择 **“确定”**。

1.  返回 **“容器”** 部分，选择新创建的 **databases** 容器。

1.  在 **“容器”** 边栏选项卡中，选择 **“上传”**。

1.  在 **“上传 Blob”** 弹出窗口中，执行以下操作：
    
    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。
    
    1.  在 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\04\\Starter**，选择 **AdventureWorks.bacpac** 文件，然后选择 **“打开”**。
    
    1.  确保 **“如果文件已存在，则覆盖”** 已选中，然后选择 **“上传”**。

    > **备注**：等待 Blob 上传完成，然后再继续本实验室。

#### 任务 3：导入 SQL 数据库

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 “**polysqlsrvr*[yourname]***” SQL 服务器。

1.  在 **“SQL 服务器”** 边栏选项卡中，选择 **“导入数据库”**。

1.  在 **“导入数据库”** 边栏选项卡中，执行以下操作：

    1.  将 **“订阅”** 列表设置为其默认值。

    1.  选择 **“存储”** 选项。

    1.  在 **“存储帐户”** 边栏选项卡中，选择你之前在本实验室中创建的 “**polystor*[yourname]***” 存储帐户*。 

    1.  在 **“容器”** 边栏选项卡中，选择你之前在本实验室中创建的 **databases** 容器。 

    1.  在 **“容器”** 边栏选项卡中，选择你之前在本实验室中创建的 **AdventureWorks.bacpac** Blob，然后选择 **“选择”** 关闭边栏选项卡。

    1.  从 **“导入数据库”** 边栏选项卡返回，将 **“定价层”** 选项设置为其默认值。

    1.  在 **“数据库名称”** 文本框中，输入 **“AdventureWorks”**。

    1.  将 **“排序规则”** 文本框设置为其默认值。

    1.  在 **“服务器管理员登录名”** 文本框中，输入 **“testuser”**。
    
    1.  在 **“密码”** 文本框中，输入 **“TestPa55w.rd”**。
    
    1.  选择 **“确定”**。

    > **备注**：等待数据库创建完成，然后再继续本实验室。如果在导入步骤中收到与防火墙相关的错误，则表示你之前在实验室中没有在 SQL Server 上正确配置 **“允许 Azure 服务访问服务器”** 设置。  查看设置，删除空白 **AdventureWorks** 数据库，然后再次尝试导入。
    
#### 任务 4：使用导入的 SQL 数据库

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 “**polysqlsrvr*[yourname]***” SQL 服务器。

1.  在 **“SQL 服务器”** 边栏选项卡中，找到边栏选项卡中的 **“安全性”** 部分，然后选择 **“防火墙和虚拟网络”** 链接。

1.  在“防火墙和虚拟网络”窗格中执行以下操作：

    1.  选择 **“添加客户端 IP”**
    
    1.  选择 **“保存”**。

    1.  在 **“成功!”** 确认对话框中，选择 **“确定”**。

    > **备注**：此步骤将确保本地计算机可以访问与此服务器关联的数据库。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 **AdventureWorks** SQL 数据库。

1.  在 **“SQL 数据库”** 边栏选项卡中，找到边栏选项卡中的 **“设置”** 部分，然后选择 **“连接字符串”** 链接。

1.  在“连接字符串”窗格中，将值记录在 **“ADO.NET (SQL 身份验证)”** 文本框中。你稍后将在本实验室中使用此值。

1.  通过执行以下操作更新记录的连接字符串：

    1.  在连接字符串中，找到 *your_username* 占位符，并将其替换为 **testuser**。

    1.  在连接字符串中，找到 *your_password* 占位符，并将其替换为 **TestPa55w.rd**。

        > **备注**：例如，如果连接字符串最初为 ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID={your_username};Password={your_password};``，则更新后的连接字符串将为 ``Server=tcp:polysqlsrvrinstructor.database.windows.net,1433;Initial Catalog=AdventureWorks;User ID=testuser;Password=TestPa55w.rd;``

1.  在边栏选项卡中找到并选择 **“查询编辑器(预览版)”** 链接。

1.  在“查询编辑器”窗格中，执行以下操作：

    1.  在 **“登录名”** 文本框中，输入 **“testuser”**。

    1.  在 **“密码”** 文本框中，输入 **“TestPa55w.rd”**。

    1.  选择 **“确定”**。

1.  在打开的查询编辑器中，输入以下查询命令：

    ```
    SELECT * FROM AdventureWorks.dbo.Models
    ```

1.  选择 **“运行”** 以运行查询，然后查看结果。

    > **备注**：此查询将返回 Web 应用程序主页上的模型列表。

1.  在查询编辑器中，将现有查询内容替换为以下查询：

    ```
    SELECT * FROM AdventureWorks.dbo.Products
    ```

1.  选择 **“运行”** 以运行查询，然后查看结果。

    > **备注**：此查询将返回与每个模型关联的产品列表。

#### 回顾

在本练习中，你导入了将与 Web 应用程序一起使用的所有资源。

### 练习 3：打开并配置 .NET Web 应用程序

#### 任务 1：打开并生成 Web 应用程序

1.  在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。

1.  在 **“文件”** 菜单上，选择 **“打开文件夹”**。

1.  在打开的 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\04\\Starter\\AdventureWorks**，然后选择 **“选择文件夹”**。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符中，输入以下命令并选择 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

    > **备注**：**dotnet build** 命令将在生成文件夹中的所有项目之前自动还原所有丢失的 NuGet 包。

1.  查看在终端上打印的生成结果。生成应成功完成，不会出现错误或警告消息。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：更新 SQL 连接字符串

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **AdventureWorks.Web** 项目。

1.  打开 **appsettings.json** 文件。

1.  在 JavaScript 对象表示法 (JSON) 对象的第 3 行，找到 **ConnectionStrings.AdventureWorksSqlContext** 路径。注意当前值为空：

    ```
    "ConnectionStrings": {
        "AdventureWorksSqlContext": "",
        ...
    },
    ```

1.  通过将 **AdventureWorksSqlContext** 属性的值设置为你之前在本实验室中记录的 SQL 数据库的 **ADO.NET（SQL 身份验证）连接字符串**来更新该值。

    > **备注**：请务必在此处使用更新后的连接字符串。从门户复制的原始连接字符串将不具有连接到 SQL 数据库所需的用户名和密码。

1.  保存 **appsettings.json** 文件。

#### 任务 3：更新 Blob 基本 URL

1.  在 JSON 对象的第 8 行，找到 **Settings.BlobContainerUrl** 路径。注意当前值为空：

    ```
    "Settings": {
        "BlobContainerUrl": "",
        ...
    }
    ```

1.  通过将 **BlobContainerUrl** 属性的值设置为你之前在本实验室中记录的名为 **images** 的 Azure 存储 Blob 容器的 **URL** 属性来更新该值。

1.  保存 **appsettings.json** 文件。

#### 任务 4：验证 Web 应用程序

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter，将终端上下文切换到 **AdventureWorks.Web** 文件夹：

    ```
    cd .\AdventureWorks.Web\
    ```

1.  在命令提示符处，输入以下命令并按 Enter，运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：**dotnet run** 命令将自动生成对项目的更改，然后在不连接调试程序的情况下启动 Web 应用程序。此命令将输出正在运行的应用程序和所有已分配端口的 URL。

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，浏览到当前正在运行的 Web 应用程序 (<http://localhost:5000>)。

1.  在 Web 应用程序中，查看首页上显示的模型列表。

1.  找到 **“水壶”** 模型并选择 **“查看详细信息”**。

1.  在 **“水壶”** 产品详细信息页面上，找到 **“添加到购物车”**，可以看到结账功能当前处于禁用状态。

1.  关闭显示 Web 应用程序的浏览器窗口。

1.  返回到 **“Visual Studio Code”** 窗口，然后选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，你配置了 ASP.NET Web 应用程序，以连接到 Azure 中的资源。

### 练习 4：将 SQL 数据迁移到 Azure Cosmos DB

#### 任务 1：创建迁移项目

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter，在同名文件夹中创建一个名为 **AdventureWorks.Migrate** 的新 .NET 控制台项目：

    ```
    dotnet new console --name AdventureWorks.Migrate
    ```

    > **备注**：**dotnet new** 命令将在与项目同名的文件夹中创建一个新的 **“控制台”** 项目。

1.  在命令提示符处，输入以下命令并按 Enter，添加对现有 **AdventureWorks.Models** 项目的引用：

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Models\AdventureWorks.Models.csproj
    ```

    > **备注**：**dotnet add reference** 命令将添加对 **AdventureWorks.Models** 项目中包含的模型类的引用。

1.  在命令提示符处，输入以下命令并按 Enter，添加对现有 **AdventureWorks.Context** 项目的引用：

    ```
    dotnet add .\AdventureWorks.Migrate\AdventureWorks.Migrate.csproj reference .\AdventureWorks.Context\AdventureWorks.Context.csproj
    ```

    > **备注**：**dotnet add reference** 命令将添加对 **AdventureWorks.Context** 项目中包含的上下文类的引用。

1.  在命令提示符处，输入以下命令并按 Enter，将终端上下文切换到 **AdventureWorks.Migrate** 文件夹：

    ```
    cd .\AdventureWorks.Migrate\
    ```

1.  在命令提示符处，输入以下命令并按 Enter，从 NuGet 导入 2.2.6 版本的 **Microsoft.EntityFrameworkCore.SqlServer**：

    ```
    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 3.0.1
    ```

    > **备注**：**dotnet add package** 命令将从 **NuGet** 添加 **Microsoft.EntityFrameworkCore.SqlServer** 包。有关更多信息，请转到：[Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/3.0.1)。

1.  在命令提示符处，输入以下命令并按 Enter，从 NuGet 导入 3.4.1 版本的 **Microsoft.Azure.Cosmos**：

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.4.1
    ```

    > **备注**：**dotnet add package** 命令将从 **NuGet** 添加 **Microsoft.Azure.Cosmos** 包。有关更多信息，请转到：[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.4.1)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET 控制台应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：创建 .NET 类 

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **AdventureWorks.Migrate** 项目。

1.  打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡中，删除现有文件中的所有代码。

1.  添加以下代码行，从引用的 **AdventureWorks.Models** 和 **AdventureWorks.Context** 项目中导入 **AdventureWorks.Models** 和 **AdventureWorks.Context** 命名空间：

    ```
    using AdventureWorks.Context;
    using AdventureWorks.Models;
    ```

1.  添加以下代码行，通过从 NuGet 导入的 **Microsoft.Azure.Cosmos** 包导入 **Microsoft.Azure.Cosmos** 命名空间：

    ```
    using Microsoft.Azure.Cosmos;
    ```

1.  添加以下代码行，通过从 NuGet 导入的 **Microsoft.EntityFrameworkCore.SqlServer** 包导入 **Microsoft.EntityFrameworkCore** 命名空间：

    ```
    using Microsoft.EntityFrameworkCore;
    ```

1.  添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  输入以下代码，创建一个新的 **Program** 类：

    ```
    public class Program
    {
    }
    ```

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **sqlDBConnectionString** 的新字符串常量：

    ```
    private const string sqlDBConnectionString = "";
    ```

1.  通过将 **sqlDBConnectionString** 字符串常量的值设置为你之前在本实验室中记录的 SQL 数据库的 **ADO.NET（SQL 身份验证）连接字符串**来更新该字符串常量。

    > **备注**：请务必在此处使用更新后的连接字符串。从门户复制的原始连接字符串将不具有连接到 SQL 数据库所需的用户名和密码。

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **cosmosDBConnectionString** 的新字符串常量： 

    ```
    private const string cosmosDBConnectionString = "";
    ```

1.  通过将 **cosmosDBConnectionString** 字符串常量的值设置为你之前在本实验室中记录的 Azure Cosmos DB 帐户的 **“主连接字符串”** 来更新该字符串常量。

1.  在 **Program** 类中，输入以下代码以创建新的异步 **Main** 方法：

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  在 **Main** 方法中，添加以下代码行以向控制台输出介绍性消息：

    ```
    await Console.Out.WriteLineAsync("Start Migration");
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以将终端上下文切换到 **AdventureWorks.Migrate** 文件夹：

    ```
    cd .\AdventureWorks.Migrate\
    ```

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET 控制台应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 3：使用实体框架获取 SQL 数据库记录

1.  在 **Program.cs** 文件中的 **Program** 类的 **Main** 方法中，添加以下代码行以创建 **AdventureWorksSqlContext** 类的新实例，并传入 *sqlDBConnectionString* 变量作为连接字符串值：

    ```
    using AdventureWorksSqlContext context = new AdventureWorksSqlContext(sqlDBConnectionString);
    ```

1.  在 **Main** 方法中，添加以下代码块以发出语言集成查询 (LINQ)，从而从数据库中获取所**有模**型和子**产品**，并将其存储在内存中的 **List<>** 集合中：

    ```
    List<Model> items = await context.Models
        .Include(m => m.Products)
        .ToListAsync<Model>();
    ```

1.  在 **Main** 方法中，添加以下代码行，以打印从 SQL 数据库导入的记录数：

    ```
    await Console.Out.WriteLineAsync($"Total Azure SQL DB Records: {items.Count}");
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以将终端上下文切换到 **AdventureWorks.Migrate** 文件夹：

    ```
    cd .\AdventureWorks.Migrate\
    ```
    
1.  在命令提示符处，输入以下命令并按 Enter，构建 .NET 控制台应用程序：

    ```
    dotnet build
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Migrate** 文件夹中的 **Program.cs** 文件。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 4：将项插入 Azure Cosmos DB

1.  在 **Program.cs** 文件中的 **Program** 类的 **Main** 方法中，添加以下代码行以创建 **CosmosClient** 类的新实例，并传入 *cosmosDBConnectionString* 变量作为连接字符串值：

    ```
    using CosmosClient client = new CosmosClient(cosmosDBConnectionString);
    ```

1.  如果 Azure Cosmos DB 帐户中还没有名为 **Retail** 的**数据库**，在 **Main** 方法中添加以下代码行，以创建该数据库：

    ```
    Database database = await client.CreateDatabaseIfNotExistsAsync("Retail");
    ```

1.  如果 Azure Cosmos DB 帐户中还没有名为 **Online** 的**容器**，在 **Main** 方法中添加以下代码块，以创建该容器，其分区键路径为 **/Category**，吞吐量为 **1000** 个请求单位：

    ```
    Container container = await database.CreateContainerIfNotExistsAsync("Online",
        partitionKeyPath: $"/{nameof(Model.Category)}",
        throughput: 1000
    );
    ```

1.  在 **Main** 方法中，添加以下代码行，创建一个名为 **count** 的 *int* 变量：

    ```
    int count = 0;
    ```

1.  在 **Main** 方法中，添加以下代码块，创建一个 **foreach** 循环用于循环访问 **items** 集合中的对象：

    ```
    foreach (var item in items)
    {
    }
    ```

1.  在 **Main** 方法的 **foreach** 循环中，添加以下代码行，以**将**对象更新插入 Azure Cosmos DB 集合，并将结果保存在名为 **document** 且类型为 *ItemResponse<>* 的变量中：

    ```
    ItemResponse<Model> document = await container.UpsertItemAsync<Model>(item);
    ```

1.  在 **Main** 方法中包含的 **foreach** 循环中，添加以下代码行，以打印每个 upsert 操作的活动 ID：

    ```
    await Console.Out.WriteLineAsync($"Upserted document #{++count:000} [Activity Id: {document.ActivityId}]");
    ```

1.  返回到 **Main** 方法中（在 **foreach** 循环之外），添加以下代码行，以打印导出到 Azure Cosmos DB 的文档数：

    ```
    await Console.Out.WriteLineAsync($"Total Azure Cosmos DB Documents: {count}");
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以将终端上下文切换到 **AdventureWorks.Migrate** 文件夹：

    ```
    cd .\AdventureWorks.Migrate\
    ```
    
1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET 控制台应用程序：

    ```
    dotnet build
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Migrate** 文件夹中的 **Program.cs** 文件。

#### 任务 5：执行迁移

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以运行 .NET 控制台应用程序：

    ```
    dotnet run
    ```

    > **备注**：**dotnet run** 命令将启动控制台应用程序。

1.  查看输出到屏幕上的各种数据，其中包括初始 SQL 记录计数、单个更新插入活动标识符以及最终 Azure Cosmos DB 文档计数。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 6：验证迁移

1.  使用 Azure 门户返回到 **Microsoft Edge** 浏览器窗口。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“PolyglotData”** 资源组。

1.  在 **“PolyglotData”** 边栏选项卡中，选择你之前在本实验室中创建的 **polycosmos*[yourname]*** Azure Cosmos DB 帐户。

1.  在 **Azure Cosmos DB 帐户**边栏选项卡中，查找并选择边栏选项卡中的 **“数据资源管理器”** 链接。

1.  在“数据资源管理器”窗格中，展开 **“零售”** 数据库节点。

1.  展开 **“Online”** 容器节点，然后选择 **“新建 SQL 查询”**。

    > **备注**：此选项的标签可能会隐藏。可以通过将鼠标悬停在“数据资源管理器”窗格的图标上来查看标签。

1.  在“查询”选项卡中，输入以下文本：

    ```
    SELECT * FROM models
    ```

1.  选择 **“执行查询”**，然后查看查询返回的 JSON 模型列表。

1.  返回查询编辑器，将现有文本替换为以下文本：

    ```
    SELECT VALUE COUNT(1) FROM models
    ```

1.  选择 **“执行查询”**，然后查看 **COUNT** 聚合操作的结果。

1.  返回到 **“Visual Studio Code”** 窗口。

#### 回顾

在本练习中，你使用了 Entity Framework 和用于 Azure Cosmos DB 的 .NET SDK 将数据从 SQL 数据库迁移到了 Azure Cosmos DB。

### 练习 5：使用 .NET 访问 Azure Cosmos DB

#### 任务 1：使用 Cosmos SDK 和引用来更新库

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以将终端上下文切换到 **AdventureWorks.Context** 文件夹：

    ```
    cd .\AdventureWorks.Context\
    ```

1.  在命令提示符处，输入以下命令，然后按 Enter 以从 NuGet 导入 **Microsoft.Azure.Cosmos**：

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.4.1
    ```

    > **备注**：**dotnet add package** 命令将从 **NuGet** 添加 **Microsoft.Azure.Cosmos** 包。有关更多信息，请转到：[Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos/3.4.1)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：编写 .NET 代码，以连接到 Azure Cosmos DB

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **AdventureWorks.Context** 项目。

1.  通过快捷方式或者右键单击或激活快捷方式菜单进入 **“AdventureWorks.Context”** 文件夹节点，然后选择 **“新建文件”**。

1.  在新文件提示符处，输入 **“AdventureWorksCosmosContext.cs”**。

1.  在 **AdventureWorksCosmosContext.cs** 文件的代码编辑器选项卡中，添加以下代码行，以从引用的 **AdventureWorks.Models** 项目中导入 **AdventureWorks.Models** 命名空间：

    ```
    using AdventureWorks.Models;
    ```

1.  添加以下代码行，通过从 NuGet 导入的 **Microsoft.Azure.Cosmos** 包导入 **Microsoft.Azure.Cosmos** 和 **Microsoft.Azure.Cosmos.Linq** 命名空间：

    ```
    using Microsoft.Azure.Cosmos;
    using Microsoft.Azure.Cosmos.Linq;
    ```

1.  添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  输入以下代码，以添加 **AdventureWorks.Context** 命名空间块：

    ```
    namespace AdventureWorks.Context
    {
    }
    ```

1.  在 **AdventureWorks.Context** 命名空间中，输入以下代码以创建新的 **AdventureWorksCosmosContext** 类：

    ```
    public class AdventureWorksCosmosContext
    {
    }
    ```

1.  通过添加表示此类将实现 **IAdventureWorksProductContext** 接口的说明来更新 **AdventureWorksCosmosContext** 类的声明：

    ```
    public class AdventureWorksCosmosContext : IAdventureWorksProductContext
    {
    }
    ```

1.  在 **AdventureWorksCosmosContext** 类中，输入以下代码行，创建一个名为 *container* 的新的只读 **_Container** 变量：

    ```
    private readonly Container _container;
    ```

1.  在 **AdventureWorksCosmosContext** 类中，添加一个使用以下签名的新构造函数：

    ```
    public AdventureWorksCosmosContext(string connectionString, string database = "Retail", string container = "Online")
    {
    }
    ```

1.  在构造函数中，添加以下代码块以创建 **CosmosClient** 类的新实例，然后从客户端获取 **“数据库”** 和 **“容器”** 实例：

    ```
    _container = new CosmosClient(connectionString)
        .GetDatabase(database)
        .GetContainer(container);
    ```

1.  在 **AdventureWorksCosmosContext** 类中，添加一个使用以下签名的新 **FindModelAsync** 方法：

    ```
    public async Task<Model> FindModelAsync(Guid id)
    {
    }
    ```

1.  在 **FindModelAsync** 方法中，添加以下代码块以创建一个 LINQ 查询，将其转换为迭代器，循环访问结果集，然后返回结果集中的单个项：

    ```
    var iterator = _container.GetItemLinqQueryable<Model>()
        .Where(m => m.id == id)
        .ToFeedIterator<Model>();

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  在 **AdventureWorksCosmosContext** 类中，添加一个使用以下签名的新 **GetModelsAsync** 方法：

    ```
    public async Task<List<Model>> GetModelsAsync()
    {
    }
    ```

1.  在 **GetModelsAsync** 方法中，添加以下代码块，以运行 SQL 查询，获取查询结果迭代器，循环访问结果集，然后返回所有结果的并集：

    ```
    string query = $@"SELECT * FROM items";

    var iterator = _container.GetItemQueryIterator<Model>(query);

    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches;
    ```

1.  在 **AdventureWorksCosmosContext** 类中，添加一个使用以下签名的新 **FindProductAsync** 方法：

    ```
    public async Task<Product> FindProductAsync(Guid id)
    {
    }
    ```

1.  在 **FindProductAsync** 方法中，添加以下代码块，以运行 SQL 查询，获取查询结果迭代器，循环访问结果集，然后返回结果集中的单个项：

    ```
    string query = $@"SELECT VALUE products
                        FROM models
                        JOIN products in models.Products
                        WHERE products.id = '{id}'";

    var iterator = _container.GetItemQueryIterator<Product>(query);

    List<Product> matches = new List<Product>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }

    return matches.SingleOrDefault();
    ```

1.  保存 **AdventureWorksCosmosContext.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以将终端上下文切换到 **AdventureWorks.Context** 文件夹：

    ```
    cd .\AdventureWorks.Context\
    ```
    
1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

    > **备注**：如果出现任何生成错误，请查看 **Allfiles (F):\\Allfiles\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Context** 文件夹中的 **AdventureWorksCosmosContext.cs** 文件。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 3：更新 Azure Cosmos DB 连接字符串

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **AdventureWorks.Web** 项目。

1.  打开 **appsettings.json** 文件。

1.  在 JSON 对象的第 4 行中，找到 **ConnectionStrings.AdventureWorksCosmosContext** 路径。注意当前值为空：

    ```
    "ConnectionStrings": {
        ...
        "AdventureWorksCosmosContext": "",
        ...
    },
    ```

1.  通过将 **AdventureWorksCosmosContext** 属性的值设置为你之前在本实验室中记录的 Azure Cosmos DB 帐户的 **“主连接字符串”** 来更新该值。

1.  保存 **appsettings.json** 文件。

#### 任务 4：更新 .NET 应用程序启动逻辑

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **AdventureWorks.Web** 项目。

1.  打开 **Startup.cs** 文件。

1.  在 **Startup** 类中，找到现有的 **ConfigureProductService** 方法：

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksProductContext, AdventureWorksSqlContext>(provider =>
            new AdventureWorksSqlContext(
                _configuration.GetConnectionString(nameof(AdventureWorksSqlContext))
            )
        );
    }
    ```

    > **备注**：当前产品服务使用 SQL 作为其数据库。

1.  在 **ConfigureProductService** 方法中，删除现有的所有代码行：

    ```
    public void ConfigureProductService(IServiceCollection services)
    {
    }
    ```

1.  在 **ConfigureProductService** 方法中，添加以下代码块，以将产品提供程序更改为之前在本实验室中创建的 **AdventureWorksCosmosContext** 实现：

    ```
    services.AddScoped<IAdventureWorksProductContext, AdventureWorksCosmosContext>(provider =>
        new AdventureWorksCosmosContext(
            _configuration.GetConnectionString(nameof(AdventureWorksCosmosContext))
        )
    );
    ```

1.  保存 **Startup.cs** 文件。

#### 任务 5：验证 .NET 应用程序是否成功连接到 Azure Cosmos DB

1.  在 **“Visual Studio Code”** 窗口中，通过快捷方式或者右键单击或激活快捷方式菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter，将终端上下文切换到 **AdventureWorks.Web** 文件夹：

    ```
    cd .\AdventureWorks.Web\
    ```

1.  在命令提示符处，输入以下命令，然后按 Enter 以运行 ASP.NET 应用程序：

    ```
    dotnet run
    ```

    > **备注**：**dotnet run** 命令将自动生成对项目的更改，然后在不连接调试程序的情况下启动 Web 应用程序。此命令将输出正在运行的应用程序和所有已分配端口的 URL。

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，浏览到当前正在运行的 Web 应用程序 (<http://localhost:5000>)。

1.  在 Web 应用程序中，查看首页上显示的模型列表。

1.  找到 **Touring-1000** 模型，并选择 **“查看详细信息”**。

1.  在 **“Touring-1000”** 产品详细信息页面上，执行以下操作：

    1.  在 **“选择选项”** 列表中，选择 **“Touring-1000 Yellow, 50, $2,384.07”**。
    
    1.  找到 **“添加到购物车”**，你会发现结帐功能仍处于禁用状态。

1.  关闭显示 Web 应用程序的浏览器窗口。

1.  返回到 **“Visual Studio Code”** 窗口，然后选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，你编写了 C# 代码以使用 .NET SDK 查询 Azure Cosmos DB 集合。

### 练习 6：清理订阅 

#### 任务 1：打开 Azure Cloud Shell

1.  在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    
    1.  对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。
    
    > **备注**：等待 Cloud Shell 完成其初始设置过程后，再继续本实验室。如果没有看到 Cloud Shell 配置选项，很可能是因为你正在使用本课程实验室中的现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1.  在命令提示符处，输入以下命令，然后按 Enter 以删除 **PolyglotData** 资源组：

    ```
    az group delete --name PolyglotData --no-wait --yes
    ```
    
1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动应用程序

1.  关闭当前正在运行的 Microsoft Edge 应用程序。

1.  关闭当前正在运行的 “Visual Studio Code” 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理订阅。
