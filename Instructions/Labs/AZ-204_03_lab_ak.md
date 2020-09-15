---
lab:
    title: '实验室：使用适用于 .NET 的 Azure 存储 SDK 检索 Azure 存储的资源和元数据'
    az204Module: '模块 03：开发使用 blob 存储的解决方案'
    az020Module: '模块 03：开发使用 blob 存储的解决方案'
    type: '参考答案'
---

# 实验室: 使用适用于 .NET 的 Azure 存储 SDK 检索 Azure 存储资源和元数据
# 学生实验室答案密钥

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不匹配。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。 **如果发生这种情况，请适应这些更改，并根据需要在实验中熟悉这些更改。**

## 说明

### 开始之前

#### 登录实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名： **管理员**

-   密码： **Pa55w.rd**

> **注意**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 评价已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

### 练习 1：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一个”**。

1.  输入你的 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **注意**：第一次登录 Azure 门户时，你会看到一个门户教程。选择 **“开始使用”**，以跳过教程并开始使用门户。

#### 任务 2：创建存储帐户

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡上，查找存储实例列表。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“添加”**。

1.  在 **“创建存储帐户”** 边栏选项卡上找到标签页，例如 **“基本”** 。

    > **注意**：每个标签页代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡上，执行以下操作：
    
    1.  将 **“订阅”** 文本框保留设置为默认值。

    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“StorageMedia”**，然后选择 **“确定”**。

    1.  在 **“存储帐户名称”** 文本框中，输入 **mediastor*[yourname]***。

    1.  在 **“位置”** 下拉列表中，选择 **“（美国）美国东部”** 区域。

    1.  在 **“性能”** 部分，选择 **“标准”**。

    1.  在 **“帐户类型”** 下拉列表中，选择 **“StorageV2（通用 v2）”**。

    1.  在 **“复制”** 下拉列表中，选择 **“读取访问异地冗余存储(RA-GRS)”**。

    1.  在 **“访问层”** 部分，确认已选择 **“热”**。

    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在上述步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建存储帐户。 

    > **注意**：等待创建任务完成，再继续本实验室。

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡，选择 **mediastor*[yourname]*** 存储帐户实例。

1.  在 **“存储帐户”** 边栏选项卡中，找到 **“设置”** 部分并选择 **“属性”** 链接。

1.  在 **“属性”** 部分，记录 **“主 Blob 服务终结点”** 文本框的值。

    > **注意**：你将在稍后的实验室中使用此值。

1.  仍然在 **“存储账户”** 边栏选项卡中，找到 **“设置”** 部分，然后选择 **“访问密钥”** 链接。

1.  在 **“访问密钥”** 部分中，执行以下操作：

    1.  在 **“存储帐户名”** 文本框中记录该值。
    
    1.  选择任一密钥，然后将值记录在 **“密钥”** 框中。

    > **注意**：所有这些值稍后将在本实验室中使用。

#### 回顾

在本练习中，你创建了将用于本实验室其余部分的新存储帐户。

### 练习 2：将 blob 上载到容器中

#### 任务 1：创建存储帐户容器

1.  在 Azure 门户的 **“导航”窗口，选择“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“StorageMedia”** 资源组。

1.  在 **“StorageMedia”** 边栏选项卡中，选择你之前在本实验室中创建的 **mediastor*[yourname]*** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“+ 容器”**。

1.  在 **“新建容器”** 弹出窗口中，执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **raster-graphics**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“专用（非匿名访问）”**，然后单击 **“确认”**。

1.  回到 **“容器”** 部分中，选择 **“+ 容器”**。

1.  在 **“新建容器”** 弹出窗口中，执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **compressed-audio**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“专用（非匿名访问）”**，然后单击 **“确认”**。

1.  在 **“容器”** 部分中，查看容器更新列表。

#### 任务 2：上传存储帐户 blob

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“StorageMedia”** 资源组。

1.  在 **“StorageMedia”** 边栏选项卡中，选择你之前在本实验室中创建的 **mediastor*[yourname]*** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分中，选择最近创建的 **“raster-graphics”** 容器。

1.	在 **“容器”** 边栏选项卡中，选择 **“上传”**。

1.	在 **“上传 blob”** 窗口中，执行以下操作：

    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。

    1.  在 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\Images**，选择 **graph.jpg** 文件，然后选择 **“打开”**。

    1.  确保选中 **“如果文件存储已经存在，则覆盖”** 复选框，然后选择 **“上传”**。 
    
    > **注意**：等待 blob 上传完成，然后再继续本实验室。

