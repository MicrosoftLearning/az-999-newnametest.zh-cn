---
lab:
    title: '实验室：跨服务安全访问资源机密'
    az204Module: '模块 07：实现安全云解决方案'
    az020Module: '模块 07：实现安全云解决方案'
    type: '参考答案'
---

# 实验室: 跨服务安全访问资源机密
# 学生实验室答案密钥

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不匹配。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验中熟悉这些更改**。

## 说明

### 开始前

#### 登录实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机：
    
-   用户名：**管理员**

-   密码：**Pa55w.rd**

> **注意**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 评价已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

### 练习 1：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，导航至 **“Azure 门户”** (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一个”**。

1.  输入你的 Microsoft 帐户**密码**，然后选择 **“登录”**。

    > **注意**：你第一次登录 Azure 门户时会为你提供门户导览。选择 **“开始使用”**，以跳过教程并开始使用门户。

#### 任务 2：创建 Azure 存储账户

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡中，找到存储实例列表。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“添加”**。

1.  从 **“创建存储帐户”** 边栏选项卡中找到各选项卡，例如 **“基本”**。

    > **注意**：每个标签页代表工作流中创建新存储帐户的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框保留默认值。

    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“SecureFunction”**，然后选择 **“确定”**。

    1.  在 **“存储帐户名称”** 文本框中，输入 **“securestor*[yourname]*”**。

    1.  在 **“位置”** 下拉列表中，选择“（美国）美国东部”区域。

    1.  在 **“性能”** 部分，选择 **“标准”**。

    1.  在 **“帐户类型”** 下拉列表中，选择 **“StorageV2（常规用途 v2）”**。

    1.  在 **“复制”** 下拉列表中，选择 **“本地冗余存储 (LRS)”**。

    1.  在 **“访问层”** 部分，确认 **“热”** 已选中。

    1.  选择 **“查看 + 创建”**。

1.  在 **“评价 + 创建”** 标签页中，评价在上一页步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建存储帐户。 

    > **注意**：等待创建任务完成，再继续本实验室。

1.  在 Azure 门户导航窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“存储帐户”**。

1.  在 **“存储帐户”** 边栏选项卡中，选择具有前缀 *securestor\** 的存储帐户实例。

1.  在 **“存储帐户”** 边栏选项卡中，找到 **“设置”** 部分并选择 **“访问密钥”** 链接。

1.  在 **“访问密钥”** 边栏选项卡中，选择任意一个密钥并记录 **“连接字符串”** 框中的任意值。你稍后将在本实验室中使用此值。

    > **注意**：你选择哪个连接字符串无关紧要。它们可以互换。

#### 任务 3：创建 Azure Key Vault

1.  在 Azure 门户的导航窗格中，选择到 **“创建资源”** 链接。

1.  在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。

1.  在搜索框中，输入 **“Vault”**，然后选择“Enter”。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“密钥保管库”** 结果。

1.  在 **“密钥保管库”** 边栏选项卡中，选择 **“创建”**。

1.  从 **“创建密钥库”** 边栏选项卡中找到各选项卡，例如 **“基本”**。

    > **注意**：每个标签页都代表在工作流中新建密钥保管库的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框保留为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表中选择 **“SecureFunction”**。
    
    1.  在 **“密钥保管库名称”** 文本框中，输入 “**securevault*[yourname]***”。

    1.  在 **“区域”** 下拉列表中，选择 **“美国东部”** 地区。
        
    1.  在 **“定价层”** 下拉列表中，选择 **“标准”**。
    
    1.  在 **“软删除”** 部分，选择 **“禁用”**。

    1.  选择 **“查看 + 创建”**。

1.  在 **“评价 + 创建”** 标签页中，评价在上一页步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建密钥库。

    > **注意**：等待创建任务完成，再继续本实验室。

#### 任务 4：创建 Azure Functions 应用

