---
lab:
    title: '实验室：使用 Azure Functions 实现任务处理操作逻辑'
    module: '模块 02：实现 Azure Functions'
    type: '参考答案'
---

# 实验室: 使用 Azure Functions 实现任务处理逻辑
# 学生实验室答案密钥

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验说明和实验步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。 **如果发生这种情况，请适应这些更改，并根据需要在实验中熟悉这些更改。**

## 说明

### 开始前

#### 登录实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名： **管理员**

-   密码： **Pa55w.rd**

> **注意**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 评价已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

-   Windows 终端

### 练习 1 ：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一个”**。

1.  输入你的 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **注意**：第一次登录 Azure 门户时，你会看到一个门户教程。选择 **“开始使用”**，以跳过教程并开始使用门户。

#### 任务 2：创建 Azure 存储帐户

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡中，查看存储帐户实例列表。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“添加”**。

1.  在 **“创建存储帐户”** 边栏选项卡上，观察边栏选项卡上的选项卡，如 **“基本”**、 **“标记”** 和 **“查看 + 创建”**。

    > **注意**：每个标签页代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  选择 **“基本”** 选项卡，然后在选项卡区域内执行以下操作：
    
    1.  将 **“订阅”** 文本框保留设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“Serverless”**，然后选择 **“确定”**。
    
    1.  在 **“存储帐户名称”** 文本框中，输入 **funcstor*[yourname]***。
    
    1.  在 **“位置”** 列表中，选择 **“（美国）美国东部”** 区域。
    
    1.  在 **“性能”** 部分，选择 **“标准”**。
    
    1.  在 **“帐户类型”** 列表中，选择 **“StorageV2（通用 v2）”**。
    
    1.  在 **“复制”** 列表中，选择 **“本地冗余存储(LRS)”**。
    
    1.  在 **“访问层级(默认)”** 部分，确保选择 **“热”**。
    
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在之前步骤中指定的选项。

1.  选择 **“创建”**，使用指定的配置创建存储帐户。

    > **注意**：在 **“部署”** 边栏选项卡中，等待创建任务完成后再继续本实验。

#### 任务 3：创建 Azure Functions 应用

1.  在 Azure 门户的导航窗格中，选择到 **“创建资源”** 链接。

1.  来自 **新** 边栏选项卡，找到 **搜索市场** 文本框。

1.  在搜索文本框中，输入 **“函数”**，然后按 Enter 键。

1.  在 **“全部内容”** 搜索结果边栏选项卡中，选择 **“函数应用”** 结果。

1.  在 **“函数应用”** 边栏选项卡中，选择 **“创建”**。

1.  查看 **“函数应用”** 边栏选项卡的选项卡，例如 **“基本”**。

    > **注意**：每个选项卡都代表在工作流中新建函数应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本”** 选项卡上，执行以下操作：
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表选择 **“无服务器”**。
    
    1.  在 **“函数应用名称”** 文本框中，输入 **funclogic*[yourname]***。

    1.  在 **“发布”** 部分，选择 **“代码”**。

    1.  在 **“运行时堆栈”** 下拉列表中，选择 **“NET Core”**。

    1.  在 **“区域”** 下拉列表中，选择 **“美国东部”** 地区。
    
    1.  选择 **“下一步：托管”**。

1.  在 **“托管”** 标签页中，执行以下操作：

    1.  在 **“存储帐户”** 下拉列表中，选择你之前在本实验室中创建的 **funcstor*[yourname]*** 存储帐户。

    1.  在 **“操作系统”** 部分，选择 **“Windows”**。

    1.  在 **“计划类型”** 下拉列表中，选择 **“使用”** 选项。

    1.  选择 **“下一步：监控”**。

1.  在 **“监控”** 选项卡中，执行以下操作：

    1.  在 **“启用 Application Insights”** 部分，选择 **“否”**。

    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在上述步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建函数应用。 

    > **注意**：等待创建任务完成，再继续本实验室。

#### 回顾

在本练习中，你创建了本实验室所需的所有资源。

### 练习 2：创建被 HTTP 申请触发的函数

#### 任务 1：创建 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“函数应用”** 边栏选项卡中，选择 **“函数”** 下拉列表旁边的加号（ **+** ）。

1.  在 **“新建 Azure 函数”** 快速入门中，执行以下操作：
    
    1.  在 **“选择开发环境”** 标题下，选择 **“在门户”**，然后选择 **“继续”**。
    
    1.  在 **“创建函数”** 标题下，选择 **“更多模板”**，然后选择 **“完成并查看模板”**。
    
    1.  在模板列表中，选择 **“HTTP 触发器”**。
    
    1.  在 **“新函数”** 弹出窗口中，找到 **“名称”** 文本框并输入 **“Echo”**。
    
    1.  在 **“新建函数”** 弹出窗口中，找到 **“授权级别”** 列表并选择 **“匿名”**。
    
    1.  在 **“新建函数”** 弹出窗口中，选择 **“创建”**。

