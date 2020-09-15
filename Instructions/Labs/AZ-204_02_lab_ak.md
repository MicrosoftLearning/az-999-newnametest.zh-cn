---
lab:
    title: '实验室：使用 Azure Functions 实现任务处理操作逻辑'
    az204Module: '模块 02：实现 Azure Functions'
    az020Module: '模块 02：实现 Azure Functions'
    type: '参考答案'
---

# 实验室: 使用 Azure Functions 实现任务处理逻辑
# 学生实验室答案密钥

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验中熟悉这些更改**。

## 说明

### 开始前

#### 登录实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名：**管理员**

-   密码：**Pa55w.rd**

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

#### 任务 2：创建 Azure 存储账户

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡中，查看存储帐户实例列表。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“添加”**。

1.  在 **“创建存储帐户”** 边栏选项卡上，观察边栏选项卡上的选项卡，如 **“基本”**、**“标记”** 和 **“查看 + 创建”**。

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

1.  在 **“基本”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框保留设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表选择 **“无服务器”**。
    
    1.  在 **“函数应用名称”** 文本框中，输入 **funclogic*[yourname]***。

    1.  在 **“发布”** 部分, 选择 **“代码”**。

    1.  在 **“运行时堆栈”** 下拉列表中，选择 **“NET Core”**。

    1.  在 **“版本”** 下拉列表中，选择 **“3.1”**。

    1.  在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。
    
    1.  选择 **“下一步:承载”**。

1.  在 **“托管”** 标签页中，执行以下操作：

    1.  在 **“存储帐户”** 下拉列表中，选择之前在本实验室中创建的 **funcstor*[yourname]*** 存储帐户。

    1.  在 **“操作系统”** 部分，选择 **“Windows”**。

    1.  在 **“计划类型”** 下拉列表中，选择 **“使用”** 选项。

    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在上述步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建函数应用。 

    > **注意**：等待创建任务完成，再继续本实验室。

#### 复习

在本练习中，你创建了本实验室所需的所有资源。

### 练习2：创建被 HTTP 申请触发的函数

#### 任务 1：创建 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“应用服务”** 边栏选项卡的 **“函数”** 部分选择 **“函数”** 选项。

1. 在 **“函数”** 窗格中选择 **“添加”** 按钮。

1.  在 **“新建函数”** 弹出窗口中，执行以下操作：
    
    1.  在 **“模板”** 选项卡中选择 **“HTTP 触发器”**。

    1.  在 **“详细信息”** 选项卡内，找到 **“新建函数”** 文本框并输入 **“Echo”**。

    1.  在 **“详细信息”** 选项卡中找到 **“授权”** 文本框，并选择 **“匿名”**。

    1.  选择 **“创建函数”**。

#### 任务 2：写入函数代码

1.  在 **“函数”** 边栏选项卡中选择 **“开发人员”** 部分的 **“代码 + 测试”** 选项。

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

        string responseMessage = string.IsNullOrEmpty(name)
            ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";

                return new OkObjectResult(responseMessage);
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

1.  选择 **“保存”** 以保留对函数代码的更改。

#### 任务 3：在门户中测试函数运行

1.  选择 **“测试/运行”**。

1.  在显示的弹出窗口中，执行以下操作：

    1.  在 **“输入”** 选项卡的 **“正文”** 文本框中，输入以下 JSON 请求正文：

        ```
        {
            "message": "Hello, World!"
        }
        ```

    1.  在 **“输入”** 选项卡中，选择 **“运行”**。

    1.  在 **“输出”** 选项卡中，观察试运行的结果。结果应与原始请求正文完全一致。

#### 任务 4：获取基本函数 URL

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，复制 **“URL”** 文本框的值。你将在稍后的实验室中使用此值。

#### 任务 5：使用 httprepl 来测试函数运行

1.  在任务栏上，选择 **Windows Terminal** 图标。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 启动 **“httprepl”** 工具，将基础统一资源标识符 (URI) 设置为你之前在本实验室中复制的 URL 值。

    ```
    httprepl <function-app-url>
    ```

    > **注意**：例如，如果你的 URL 是 **https://funclogicstudent.azurewebsites.net** ，则你的命令就是 **httprepl https://funclogicstudent.azurewebsites.net** 。