1.  在 Azure 门户的导航窗格中，选择到 **“创建资源”** 链接。

1.  在 **“新建”** 边栏选项卡，找到精选服务列表上方的 **“搜索市场”** 文本框。

1.  在搜索文本框中，输入 **“函数”**，然后按 Enter 键。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“函数应用”** 结果。

1.  在 **“函数应用”** 边栏选项卡中，选择 **“创建”**。

1.  从 **“函数应用”** 边栏选项卡中找到各选项卡，例如 **“基本信息”**。

    > **注意**：每个选项卡都代表在工作流中新建函数应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框保留为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“使用现有”**，然后从列表中选择 **“SecureFunction”**。
    
    1.  在 **“函数应用名称”** 文本框中，输入 “**securefunc*[yourname]***”。

    1.  在 **“发布”** 部分，选择 **“代码”**。

    1.  在 **“运行时堆栈”** 下拉列表中，选择 **“.NET Core”**。

    1.  在 **“版本”** 下拉列表中，选择 **“3.1”**。

    1.  在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。
    
    1.  选择 **“下一步:承载”**。

1.  在 **“托管”** 选项卡中，执行以下操作：

    1.  在 **“存储帐户”** 下拉列表中，选择你之前在本实验室中创建的 “**securestor*[yourname]***”存储帐户。

    1.  在 **“操作系统”** 部分，选择 **“Windows”**。

    1.  在 **“计划类型”** 下拉列表中，选择 **“消耗（无服务器）”** 选项。

    1.  选择 **“查看 + 创建”**。

1.  在 **“评价 + 创建”** 标签页中，评价在上一页步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建函数应用。 

    > **注意**：等待创建任务完成，再继续本实验室。

#### 复习

在本练习中，你创建了本实验室所需的所有资源。

### 练习2：配置机密和标识

#### 任务 1：配置系统分配的托管服务标识

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***” 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，选择 **“设置”** 部分的 **“标识”** 选项。

1.  在 **“标识”** 窗格中，找到 **“系统分配”** 选项卡，然后执行以下操作：
    
    1.  在 **“状态”** 部分，选择 **“开启”**，然后选择 **“保存”**。
    
    1.  在确认对话框中，选择 **“是”**。

    > **注意**：等待系统分配的托管标识创建完成后再继续本实验室。

#### 任务 2：创建密钥保管库机密

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  在 **“SecureFunction”** 边栏选项卡中，选择你之前在本实验室中创建的 “**securevault*[yourname]***” 密钥保管库。

1.  在 **“密钥保管库”** 边栏选项卡中，选择位于 **“设置”** 部分的 **“机密”** 链接。

1.  在 “**机密**” 窗格中，选择 “**生成/导入**”。

1.  在 **“创建机密”** 边栏选项卡中，执行以下操作：
    
    1.  在 **“上传选项”** 下拉列表中，选择 **“手动”**。
    
    1.  在 **“名称”** 文本框中，输入 **“storagecredentials”**。
    
    1.  在 **“值”** 文本框中，输入之前在本实验室中记录的存储帐户连接字符串。
    
    1.  将 **“内容类型”** 文本框保留设置为默认值。
    
    1.  将 **“设置激活日期”** 文本框保留设置为默认值。
    
    1.  将 **“设置到期日期”** 文本框保留设置为默认值。
    
    1.  在 **“已启用”** 部分，选择 **“是”**，然后选择 **“创建”**。
    
    > **注意**：等待机密创建完成后再继续本实验室。

1.  返回“机密”窗格，在列表中选择 **“storagecredentials”** 项目。

1.  在“版本”窗格中，选择最新版本的 **“storagecredentials”** 机密。

1.  在“机密版本”窗格中，执行以下操作：
    
    1.  找到最新版本机密的元数据。
    
    1.  选择 **“显示机密值”**，可以找到机密的值。
    
    1.  记录 **“机密标识符”** 文本框的值，稍后将在本实验室中用到。

    > **注意**：是记录 **“机密标识符”** 文本框中的值，而不是 **“机密值”** 文本框中的值。