#### 任务 2：写入函数代码

1.  在函数编辑器中，观察示例 **“run.csx”** 函数脚本：

    ```
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
        name = name ?? data?.name;

        return name != null
            ? (ActionResult)new OkObjectResult($"Hello, {name}")
            : new BadRequestObjectResult("Please pass a name on the query string or in the request body");
    }
    ```

1.  删除所有示例代码。

1.  添加以下代码行以导入 **Microsoft.AspNetCore.Mvc** 命名空间：

    ```
    using Microsoft.AspNetCore.Mvc;
    ```

1.  添加以下代码行以导入 **“System.Net”** 命名空间：

    ```
    using System.Net;
    ```

1.  添加以下代码块以创建一个名为 **“Run”** 的新 **public static** 方法，该方法返回类型为 **IActionResult** 的变量，并且也接受 **HttpRequest** 和 **ILogger** 类型的变量作为参数，名为 *“req”* 和 *“log”*：

    ```
    public static IActionResult Run(HttpRequest req, ILogger log)
    {
    }
    ```

1.  在 **“Run”** 方法中，输入以下代码行以呈现一条固定消息：

    ```
    log.LogInformation("Received a request");
    ```

1.  输入以下代码行以将 HTTP 请求的正文作为 HTTP 响应进行回显：

    ```
    return new OkObjectResult(req.Body);
    ```

1.  查看 **“run.csx”** 文件，该文件现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static IActionResult Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("Received a request");

        return new OkObjectResult(req.Body);
    }
    ```

1.  选择 **“保存”** 以保存脚本。

#### 任务 3：在门户中测试函数运行

1.  选择 **“日志”**。

1.  观察编译结果。结果应包含 “编译成功” 的消息。

1.  选择 **“运行”** 以测试函数。

1.  观察运行测试的结果。结果应与原始请求正文完全一致。

#### 任务 4：获取基本函数 URL

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“函数应用”** 边栏选项卡中，复制 **“URL”** 文本框的值。你将在稍后的实验室中使用此值。

#### 任务 5：使用 httprepl 来测试函数运行

1.  在任务栏上，选择 **Windows Terminal** 图标。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 启动 **“httprepl”** 工具，将基础统一资源标识符 (URI) 设置为你之前在本实验室中复制的 URL 值。

    ```
    httprepl <function-app-url>
    ```

    > **注意**：例如，如果你的 URL 是 **https://funclogicstudent.azurewebsites.net**，则你的命令就是 **httprepl https://funclogicstudent.azurewebsites.net**。

1.  在工具提示下，输入以下命令，然后按 Enter 以浏览到相对的 **“api”** 目录：

    ```
    cd api
    ```

1.  输入以下命令，然后按 Enter 浏览到相对的 **“echo”** 目录：

    ```
    cd echo
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，该命令使用 **“--content”** 选项发送一条数值设为 **3** 的 HTTP 请求正文：

    ```
    发布 --内容 3
    ```