#### 回顾

在本练习中，你在存储帐户中创建了几个占位符容器，并在其中一个容器中填充了一个 blob。

### 练习 3：使用 .NET SDK 访问容器

#### 任务 1：创建 .NET 项目

1.  在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。

1.  在 **“文件”** 菜单上，选择 **“打开文件夹”**。

1.  在打开的 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\BlobManager**，然后选择 **“选择文件夹”**。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开命令提示符中输入以下命令，然后选择“Enter”在当前文件夹中创建一个名为 **BlobManager** 的 .NET 项目：

    ```
    dotnet new console --name BlobManager --output .
    ```

    > **注意**： **“dotnet new”** 命令将在与项目同名的文件夹中创建一个新的 **“控制台”** 项目。

1.  在命令提示符中，输入以下命令并按 Enter 键，然后从 NuGet 导入 12.0.0 版本的 **Azure.Storage.Blobs**：

    ```
    dotnet add package Azure.Storage.Blobs --version 12.0.0
    ```

    > **注意**： **dotnet add package** 命令将从 NuGet 添加 **Azure.Storage.Blobs** 包。有关详细信息，请转到 [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.0.0)。

1.  在命令提示符中，输入以下命令并按 “Enter”，以构建 .NET Core Web 应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：修改程序类以访问存储

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，展开 **“Program.cs”** 文件。

1.  在 **“Program.cs”** 文件的代码编辑器选项卡中，删除现有文件中的所有代码。

1.  添加以下代码行，从 **Azure.Storage.Blobs** 包（从 NuGet 中导入）中导入 **Azure.Storage**、 **Azure.Storage.Blobs** 和 **Azure.Storage.Blobs.Models** 命名空间：

    ```
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    ```
    
1.  添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```
    using System;
    using System.Threading.Tasks;
    ```

1.  输入以下代码，创建一个新的 **Program** 类：

    ```
    public class Program
    {
    }
    ``` 

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **blobServiceEndpoint** 的新字符串常量：

    ```
    private const string blobServiceEndpoint = "";
    ```

1.  通过将 **“blobServiceEndpoint”** 字符串常量的值设置为之前在本实验中记录的存储帐户的 **“主 Blob 服务终结点”** 来更新该字符串常量。

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **storageAccountName** 的新字符串常量：

    ```
    private const string storageAccountName = "";
    ```

1.  通过将 **“storageAccountName”** 字符串常数的值设置为之前在本实验室中记录的存储帐户的 **“存储帐户名称”** 来更新该字符串常量。

1.  在 **Program** 类中，输入以下代码行，创建一个名为 **storageAccountKey** 的新字符串常量：

    ```
    private const string storageAccountKey = "";
    ```

1.  通过将 **storageAccountKey** 字符串常量的值设置为之前在本实验室中记录的存储帐户的 **密钥** 来更新该字符串常量。