#### 任务 3：配置密钥保管库访问策略

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  在 **“SecureFunction”** 边栏选项卡中，选择你之前在本实验室中创建的 “**securevault*[yourname]***” 密钥保管库。

1.  在 **“Key Vault”** 边栏选项卡中，选择位于 **“设置”** 部分的 **“访问策略”** 链接。

1.  在“访问策略”窗格中，选择 **“添加访问策略”**。

1.  在 **“添加访问策略”** 边栏选项卡中，执行以下操作：
    
    1.  选择 **“选择主体”** 链接。
    
    1.  在 **“主体”** 边栏选项卡中，找到并选择名为 “**securefunc*[yourname]***” 的服务主体，然后选择 **”选择“**。

        > **注意**：你之前在本实验室中创建的系统分配的托管标识将与 Azure Function 资源具有相同的名称。
    
    1.  将 **“密钥权限”** 列表保留设置为默认值。
    
    1.  在 **“机密权限”** 下拉列表中，选择 **“GET”** 权限。
    
    1.  将 **“证书权限”** 列表保留设置为默认值。
    
    1.  将 **“授权应用程序”** 文本框保留设置为默认值。
    
    1.  选择 **“添加”**。

1.  返回"访问策略"窗格，选择 **“保存”**。 

    > **注意**：等待访问策略更改保存后再继续本实验室。

#### 回顾

在本练习中，你为函数应用创建了服务器分配的托管服务标识，然后为该标识提供了相应的权限，以获取密钥保管库中的机密值。最后，你创建了一个将在函数应用中使用的机密。

### 练习 3：编写函数应用代码 

#### 任务 1：创建密钥保管库派生的应用程序设置 

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***” 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，选择 **“设置”** 部分中的 **“配置”** 选项。

1.  在 **“配置”** 窗格中，执行以下操作：
    
    1.  选择 **“应用程序设置”** 标签页，然后选择 **“新应用程序设置”**。
    
    1.  在出现的 **“添加/编辑应用程序设置”** 弹出窗口中，在 **“名称”** 字段，输入 **“StorageConnectionString”**。
    
    1.  在 **“输入值”** 文本框中，使用下列语法构造一个值：**@Microsoft.KeyVault(SecretUri=*Secret Identifier*)**

        > **注意**：你需要使用以上语法生成对**机密标识符**的引用。例如，如果机密标识符为 **https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf** ，则值为 **@Microsoft.KeyVault (SecretUri=https://securevaultstudent.vault.azure.net/secrets/storagecredentials/17b41386df3e4191b92f089f5efb4cbf)**
    
    1.  将 **“部署槽设置”** 文本框保留设置为默认值。

    1.  选择 **“确定”** 关闭弹出窗口并返回到 **“配置”** 部分。
    
    1.  在边栏选项卡单击 **“保存”** 以保留设置。  

    1.  在弹出的 **“保存更改”** 确认对话框中，选择 **“继续”**。

    > **注意**：等待应用程序设置保存后再继续本实验室。

#### 任务 2：创建 HTTP 触发的函数

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***” 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，从 **“函数”** 部分选择 **“函数”** 选项。

1. 在 **“函数”** 窗格中，选择 **“添加”** 按钮。

1.  在 **“新建函数”** 弹出窗口中，执行以下操作：
    
    1.  在 **“模板”** 选项卡中，选择 **“HTTP 触发器”**。

    1.  在 **“详细信息”** 选项卡中，找到 **“新建函数”** 文本框并输入 **“FileParser”**。

    1.  在 **“详细信息”** 选项卡中，找到 **“授权”** 文本框并选择 **“匿名”**。

    1.  选择 **“创建函数”**。

1.  在 **“函数”** 边栏选项卡中，从 **“开发人员”** 部分选择 **“代码 + 测试”** 选项。

1.  在函数编辑器中，观察示例函数脚本：

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

1.  **删除**所有示例代码，然后在函数编辑器中复制并粘贴以下占位符函数：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        return new OkObjectResult("Test Successful");
    }
    ```

1.  选择 **“保存”** 以保留对函数代码的更改。

1.  选择 **“测试/运行”**。

1.  在显示的弹出窗口中，执行以下操作：

    1.  在 **“输入”** 选项卡中，选择 **“运行”**。

    1.  在 **“输出”** 选项卡中，观察输出消息“Test Successful”。

#### 任务 3：测试密钥保管库派生的应用程序设置

1.  删除脚本的 **Run** 方法中的现有代码。

1.  观察 **“Run”** 方法，该方法现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

1.  添加以下代码行，以通过使用 **Environment.GetEnvironmentVariable** 方法获取 **StorageConnectionString** 应用程序设置的值：

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  添加以下代码行，以通过使用 **OkObjectResult** 类构造函数返回 *connectionString* 变量的值：
   
    ```
    return new OkObjectResult(connectionString);
    ```
    
1.  观察 **“Run”** 方法，该方法现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        return new OkObjectResult(connectionString);
    }
    ```