1.  查看 httprepl 工具显示的错误消息。出现此消息的原因是该工具正在搜索用于“遍历”API 的 Swagger 定义文件。由于逻辑应用程序未生成 Swagger 定义文件，因此需要手动遍历该 API。

1.  在工具提示下，输入以下命令，然后按 Enter 以浏览到相对的 **“api”** 目录：

    ```
    cd api
    ```

1.  输入以下命令，然后按 Enter 浏览到相对的 **“echo”** 目录：

    ```
    cd echo
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，通过使用 **“\-\-content”** 选项发送设为数值 **“3”** 的 HTTP 请求正文：

    ```
    post --content 3
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，通过使用 **“\-\-content”** 选项发送设为数值 **“5”** 的 HTTP 请求正文：

    ```
    post --content 5
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，通过使用 **“\-\-content”** 选项发送设为字符串值 **“Hello”** 的 HTTP 请求正文：

    ```
    post --content "Hello"
    ```

1.  输入以下命令，然后按 Enter 运行 **post** 命令，通过使用 **“\-\-content”** 选项发送设为 JavaScript 对象表示法 (JSON) 值 **{"msg":"Successful"}** 的 HTTP 请求正文：

    ```
    post --content "{"msg": "Successful"}"
    ```

1.  输入以下命令，然后按 Enter 退出 **“httprepl”** 应用程序：

    ```
    exit
    ```

1.  关闭当前正在运行的 Windows Terminal 应用程序。

1.	返回 Azure 门户的浏览器窗口。

#### 复习

在本练习中，你成功创建了一个基本函数。该函数可回响通过 HTTP POST 申请所发送的内容。

### 练习 3：创建一个按日程触发的函数

#### 任务 1：创建由日程触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“应用服务”** 边栏选项卡的 **“函数”** 部分选择 **“函数”** 选项。

1. 在 **“函数”** 窗格中选择 **“添加”** 按钮。

1.  在 **“新建函数”** 弹出窗口中，执行以下操作：
    
    1.  在 **“模板”** 选项卡内，选择 **“计时器触发器”**。

    1.  在 **“详细信息”** 选项卡内，找到 **“新建函数”** 文本框并输入 **“Recurring”**。

    1.  在 **“详细信息”** 选项卡内，找到 **“计划”** 文本框并输入 **0 \*/2 \* \* \* \***。

    1.  在 **“详细信息”** 选项卡中找到 **“授权”** 文本框，并选择 **“匿名”**。

    1.  选择 **“创建函数”**。

#### 任务 2：观察函数运行

1.  在 **“函数”** 边栏选项卡中选择 **“开发人员”** 部分的 **“代码 + 测试”** 选项。

1.  在函数编辑器中，选择 **“日志”**。

1.  观察函数运行，大约每两分钟运行一次。每次运行函数都应向日志呈现一条简单的消息。

#### 任务 3：更新函数集成配置

1.  在 **“函数”** 边栏选项卡中，从 **“开发人员”** 部分，选择 **“集成”** 选项。

1.  在 **“集成”** 窗格中，选择 **“计时器”** 触发器。

1.  在 **“编辑触发器”** 弹出窗口中，执行以下操作：

    1.  在 **“计划”** 文本框中，将该值更改为 “**\*/30 \* \* \* \* \***”。

    1.  选择 **“保存”**。

#### 任务 4：观察函数运行

1.  在 **“函数”** 边栏选项卡中选择 **“开发人员”** 部分的 **“代码 + 测试”** 选项。

1.  在函数编辑器中，选择 **“日志”**。

1.  观察现在大约每 30 秒发生一次的函数运行。每次运行函数都应向日志呈现一条简单的消息。

#### 回顾

在本练习中，你创建了一个按照固定日程自动运行的函数。

### 练习 4：创建与其他服务集成的函数

#### 任务 1：创建 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“应用服务”** 边栏选项卡的 **“函数”** 部分选择 **“函数”** 选项。

1. 在 **“函数”** 窗格中，选择 **“添加”** 按钮。

1.  在 **“新建函数”** 弹出窗口中，执行以下操作：
    
    1.  在 **“模板”** 选项卡中，选择 **“HTTP 触发器”**。

    1.  在 **“详细信息”** 选项卡中，找到 **“新建函数”** 文本框，并输入 **“GetSettingInfo”**。

    1.  在 **“详细信息”** 选项卡中找到 **“授权”** 文本框，并选择 **“匿名”**。

    1.  选择 **“创建函数”**。

#### 任务 2：上传示例内容

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“无服务器”** 资源组。

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funcstor*[yourname]*** 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“容器”**。

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

1.  在 **“无服务器”** 边栏选项卡中，选择之前在本实验室中创建的 **funclogic*[yourname]*** 函数应用。

1.  在 **“应用服务”** 边栏选项卡的 **“函数”** 部分选择 **“函数”** 选项。

1.  在 **“函数”** 选项卡中，选择现有的 **GetSettingInfo** 函数以打开函数编辑器。

1.  在 **“函数”** 边栏选项卡中，从 **“开发人员”** 部分，选择 **“集成”** 选项。

1.  在 **“集成”** 窗格中，选择 **“添加输入”**。

1.  在 **“创建输入”** 弹出对话框中，执行以下操作：

    1.  在 **“绑定类型”** 列表中，选择 **“Azure Blob 存储”**。

    1.  在 **“Blob 参数名称”** 文本框中，输入值 **“json”**。

    1.  在 **“路径”** 文本框中，输入值 **“content/settings.json”**。

    1.  在 **“存储帐户连接”** 列表中，选择 **“AzureWebJobsStorage”**。

    1.  单击 **“确定”**。

1.  回到 **“集成”** 窗格中，选择 **“HTTP 触发器”**。

1.  在 **“编辑触发器”** 弹出对话框中，执行以下操作：

    1.  在 **“请求参数名称”** 文本框中输入值 **“request”**。

    1.  在 **“选定的 HTTP 方法”** 复选框组中，确保仅 **“GET”** 选项被选中。

    1.  选择 **“保存”**。

#### 任务 4：写入函数代码

1.  在 **“函数”** 边栏选项卡中选择 **“开发人员”** 部分的 **“代码 + 测试”** 选项。

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

        string responseMessage = string.IsNullOrEmpty(name)
            ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";

                return new OkObjectResult(responseMessage);
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
    public static IActionResult Run(HttpRequest request, string json)
    {
    }
    ```