1.  在 **“Program”** 类中，输入以下代码以创建新的异步 **“Main”** 方法：

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  查看 **“Program.cs”** 文件，现在应包括：

    ```
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    using System;
    using System.Threading.Tasks;

    公共类程序
    {
        private const string blobServiceEndpoint = "<primary-blob-service-endpoint>";
        private const string storageAccountName = "<storage-account-name>";
        private const string storageAccountKey = "<key>";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 任务 3：连接到 Azure 存储 Blob 服务终结点

1.  在 **Main** 方法中，使用 **storageAccountName** 和 **storageAccountKey** 常量作为构造函数参数，添加以下代码行，创建新的 **StorageSharedKeyCredential** 实例：

    ```
    StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
    ```

1.  在 **Main** 方法中，使用 **blobServiceEndpoint** 常量和 *accountCredentials* 变量作为构造函数参数添加以下代码行，创建新的 **BlobServiceClient** 类实例：

    ```
    BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
    ```

1.  在 **Main** 方法中，添加以下代码行，调用 **BlobServiceClient** 类的 **GetAccountInfoAsync** 方法，从服务中检索帐户元数据：

    ```
    AccountInfo info = await serviceClient.GetAccountInfoAsync();
    ```
    
1.  在 **Main** 方法中，添加以下代码行，呈现欢迎消息：

    ```
    await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
    ```
    
1.  在 **“Main”** 方法中，添加以下代码行，以呈现存储帐户名称：

    ```
    await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
    ```
    
1.  在 **Main** 方法中，添加以下代码行以呈现存储帐户类型：

    ```
    await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
    ```
    
1.  在 **“Main”** 方法中，添加以下代码行，以呈现当前为存储帐户选择的库存单位 (SKU)：

    ```
    await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    ```

1.  查看 **Main** 方法，现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);	

        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);

        AccountInfo info = await serviceClient.GetAccountInfoAsync();

        await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
        await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
        await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
        await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按“Enter”键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **注意**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager”** 文件夹中的 **Program.cs** 文件。

1.  观察当前运行的控制台应用程序的输出。输出包含从服务中检索到的存储帐户的元数据。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 4：枚举现有容器

1.  在 **Program** 类中，输入以下代码，创建名为 **EnumerateContainersAsync** 的新 **private static** 异步方法，该方法只有一个 **BlobServiceClient** 参数类型：

    ```
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
    }
    ```

1.  在 **EnumerateContainersAsync** 方法中，输入以下代码，创建异步 **foreach** 循环，对 **BlobServiceClient** 类的 **GetBlobContainersAsync** 方法的调用结果进行迭代：

    ```
    await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
    {
    }
    ```

1.  在 **foreach** 循环中，输入以下代码，打印每个容器的名称：

    ```
    await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
    ```

1.  观察 **EnumerateContainersAsync** 方法，现在包括：

    ```
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
        await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
        {
            await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
        }
    }
    ```

1.  在 **Main** 方法中，请在方法末尾输入以下代码，调用 **EnumerateContainersAsync** 方法，传入 *serviceClient* 变量作为参数：

    ```
    await EnumerateContainersAsync(serviceClient);
    ```

1.  查看 **Main** 方法，现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        \\ 为简洁起见，删除了现有代码
        
        await EnumerateContainersAsync(serviceClient);
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或通过快捷菜单进入“资源管理器”窗格，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按“Enter”键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **注意**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager”** 文件夹中的 **Program.cs** 文件。

1.  观察当前运行的控制台应用程序的输出。更新后的输出包括帐户中每个现有容器的列表。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，使用 Azure 存储 SDK 访问现有容器。 

### 练习 4：使用 .NET SDK 检索 blob 统一资源标识符 (URI) 

#### 任务 1：使用 SDK 枚举现有容器中的 blob

1.  在 **Program** 类中，输入以下代码，以创建名为 **EnumerateBlobsAsync** 的新 **private static** 异步方法，该方法具有两种参数类型，即 **BlobServiceClient** 和 **string**：

    ```
    private static async Task EnumerateBlobsAsync(BlobServiceClient client, string containerName)
    {      
    }
    ```

1.  在 **EnumerateBlobsAsync** 方法中，输入以下代码，使用 **BlobContainerClient** 类的 **GetBlobContainerClient** 方法获取 **BlobServiceClient** 类的新实例，并传入 **containerName** 参数：

    ```
    BlobContainerClient container = client.GetBlobContainerClient(containerName);
    ```

1.  在 **EnumerateBlobsAsync** 方法中，输入以下代码，将呈现枚举容器的名称：

    ```
    await Console.Out.WriteLineAsync($"Searching:\t{container.Name}");
    ```

1.  在 **“EnumerateBlobsAsync”** 方法中，输入以下代码，以创建异步 **foreach** 循环，该循环对 **“BlobContainerClient”** 类的 **“GetBlobsAsync”** 方法的调用结果进行循环访问：

    ```
    await foreach (BlobItem blob in container.GetBlobsAsync())
    {        
    }
    ```

1.  在 **foreach** 循环中，输入以下代码，以打印每个 Blob 的名称：

    ```
     await Console.Out.WriteLineAsync($"Existing Blob:\t{blob.Name}");
    ```

1.  查看 **EnumerateBlobsAsync** 方法，现在包括：

    ```
    private static async Task EnumerateBlobsAsync(BlobServiceClient client, string containerName)
    {      
        BlobContainerClient container = client.GetBlobContainerClient(containerName);
        
        await Console.Out.WriteLineAsync($"Searching:\t{container.Name}");
        
        await foreach (BlobItem blob in container.GetBlobsAsync())
        {        
             await Console.Out.WriteLineAsync($"Existing Blob:\t{blob.Name}");
        }
    }
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，创建一个名为 *existingContainerName* 的变量，值为 **raster-graphics**：

    ```
    string existingContainerName = "raster-graphics";
    ```