1.  选择 **“保存”** 以保留对函数代码的更改。

1.  选择 **“测试/运行”**。

1.  在显示的弹出窗口中，执行以下操作：

    1.  在 **“输入”** 选项卡中，选择 **“运行”**。

    1.  在 **“输出”** 选项卡中，观察该函数返回的输出连接字符串。

#### 复习

在本练习中，使用了服务标识读取密钥库中存储的机密值并将该值作为函数应用的结果返回。

### 练习 4：访问存储帐户 blob

#### 任务 1：上传示例存储 blob

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  在 **“SecureFunction”** 边栏选项卡中，选择你之前在本实验室中创建的 “**securestor*[yourname]***” 存储帐户。

1.  在 **“存储帐户”** 边栏选项卡中，选择 **“Blob 服务”** 部分的 **“容器”** 链接。

1.  在 **“容器”** 部分，选择 **“容器”**。

1.  在 **“新建容器”** 弹出窗口中，执行以下操作：
    
    1.  在 **“名称”** 文本框中，输入 **“drop”**。
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“Blob（仅限 blob 匿名读取访问权限）”**，然后选择 **“确定”**。

1.  返回 **“容器”** 部分，选择新创建的 **“drop”** 容器。

1.  在 **“容器”** 边栏选项卡中，选择 **“上传”**。

1.  在 **“上传 blob”** 弹出窗口中，执行以下操作：
    
    1.  在 **“文件”** 部分，选择 **“文件夹”** 图标。
    
    1.  在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\07\\Starter”**，选择 **“records.json”** 文件，然后选择 **“打开”**。
    
    1.  确保 **“如果文件已存在，则覆盖”** 已选中，然后选择 **“上传”**。  

    > **注意**：等待 blob 上传完成，然后再继续本实验室。

1.  返回 **“容器”** 边栏选项卡，从 blob 列表选择 **“records.json”** blob。

1.  在 **“blob”** 边栏选项卡中，找到 blob 元数据，然后复制该 blob 的 URL。

1.  在任务栏上，右键选择 **“Microsoft Edge”** 图标或激活快捷菜单，然后选择 **“新窗口”**。

1.  在新的浏览器窗口中，前往你为 blob 复制的 URL。

1.  你现在应该看到 blob 的 JavaScript 对象表示法 (JSON) 内容。关闭显示 JSON 内容的浏览器窗口。

1.  返回显示 Azure 门户的浏览器窗口，然后关闭 **“Blob”** 边栏选项卡。

1.  从 **“容器”** 边栏选项卡返回后，选择 **“更改访问级别策略”**。