1.  输入以下命令，然后按 Enter 运行 **“post”** 命令，通过使用 **“--content”** 选项发送一条设为数值 **“5”** 的 HTTP 请求正文：

    ```
    发布 --内容 5
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，通过使用 **--content** 选项发送一条设为字符串值 **Hello** 的 HTTP 请求正文：

    ```
    post --content "Hello"
    ```

1.  输入以下命令，然后选择“Enter”运行 **“post”** 命令，发送一条设为 JavaScript 对象表示法 (JSON) 值 **{"msg": **的 HTTP 请求正文** 通过使用 **“--content”** 选项获得 **"Successful"**}** 结果：

    ```
    发布 --内容 "{"msg": "Successful"}"
    ```

1.  输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```
    exit
    ```

1.  关闭当前正在运行的 Windows Terminal 应用程序。

1.	返回 Azure 门户的浏览器窗口。

#### 回顾

在本练习中，你成功创建了一个基本函数。该函数可回响通过 HTTP POST 申请所发送的内容。

### 练习 3：创建一个按日程触发的函数

#### 任务 1：创建由日程触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“函数应用”** 边栏选项卡中，选择 **“函数”** 下拉列表旁边的加号（ **+** ）。

1.  在 **“新建 Azure 函数”** 快速入门中，执行以下操作：
        
    1.  在模板列表中，选择 **“计时器触发器”**。
    
    1.  在 **“新建函数”** 弹出窗口中，找到 **“名称”** 文本框并输入 **Recurring**。
    
    1.  在 **“新函数”** 弹出窗口中，找到 **“计划”** 文本框并输入 **“0 \* \* \* \* \”***。
    
    1.  在 **“新建函数”** 弹出窗口中，选择 **“创建”**。

#### 任务 2：观察函数运行

1.  在函数编辑器中，选择 **“保存”** 以保留默认的函数实现。

1.  选择 **“日志”**。

1.  观察函数运行，大约每分钟运行一次。每次运行函数都应向日志呈现一条简单的消息。

#### 任务 3：更新函数集成配置

1.  返回 **“函数应用”** 边栏选项卡，执行以下操作：

    1.  展开之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用的节点。

    1.  展开 **“函数”** 节点。

    1.  展开该特定函数的 **“重复”** 节点。

    1.  选择 **“集成”** 节点。

1.  在 **“集成”** 部分，执行以下操作：

    1.  选择 **“计时器”** 部分中的 **“计时器 (myTimer)”** 选项。

    1.  在 **“计划”** 文本框中输入值 **“\*/30 \* \* \* \* \*”**。

    1.  选择 **“保存”**。

#### 任务 4：观察函数运行

1.  返回 **“函数应用”** 边栏选项卡，执行以下操作：

    1.  展开之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用的节点。

    1.  展开 **“函数”** 节点。

    1.  选择该特定函数的 **“重复执行”** 节点。

1.  在函数编辑器中，选择 **“日志”**。

1.  观察现在大约每 30 秒发生一次的函数运行。每次运行函数都应向日志呈现一条简单的消息。

#### 回顾

在本练习中，你创建了一个按照固定日程自动运行的函数。

### 练习 4：创建与其他服务集成的函数

#### 任务 1：创建 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“函数应用”** 边栏选项卡中，选择 **“函数”** 下拉列表旁边的加号（ **+** ）。

1.  在 **“新建 Azure 函数”** 快速入门中，执行以下操作：
        
    1.  在模板列表中，选择 **“HTTP 触发器”**。
    
    1.  在 **“新函数”** 弹出窗口中，找到 **“名称”** 文本框并输入 **“GetSettingInfo”**。
    
    1.  在 **“新建函数”** 弹出窗口中，找到 **“授权级别”** 列表并选择 **“匿名”**。
    
    1.  在 **“新建函数”** 弹出窗口中，选择 **“创建”**。

#### 任务 2：上传示例内容

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funcstor*[yourname]*** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“+ 容器”**。

1.  在 **“新建容器”** 弹出窗口中，执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **“内容”**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“专用(非匿名访问)”**。
    
    1.  选择 **“确定”**。

1.  返回 **“容器”** 部分，选择新创建的 **“内容”** 容器。

1.	在 **“容器”** 边栏选项卡中，选择 **“上传”**。

1.	在 **“上传 blob”** 窗口中，执行以下操作：

    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。

    1.  在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\02\\Starter”**，选择 **“settings.json”** 文件，然后选择 **“打开”**。

    1.  确保选中 **“如果文件存储已经存在，则覆盖”** 复选框，然后选择 **“上传”**。 
    
    > **注意**：等待 blob 上传完成，然后再继续本实验室。

#### 任务 3：配置 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择你之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“函数应用”** 边栏选项卡中，执行以下操作：

    1.  展开之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用的节点。

    1.  展开 **“函数”** 节点。

    1.  展开该特定函数的 **“GetSettingInfo”** 节点。

    1.  选择 **“集成”** 节点。

1.  在 **“集成”** 部分，执行以下操作以创建新的输入类型 **“Azure Blob 存储”**：

    1.  选择 **“新建输入”**。

    1.  选择 **“Azure Blob 存储”**。

    1.  选择 **“选择”**。

1.  在 **“Azure Blob 存储输入”** 部分，执行以下操作：

    1.  在 **“Blob 参数名称”** 文本框中，输入值 **“json”**。

    1.  在 **“路径”** 文本框中，输入值 **“content/settings.json”**。

    1.  在 **“存储帐户连接”** 列表中，选择 **“AzureWebJobsStorage”**。

    1.  选择 **“保存”**。

1.  回到 **“整合”** 部分，选择现有的 **“HTTP 触发器”**。

1.  在 **“HTTP 触发器”** 部分，执行以下操作：

    1.  在 **允许的 HTTP 方法”** 列表中，选择 **“选定的方法”**。

    1.  在 **“请求参数名称”** 文本框中输入值 **“request”**。

    1.  在 **“选定的 HTTP 方法”** 复选框组中，确保仅 **“GET”** 选项被选中。

    1.  选择 **“保存”**。

#### 任务 4：写入函数代码

1.  在 **“函数应用”** 边栏选项卡中，执行以下操作：

    1.  展开之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用的节点。

    1.  展开 **“函数”** 节点。

    1.  选择该特定函数的 **“GetSettingInfo”** 节点。

1.  在函数编辑器中，观察示例 **“run.csx”** 函数脚本：

    ```
    #r "Newtonsoft.Json"

    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Primitives;
    using Newtonsoft.Json;

    public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");

        string name = req.Query["name"];

        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
        name = name ?? data?.name;

        return name != null
            ? (ActionResult)new OkObjectResult($"Hello, {name}")
            : new BadRequestObjectResult("Please pass a name on the query string or in the request body");
    }
    ```

1.  **删除**所有示例代码。

1.  添加以下代码行以导入 **Microsoft.AspNetCore.Mvc** 命名空间：

    ```
    using Microsoft.AspNetCore.Mvc;
    ```

1.  添加以下代码行以导入 **“System.Net”** 命名空间：

    ```
    using System.Net;
    ```

1.  添加以下代码块，创建一个新的名为 **“Run”** 的 **“公共静态”** 方法，该方法返回类型 **“IActionResult”** 的变量，并且也接受类型 **“HttpRequest”** 和 **“string”** 的变量作为参数，名为 *“request”* 和 *“json”*：

    ```
    公共静态 IActionResult 运行（HttpRequest 请求，字符串 json）
    {
    }
    ```

1.  在 **Run** 方法中，输入以下代码行以返回 *json* 参数的内容作为函数的 HTTP 响应：

    ```
    退回 new OkObjectResult(json)；
    ```

1.  查看 **“run.csx”** 文件，该文件现在应包括：

    ```
    using Microsoft.AspNetCore.Mvc;
    using System.Net;

    公共静态 IActionResult 运行（HttpRequest 请求，字符串 json）
    {
        退回 new OkObjectResult(json)；
    }
    ```

1.  选择 **“保存”** 以保存脚本。

#### 任务 5：测试函数运行

1.  在任务栏上，选择 **Windows Terminal** 图标。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以启动 **httprepl** 工具，将基 URI 设置为之前在本实验室中复制的 URL 值。

    ```
    httprepl <function-app-url>
    ```

    > **注意**：例如，如果你的 URL 是 **https://funclogicstudent.azurewebsites.net**，则你的命令就是 **httprepl https://funclogicstudent.azurewebsites.net**。

1.  在工具提示下，输入以下命令，然后按 Enter 以浏览到相对的 **“api”** 终结点：

    ```
    cd api
    ```

1.  输入以下命令，然后选择“Enter”转到 **“getsettinginfo”** 相关终结点：

    ```
    cd getsettinginfo
    ```

1.  输入以下命令，然后按 Enter 来对当前终结点运行 **“get”** 命令：

    ```
    获取
    ```

1.  查看函数应用响应的 JSON 内容，该内容现在应包括：

    ```
    {
        "version": "0.2.4",
        "root": "/usr/libexec/mews_principal/",
        "device": {
            "id": "21e46d2b2b926cba031a23c6919"
        },
        "notifications": {
            "email": "Anais85@outlook.com",
            "phone": "751.757.2014 x4151"
        }
    }
    ```

1.  输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```
    exit
    ```

1.  关闭当前正在运行的 Windows Terminal 应用程序。

1.	返回 Azure 门户的浏览器窗口。

#### 回顾

在本练习中，你在 Storage 里创建了能退回 JSON 文件内容的函数。

### 练习 5：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在 Azure 门户的导航窗格，选择 **“Cloud Shell”** 图标，打开一个新的 shell 实例。

    > **注意**： **Cloud Shell** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，你可以使用 **欢迎来到 Azure Cloud Shell 向导** 来配置 Cloud Shell 的初次使用。在向导中执行以下操作：
    
    1.  对话框提示你在开始使用 shell 前，先新建一个存储帐户。接受默认设置并选择 **“创建存储”** 。 

    > **注意**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室内容。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验是假设你使用的是新订阅的情况下编写的。

1.  在门户的 **Cloud Shell** 命令提示符中，输入以下命令，然后选择“输入”以列出订阅中的所有资源组：

    ```
    az group list
    ```

1.  在命令提示符中，键入以下命令，然后按“Enter”查看用于删除资源组的可用命令列表：

    ```
    az group delete --help
    ```

#### 任务 2：删除资源组

1.  在命令提示符中输入以下命令，然后按 Enter 删除 **无服务器** 资源组：

    ```
    AZ 组 删除 --名称 无服务器 --否-等待 --是
    ```
    
1.  关闭门户里的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1.     当前正在运行的 Microsoft Edge 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中曾经使用的资源组来清理订阅。