1.  在 **Run** 方法中，输入以下代码行以返回 *json* 参数的内容作为函数的 HTTP 响应：

    ```
    return new OkObjectResult(json);
    ```

1.  查看 **“run.csx”** 文件，该文件现在应包括：

    ```
    using Microsoft.AspNetCore.Mvc;
    using System.Net;

    public static IActionResult Run(HttpRequest request, string json)
    {
        return new OkObjectResult(json);
    }
    ```

1.  选择 **“保存”** 以保留对函数代码的更改。

#### 任务 5：测试函数运行

1.  在任务栏上，选择 **Windows Terminal** 图标。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以启动 **httprepl** 工具，将基 URI 设置为之前在本实验室中复制的 URL 值。

    ```
    httprepl <function-app-url>
    ```

    > **注意**：例如，如果你的 URL 是 **https://funclogicstudent.azurewebsites.net** ，则你的命令就是 **httprepl https://funclogicstudent.azurewebsites.net** 。

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
    get
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

#### 复习

在本练习中，你在 Storage 里创建了能退回 JSON 文件内容的函数。

### 练习 5：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在“Azure 门户的导航”窗格，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **注意**：**Cloud Shell** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，你可以使用 **欢迎来到 Azure Cloud Shell 向导** 来配置 Cloud Shell 的初次使用。在向导中执行以下操作：
    
    1.  对话框提示你在开始使用 shell 前，先新建一个存储帐户。接受默认设置并选择 **“创建存储”** 。 

    > **注意**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1.  在命令提示符中输入以下命令，然后按 Enter 删除**无服务器**资源组：

    ```
    az group delete --name Serverless --no-wait --yes
    ```
    
1.  关闭门户里的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1.     当前正在运行的 Microsoft Edge 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中曾经使用的资源组来清理订阅。