1.  在 **“更改访问级别”** 弹出窗口中，执行以下操作：
    
    1.  在 **“公共访问级别”** 下拉列表中，选择 **“专用(非匿名访问)”**。
    
    1.  选择 **“确定”**。

1.  在任务栏上，右键选择 **“Microsoft Edge”** 图标或激活快捷菜单，然后选择 **“新窗口”**。

1.  在新的浏览器窗口中，前往你为 blob 复制的 URL。

1.  你现在应看到一条显示找不到资源的错误消息。

    > **注意**：如果你没有看到错误消息，则浏览器可能已缓存该文件。按 Ctrl+F5 刷新页面，直到看到错误消息。

#### 任务 2：添加 .NET 应用程序设置

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***” 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，选择 **“设置”** 部分中的 **“配置”** 选项。

1.  在 **“配置”** 窗格中，执行以下操作：
    
    1.  选择 **“应用程序设置”** 标签页，然后选择 **“新应用程序设置”**。
    
    1.  在 **“添加/编辑应用程序设置”** 弹出窗口中的 **“名称”** 文本框中，输入 **“DOTNET_ADD_GLOBAL_TOOLS_TO_PATH”**。
    
    1.  在 **“值”** 文本框中，输入 **“false”**。
    
    1.  将 **“部署槽设置”** 文本框保留设置为默认值。

    1.  选择 **“确定”** 关闭弹出窗口并返回到 **“配置”** 部分。
    
    1.  在边栏选项卡单击 **“保存”** 以保留设置。  

    1.  在弹出的 **“保存更改”** 确认对话框中，选择 **“继续”**。

    > **注意**：等待应用程序设置保存后再继续本实验室。

#### 任务 3：从 NuGet 拉取存储帐户 SDK

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***” 函数应用。

1.  在 **“应用服务”** 边栏选项卡中，从 **“开发工具”** 部分选择 **“应用服务编辑器（预览版）”** 选项 。

1.  在 **“应用服务编辑器（预览）”** 窗格中，选择 **“前往 ->”**。

1.  在 **“应用服务编辑器”** 浏览器窗口中，展开 **“FileParser”** 文件夹，打开上下文菜单，然后选择 **“新建文件”**。

1.  在对话框中，输入 **“function.proj”**，然后按 Enter，之后将显示一个空的代码编辑器。

1.  在编辑器中，插入以下配置内容：

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard2.0</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
            <PackageReference Include="Azure.Storage.Blobs" Version="12.4.0" />
        </ItemGroup>
    </Project>
    ```

    > **注意**：应用服务编辑器将自动保存文件的更改。这个 .proj 文件包含导入 [Azure.Storage.Blob](https://www.nuget.org/packages/Azure.Storage.Blobs/12.4.0) 包所需的 NuGet 包引用。

1.  关闭显示 **“应用服务编辑器”** 的浏览器窗口。

#### 任务 4：更新名称空间引用

1.  在 Azure 门户的“导航”窗口，选择 **“资源组”** 链接。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“SecureFunction”** 资源组。

1.  从 **“SecureFunction”** 边栏选项卡中，选择你先前在本实验室中创建的 “**securefunc*[yourname]***”*函数应用。

1.  在 **“应用服务”** 边栏选项卡中，从 **“函数”** 部分选择 **“函数”** 选项。

1.  在 **“函数”** 窗格中，找到现有的 **“FileParser”** 函数以打开该函数的编辑器。

1.  在 **“函数”** 边栏选项卡中，从 **“开发人员”** 部分选择 **“代码 + 测试”** 选项。

1.  在编辑器中，删除脚本 **Run** 方法中的现有代码。

1.  在代码文件中，添加以下代码行以创建 **Azure.Storage** 命名空间的 **using** 指令：

    ```
    using Azure.Storage;
    ```

1.  在代码文件中，添加以下代码行创建 **“Azure.Storage.Blobs”** 命名空间的 **“using”** 指令：

    ```
    using Azure.Storage.Blobs;
    ```

1.  添加以下代码行创建 **Azure.Storage.Blobs.Models** 命名空间的 **using** 指令：

    ```
    using Azure.Storage.Blobs.Models;
    ```

1.  观察 **“Run”** 方法，该方法现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {

    }
    ```