1.  在 **“Main”** 方法中，在方法末尾输入以下代码，调用 **“EnumerateBlobsAsync”** 方法，传入 *“serviceClient”* 和 *“existingContainerName”* 变量作为参数：

    ```
    await EnumerateBlobsAsync(serviceClient, existingContainerName);
    ```

1.  查看 **Main** 方法，现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        \\ 为简洁起见，删除了现有代码
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
    }
    ```

1.  保存 **“Program.cs”** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按“Enter”键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **注意**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager”** 文件夹中的 **Program.cs** 文件。

1.  观察当前运行的控制台应用程序的输出。更新后的输出包括有关现有容器和 blob 的元数据。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：使用 SDK 创建新容器

1.  在 **“程序”** 类中输入以下代码，创建名为 **“GetContainerAsync”** 的新 **“专用静态”** 异步方法，该方法有两种参数类型， 即 **“BlobServiceClient”** 和 **“string”**：

    ```
    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName)
    {      
    }
    ```

1.  在 **GetContainerAsync** 方法中，输入以下代码，使用 **BlobServiceClient** 类的 **GetBlobContainerClient** 方法获取 **BlobContainerClient** 类新实例，并传入 **containerName** 参数：

    ```
    BlobContainerClient container = client.GetBlobContainerClient(containerName);
    ```

1.  在 **GetContainerAsync** 方法中，输入以下代码，调用 **BlobContainerClient** 类的 **CreateIfNotExistsAsync** 方法：

    ```
    await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
    ```

1.  在 **“GetContainerAsync”** 方法中输入以下代码，呈现可能创建的容器的名称：

    ```
    await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
    ```

1.  在 **GetContainerAsync** 方法中，输入以下代码，返回名为 **container** 的 **BlobContainerClient** 类新实例，作为 **GetContainerAsync** 方法的结果：

    ```
    退回容器；
    ```  

1.  观察 **GetContainerAsync** 方法，现在应包括：

    ```
    private static async Task<BlobContainerClient> GetContainerAsync(BlobServiceClient client, string containerName)
    {      
        BlobContainerClient container = client.GetBlobContainerClient(containerName);
        
        await container.CreateIfNotExistsAsync(PublicAccessType.Blob);
        
        await Console.Out.WriteLineAsync($"New Container:\t{container.Name}");
        
        退回容器；
    }
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，创建一个名为 *newContainerName* 的变量，值为 **vector-graphics**：

    ```
    string newContainerName = "vector-graphics";
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，调用 **GetContainerAsync** 方法，传入 *serviceClient* 和 *newContainerName* 变量作为参数，并将结果存储在名为 *containerClient* 的 **BlobContainerClient** 类变量中：

    ```
    BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
    ```

1.  查看 **Main** 方法，现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        \\ 为简洁起见，删除了现有代码
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
        
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按“Enter”键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **注意**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager”** 文件夹中的 **Program.cs** 文件。

1.  观察当前运行的控制台应用程序的输出。更新后的输出包括有关现有容器和 blob 的元数据。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 3：使用门户上传新 blob

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“StorageMedia”** 资源组。

1.  在 **“StorageMedia”** 边栏选项卡中，选择你之前在本实验室中创建的 **mediastor*[yourname]*** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分中，选择新创建的 **vector-graphics** 容器。

1.	在 **“容器”** 边栏选项卡中，选择 **“上传”**。

1.	在 **“上传 blob”** 窗口中，执行以下操作：

    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。

    1.  在 **“文件资源管理器”** 窗口中，转到 **Allfiles (F):\\Allfiles\\Labs\\03\\Starter\\Images**，选择 **graph.svg** 文件，然后选择 **“打开”**。

    1.  确保选中 **“如果文件存储已经存在，则覆盖”** 复选框，然后选择 **“上传”**。 
    
    > **注意**：等待 blob 上传完成，然后再继续本实验室。

#### 任务 4：使用 SDK 访问 blob URI

1.  在 **Program** 类中，输入以下代码，创建名为 **GetBlobAsync** 的新 **private static** 异步方法。该方法具有两种参数类型，即 **BlobContainerClient** 和 **string**：

    ```
    private static async Task<BlobClient> GetBlobAsync(BlobContainerClient client, string blobName)
    {      
    }
    ```

1.  在 **GetBlobAsync** 方法中，输入以下代码，使用 **BlobContainerClient** 类的 **GetBlobClient** 方法获取 **BlobClient** 类的新实例，并传入 **blobName** 参数：

    ```
    BlobClient blob = client.GetBlobClient(blobName);
    ```

1.  在 **GetBlobAsync** 方法中，输入以下代码，呈现所引用的 blob 的名称：

    ```
    await Console.Out.WriteLineAsync($"Blob Found:\t{blob.Name}");
    ```

1.  在 **GetBlobAsync** 方法中，输入以下代码，返回名为 **blob** 的 **BlobClient** 类实例，作为 **GetBlobAsync** 方法的结果：

    ```
    return blob;
    ```

1.  观察 **GetBlobAsync** 方法，现在包括：

    ```
    private static async Task<BlobClient> GetBlobAsync(BlobContainerClient client, string blobName)
    {      
        BlobClient blob = client.GetBlobClient(blobName);
        await Console.Out.WriteLineAsync($"Blob Found:\t{blob.Name}");
        return blob;
    }
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，创建一个名为 *uploadBlobName* 的变量，值为 **graph.svg**：

    ```
    string uploadedBlobName = "graph.svg";
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，调用 **GetBlobAsync** 方法，传入 *containerClient* 和 *uploadBlobName* 变量作为参数，并将结果存储在名为 *blobClient* 的 **BlobClient** 类变量中：

    ```
    BlobClient blobClient = await GetBlobAsync(containerClient, uploadedBlobName);
    ```

1.  在 **Main** 方法中，在方法末尾输入以下代码，呈现 *blobClient* 变量的 **Uri** 属性：

    ```
    await Console.Out.WriteLineAsync($"Blob Url:\t{blobClient.Uri}");
    ```

1.  查看 **Main** 方法，现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        \\ 为简洁起见，删除了现有代码
        
        await EnumerateContainersAsync(serviceClient);

        string existingContainerName = "raster-graphics";
        await EnumerateBlobsAsync(serviceClient, existingContainerName);
        
        string newContainerName = "vector-graphics";
        BlobContainerClient containerClient = await GetContainerAsync(serviceClient, newContainerName);
        
        string uploadedBlobName = "graph.svg";
        BlobClient blobClient = await GetBlobAsync(containerClient, uploadedBlobName);

        await Console.Out.WriteLineAsync($"Blob Url:\t{blobClient.Uri}");
    }
    ```