#### 任务 5：编写存储帐户代码

1.  在 **“Run”** 方法中添加以下代码行，以通过使用 **“Environment.GetEnvironmentVariable”** 方法获取 **“StorageConnectionString”** 应用程序设置的值：

    ```
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

1.  添加以下代码行，通过将 *connectionString* 变量传入构造函数，创建 **BlobServiceClient** 类的新实例：

    ```
    BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
    ```

1.  添加以下代码行，以在传入 **drop** 容器名称时使用 **BlobServiceClient.GetBlobContainerClient** 方法创建一个引用之前在本实验室中创建的容器的 **BlobContainerClient** 类新实例：

    ```
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
    ```

1.  添加以下代码行，以在传入 **records.json** blob 名称时使用 **BlobContainerClient.GetBlobClient** 方法创建一个引用之前在本实验室中上传的 blob 的 **BlobClient** 类新实例：

    ```
    BlobClient blobClient = containerClient.GetBlobClient("records.json");
    ```
    
1.  观察 **“Run”** 方法，该方法现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
    }
    ```

#### 任务 6：下载 blob

1.  添加以下代码行，以使用 **BlobClient.DownloadAsync** 方法以异步方式下载引用的 blob 内容，并将结果存储在名为 *response* 的变量中：

    ```
    var response = await blobClient.DownloadAsync();
    ```

1.  添加以下代码行，以通过使用 **FileStreamResult** 类构造函数返回 *content* 变量中存储的各种内容：

    ```
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

1.  观察 **“Run”** 方法，该方法现在应包括：

    ```
    using System.Net;
    using Microsoft.AspNetCore.Mvc;
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;

    public static async Task<IActionResult> Run(HttpRequest req)
    {
        string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
        BlobServiceClient serviceClient = new BlobServiceClient(connectionString);
        BlobContainerClient containerClient = serviceClient.GetBlobContainerClient("drop");
        BlobClient blobClient = containerClient.GetBlobClient("records.json");
        var response = await blobClient.DownloadAsync();
        return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    }
    ```

1.  选择 **“保存”** 以保留对函数代码的更改。

1.  选择 **“测试/运行”**。

1.  在显示的弹出窗口中，执行以下操作：

    1.  在 **“输入”** 选项卡中，选择 **“运行”**。

    1.  在 **“输出”** 选项卡中，观察存储在存储帐户中的 **$/drop/records.json** blob 的输出内容。

#### 复习

在本练习中，你使用 C\# 代码访问了存储帐户，然后下载了 blob 的内容。

### 练习 5：清理订阅 

#### 任务 1：打开 Azure Cloud Shell 并列出资源组

1.  在“Azure 门户的导航”窗格，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **注意**： **“Cloud Shell”** 图标使用大于符号 () 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，你可以使用 **欢迎来到 Azure Cloud Shell 向导** 来配置 Cloud Shell 的初次使用。在向导中执行以下操作：
    
    1.  对话框提示你在开始使用 shell 前，先新建一个存储帐户。接受默认设置并选择 **“创建存储”**。 

    > **注意**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，这很可能是因为你在本课程实验室中使用的是现有订阅。实验室是在你使用的是新订阅的假设下编写的。

#### 任务 2：删除资源组

1.  在命令提示符中输入以下命令，然后选择“Enter”删除 **“SecureFunction”** 资源组：

    ```
    az group delete --name SecureFunction --no-wait --yes
    ```
    
1.  关闭门户里的 Cloud Shell 窗格。

#### 任务 3：关闭活动的应用程序

1.     当前正在运行的 Microsoft Edge 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理订阅。