1.  保存 **Program.cs** 文件。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按“Enter”键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **注意**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\03\\Solution\\BlobManager”** 文件夹中的 **Program.cs** 文件。

1.  观察当前运行的控制台应用程序的输出。更新后的输出包括在线访问 blob 的最终 URL。记录本 URL 的值，以便稍后在本实验中使用：

    > **注意**：该 URL 可能类似于以下字符串： **https://mediastor*[yourname]*.blob.core.windows.net/vector-graphics/graph.svg**

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 5：使用浏览器测试该 URI

1.  在任务栏上，右键选择 **“Microsoft Edge”** 图标或激活快捷菜单，然后选择 **“新窗口”**。

1.  在新的浏览器窗口中，转到之前在本实验室中针对 Blob 复制的 URL。

1.  现在，应该在浏览器窗口中注意到可缩放矢量图形 (SVG) 文件。

#### 回顾

在本练习中，你使用存储 SDK 创建了容器并管理了 blob。 

### 练习 5：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在 Azure 门户的导航窗格，选择 **“Cloud Shell”** 图标，打开一个新的 shell 实例。

    > **注意**： **Cloud Shell** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，你可以使用 **欢迎来到 Azure Cloud Shell 向导** 来配置 Cloud Shell 的初次使用。在向导中执行以下操作：
    
    1.  对话框提示你在开始使用 shell 前，先新建一个存储帐户。接受默认设置并选择 **“创建存储”** 。 

    > **注意**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室内容。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1.  在命令提示符处，键入以下命令，然后按 Enter 键，删除 **StorageMedia** 资源组：

    ```
    az group delete --name StorageMedia --no-wait --yes
    ```
    
1.  关闭门户里的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1.     当前正在运行的 Microsoft Edge 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理了订阅。
