---
lab:
    az204Title: '实验室 11: 监视部署到 Azure 的服务'
    az020Title: '实验室 11: 监视部署到 Azure 的服务'
    az204Module: '模块 11: 监视和优化 Azure 解决方案'
    az020Module: '模块 11: 监视和优化 Azure 解决方案'
    type: '答案要点'
---

# 实验室 11：监视部署到 Azure 的服务
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和步骤不匹配。

我们发现社区进行了必要更改时，Microsoft 将会更新此培训课程。但由于云更新频繁，在此培训内容更新前 UI 可能已更改。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录到实验室虚拟机

使用以下凭据登录到 Windows 10 虚拟机 (VM)：
    
-   用户名： **Admin**

-   密码： **Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：
    
-   Microsoft Edge

-   文件资源管理器

-   Visual Studio Code

-   Windows PowerShell

### 练习 1：创建和配置 Azure 资源

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  在登录页面中，输入 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

> **备注**：如果首次登录到 Azure 门户，则对话框会显示门户导览。选择 **“开始使用”**，以跳过导览并开始使用门户。

#### 任务 2：创建 Application Insights 资源

1.  在 Azure 门户的导航窗格上，选择 **“创建资源”**。

1.  在 **“新建”** 边栏选项卡上，找到 **“搜索市场”** 文本框。

1.  在搜索框中，输入 **“Insights”**，然后按 Enter。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“Application Insights”** 结果。

1.  在 **“Application Insights”** 边栏选项卡中，选择 **“创建”**。

1.  从第二个 **“Application Insights”** 边栏选项卡中查找选项卡，例如 **“基本”**。

    > **备注**：每个选项卡都代表在工作流中新建“Application Insights”实例的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 部分，选择 **“新建”**，输入 **“MonitoredAssets”**，然后选择 **“确定”**。
    
    1.  在 **“名称”** 文本框中，输入 “**instrm[yourname]**”。
    
    1.  在 **“区域”** 下拉列表中，选择 **“(美国)美国东部”** 区域。
    
    1.  在 **“资源模式”** 部分中，选择 **“经典”** 选项。
    
    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建 Application Insights 实例。   

    > **备注**：等待创建任务完成，再继续本实验室。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**instrm[yourname]**” Application Insights 帐户。

1.  在 **“Application Insights”** 边栏选项卡的 **“配置”** 类别中，选择 **“属性”** 链接。

1.  在 **“属性”** 部分，找到 **“检测密钥”** 文本框的值。客户端应用程序使用此密钥连接到 Application Insights。

#### 任务 3：使用 Azure 应用服务资源创建 Web 应用

1.  在 Azure 门户的导航窗格上，选择 **“创建资源”**。

1.  在 **“新建”** 边栏选项卡上，找到 **“搜索市场”** 文本框。

1.  在搜索框中，输入 **“Web”**，然后按 Enter。

1.  在 **“市场”** 搜索结果边栏选项卡中，选择 **“Web 应用”** 结果。

1.  在 **“Web 应用”** 边栏选项卡中，选择 **“创建”**。

1.  查看第二个 **“Web 应用”** 边栏选项卡中的各选项卡，例如 **“基本”**。

    > **备注**：每个选项卡都代表在工作流中新建 Web 应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1.  在 **“基本信息”** 选项卡中，执行以下操作：
    
    1.  将 **“订阅”** 文本框设置为默认值。
    
    1.  在 **“资源组”** 下拉列表中，选择 **MonitoredAssets**。
    
    1.  在 **“名称”** 文本框中，输入 “**smpapi[yourname]**”。

    1.  在 **“发布”** 部分，选择 **“代码”**。

    1.  在 **“运行时堆栈”** 下拉列表中，选择 **“.NET Core 3.1 (LTS)”**。

    1.  在 **“操作系统”** 部分，选择 **“Windows”**。

    1.  在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。

    1.  在 **“Windows 计划(美国东部)”** 部分中，选择 **“新建”**，然后将值 **“MonitoredPlan”** 输入 **“名称”** 文本框，接着选择 **“确定”**。

    1.  将 **“SKU 和大小”** 部分保留设置为默认值。

    1.  选择 **“下一步: 监视”**。

1.  在 **“监视”** 选项卡中，执行以下操作：

    1.  在 **“启用 Application Insights”** 部分，选择 **“是”**。

    1.  在 **“Application Insights”** 下拉列表中，选择你之前在本实验室中创建的 **instrm[yourname]** Application Insights 帐户。

    1.  选择 **“查看 + 创建”**。

1.  在 **“查看 + 创建”** 选项卡中，查看在先前步骤中选择的选项。

1.  选择 **“创建”**，使用指定的配置创建 Web 应用。   

    > **备注**：等待创建任务完成，再继续本实验室。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**smpapi[yourname]**” Web 应用。

1.  在 **“应用服务”** 边栏选项卡的 **“设置”** 类别，选择 **“配置”** 链接。

1.  在 **“配置”** 部分，执行以下操作：
    
    1.  选择 **“应用程序设置”** 选项卡。

    1.  选择 **“显示值”** 以获取与 API 关联的机密。

    1.  查找对应于 **“APPINSIGHTS\_INSTRUMENTATIONKEY”** 密钥的值。构建 Web 应用资源时会自动设置此值。

1.  在 **“应用服务”** 边栏选项卡的 **“设置”** 类别，选择 **“属性”** 链接。

1.  在 **“属性”** 部分，记录 **“URL”** 文本框的值。稍后将在本实验室中使用此值来对 API 发出请求。

#### 任务 4：配置 Web 应用自动缩放选项

1.  在 **“应用服务”** 边栏选项卡的 **“设置”** 类别，选择 **“横向扩展(应用服务计划)”** 链接。

1.  在 **“横向扩展”** 部分，执行以下操作：
    
    1.  选择 **“自定义自动缩放”**。
    
    1.  在 **“自动缩放设置名称”** 文本框中，输入 **“ComputeScaler”**。
    
    1.  在 **“资源组”** 列表中，选择 **“MonitoredAssets”**。
    
    1.  在 **“缩放模式”** 部分，选择 **“根据指标进行缩放”**。
    
    1.  在 **“实例限制”** 部分的 **“下限”** 文本框中，输入 **“2”**。
    
    1.  在 **“实例限制”** 部分的 **“上限”** 文本框中，输入 **“8”**。
    
    1.  在 **“实例限制”** 部分的 **“默认值”** 文本框中，输入 **“3”**。
    
    1.  选择 **“添加规则”**。在 **“缩放规则”** 弹出对话框中，将所有框设置为默认值，然后选择 **“添加”**。
    
    1.  在此部分中，选择 **“保存”**。 

    > **备注**：等待保存操作完成后，再继续本实验室。

#### 回顾

在此练习中，你创建了将用于本实验室其余部分的资源。

### 练习 2：使用 Application Insights 监视本地的 Web 应用程序 

#### 任务 1：生成一个 .NET Web API 项目

1.  在任务栏上，选择 **“Visual Studio Code””** 图标。

1.  在 **“文件”** 菜单上，选择 **“打开文件夹”**。

1.  在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\11\\Starter\\Api”**，然后选择 **“选择文件夹”**。

1.  在 **“Visual Studio Code””** 窗口中，右键单击“资源管理器”窗格或激活快捷菜单，然后选择 **“在终端中打开”**。

1.  在 **“打开”** 命令提示符处，输入以下命令并按 Enter，以在当前目录中创建一个名为 **“SimpleApi”** 的 .NET Web API 应用程序：

    ```
    dotnet new webapi --output . --name SimpleApi
    ```

1.  在命令提示符处，输入以下命令并按 Enter，将 2.14.0 版本的 **Microsoft.ApplicationInsights** 从 NuGet 导入到当前项目：

    ```
    dotnet add package Microsoft.ApplicationInsights --version 2.14.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.ApplicationInsights** 包。有关详细信息，请前往 [“Microsoft.ApplicationInsights”](https://www.nuget.org/packages/Microsoft.ApplicationInsights/2.14.0)。

1.  在命令提示符处，输入以下命令并按 Enter，从 NuGet 导入 2.14.0 版本的 **Microsoft.ApplicationInsights.AspNetCore**：

    ```
    dotnet add package Microsoft.ApplicationInsights.AspNetCore --version 2.14.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.ApplicationInsights.AspNetCore** 包。有关详细信息，请前往 [“Microsoft.ApplicationInsights.AspNetCore”](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/2.14.0)。

1.  在命令提示符处，输入以下命令并按 Enter，将 2.14.0 版本的 **Microsoft.ApplicationInsights.PerfCounterCollector** 从 NuGet 导入当前项目：

    ```
    dotnet add package Microsoft.ApplicationInsights.PerfCounterCollector  --version 2.14.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.ApplicationInsights.PerfCounterCollector**。有关详细信息，请转到 [Microsoft.ApplicationInsights.PerfCounterCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector/2.14.0)。


1.  在命令提示符中，输入以下命令并按 Enter，生成 .NET Web 应用程序：

    ```
    dotnet build
    ```
    
#### 任务 2：更新应用程序代码以禁用 HTTPS 并使用 Application Insights

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，选择 **“Startup.cs”** 文件以在编辑器中打开该文件。

1.  在编辑器的 **Startup** 类中，在第 39 行找到并删除以下代码行：

    ```
    app.UseHttpsRedirection();
    ```

    > **备注**：这行代码强制 Web 应用使用 HTTPS。对本实验室而言，没有这个必要。

1.  在 **Startup** 类中，添加名为 **INSTRUMENTATION_KEY** 的新静态字符串常量，并将其值设置为从之前在本实验室中创建的 Application Insights 资源中复制的检测密钥：

    ```
    private const string INSTRUMENTATION_KEY = "{your_instrumentation_key}";
    ```

    > **备注**：例如，如果检测密钥为 ``d2bb0eed-1342-4394-9b0c-8a56d21aaa43``，则代码行应为 ``private const string INSTRUMENTATION_KEY = "d2bb0eed-1342-4394-9b0c-8a56d21aaa43";``

1.  找到 **“Startup”** 类中的 **“ConfigureServices”** 方法：

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
    }
    ```

1.  在 **ConfigureServices** 方法末尾添加新代码行，以使用提供的检测密钥配置 Application Insights：

    ```    
    services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);
    ```

1.  观察 **“ConfigureServices”** 方法，该方法现在应包括：

    ```
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddControllers();
        services.AddApplicationInsightsTelemetry(INSTRUMENTATION_KEY);        
    }
    ```

1.  保存 **Startup.cs** 文件。

1.  在命令提示符中，输入以下命令并按 Enter，以生成 .NET Web 应用程序。

    ```
    dotnet build
    ```

#### 任务 3：本地测试 API 应用程序

1.  在命令提示符中，输入以下命令并按 Enter，运行 .NET Web 应用程序。

    ```
    dotnet run
    ```

1.  在任务栏上，打开 **“Microsoft Edge”** 图标的上下文菜单，然后打开一个新的浏览器窗口。

1.  在打开的浏览器窗口中，进入到托管在端口 **5000** 上的 **localhost** 上的测试应用程序的相对路径 **/weatherforecast**。
    
    > **备注**：完整的 URL 为 http://localhost:5000/weatherforecast

1.  关闭显示 http://localhost:5000/weatherforecast 地址的浏览器窗口。

1.  关闭当前正在运行的 “Visual Studio Code”应用程序。

#### 任务 4：获取 Application Insights 中的指标

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  在门户中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**instrm[yourname]**” Application Insights 帐户。

1.  在 **“Application Insights”** 边栏选项卡中心的磁贴中，找到显示的指标。具体来说，找到已经发生的服务器请求数量和平均服务器响应时间。

    > **备注**：请求最多可能需要五分钟即可显示在 Application Insights 指标图表中。

#### 回顾

在本练习中，你使用 ASP.NET Core 创建了一个 API，并将配置它将应用程序指标流式传输到 Application Insights。然后，你使用 Application Insights 仪表板查看有关 API 的性能详细信息。

### 练习 3：使用 Application Insights 监视 Web 应用

#### 任务 1：将应用程序部署到 Web 应用

1.  在任务栏上，选择 **“Visual Studio Code””** 图标。

1.  在 **“文件”** 菜单上，选择 **“打开文件夹”**。

1.  在 **“文件资源管理器”** 窗口中，浏览到 **“Allfiles (F):\\Allfiles\\Labs\\11\\Starter\\Api”**，然后选择 **“选择文件夹”**。

1.  在 “Visual Studio Code” 窗口中，右键单击“资源管理器”窗格或激活快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符中，输入以下命令并按 Enter 以登录 Azure 命令行接口 (CLI)：

    ```
    az login
    ```

1.  在浏览器窗口中，执行以下操作：
    
    1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。
    
    1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

1.  返回当前打开的“命令提示符”应用程序。  

    > **备注**：等待登录过程完成。

1.  在命令提示符处，输入以下命令并按 Enter，列出 **“MonitoredAssets”** 资源组中的所有应用：

    ```
    az webapp list --resource-group MonitoredAssets
    ```

1.  输入以下命令并按 Enter，找到前缀为 **smpapi\*** 的应用：

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')]"
    ```

1.  输入以下命令并按 Enter，以仅显示具有 **smpapi\*** 的单个应用的名称：

    ```
    az webapp list --resource-group MonitoredAssets --query "[?starts_with(name, 'smpapi')].{Name:name}" --output tsv
    ```

1.  输入以下命令并按 Enter，将当前目录更改为包含部署文件的 **“Allfiles (F):\\Allfiles\\Labs\\11\\Starter”** 目录：

    ```
    cd F:\Allfiles\Labs\12\Starter\
    ```

1.  输入以下命令并按 Enter，将 **api.zip** 文件部署到之前在本实验室中创建的 Web 应用：

    ```
    az webapp deployment source config-zip --resource-group MonitoredAssets --src api.zip --name <name-of-your-api-app>
    ```

    > **备注**：将 *name-of-your-api-app* 占位符替换为之前在本实验室中创建的 Web 应用的名称。你最近在之前的步骤中查询了此应用的名称。   

    > **备注**：等待部署完成后，再继续本实验室。

1.  关闭当前正在运行的 “Visual Studio Code” 应用程序。

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**smpapi[yourname]**” Web 应用。

1.  在 **“应用服务”** 边栏选项卡中，选择 **“浏览”**。将打开一个新的浏览器窗口或选项卡并返回 “404（未找到）” 错误。

1.  在浏览器地址栏中，通过将后缀 **/weatherforecast** 添加到当前 URL 的末尾并按 Enter 来更新 URL。

    > **备注**：例如，如果你的 URL 为 https://smpapistudent.azurewebsites.net， 则新的 URL 为 https://smpapistudent.azurewebsites.net/weatherforecast。

1.  找到作为使用 API 的结果返回的 JavaScript 对象表示法 (JSON) 数组。

#### 任务 2：配置 Web 应用的深入指标集合

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**smpapi[yourname]**” Web 应用。

1.  在 **“应用服务”** 边栏选项卡中，选择 **“Application Insights”**。

1.  在 **“Application Insights”** 边栏选项卡中，执行以下操作：

    1.  确保 **“Application Insights”** 部分设置为 **“启用”**。

    1.  在 **“检测应用程序”** 部分中，选择 **“.NET”** 选项卡。

    1.  在 **“集合级别”** 部分，选择 **“建议”**。

    1.  在 **“探查器”** 部分，选择 **“开”**。

    1.  在 **“Snapshot Debugger”** 部分，选择 **“关”**。

    1.  在 **“SQL 命令”** 部分，选择 **“关”**。

    1.  选择 **“应用”**。

    1.  在确认对话框中，选择 **“是”**。

1.  关闭 **“Application Insights”** 边栏选项卡。

1.  从 **“应用服务”** 边栏选项卡返回，选择 **“浏览”**。将打开一个新的浏览器窗口或选项卡并返回 “404（未找到）” 错误。

1.  在浏览器地址栏中，通过将后缀 **/weatherforecast** 添加到当前 URL 的末尾并按 Enter 来更新 URL。

    > **备注**：例如，如果你的 URL 为 https://smpapistudent.azurewebsites.net， 则新的 URL 为 https://smpapistudent.azurewebsites.net/weatherforecast。

1.  观察作为使用 API 结果返回的 JSON 数组。

1.  记录用于访问 JSON 数组的 URL。

    > **备注**：使用上一步中的示例，你需要记录 URL ``https://smpapistudent.azurewebsites.net/weatherforecast``。

#### 任务 3：在 Application Insights 中查看更新指标

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  在门户中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**instrm[yourname]**” Application Insights 帐户。

1.  在 **“Application Insights”** 边栏选项卡中心的磁贴中，找到显示的指标。具体来说，找到已经发生的服务器请求数量和平均服务器响应时间。

    > **备注**：请求最多可能需要五分钟即可显示在 Application Insights 指标图表中。

#### 任务 4：在 Application Insights 中查看实时指标

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  在门户中，选择 **“资源组”**。

1.  在 **“资源组”** 边栏选项卡中，找到并选择你之前在本实验室中创建的 **“MonitoredAssets”** 资源组。

1.  在 **“MonitoredAssets”** 边栏选项卡中，选择你之前在本实验室中创建的 “**instrm[yourname]**” Application Insights 帐户。

1.  在 **“Application Insights”** 边栏选项卡中，选择 **“调查”** 部分中的 **“实时指标流”**。

1.  在任务栏上，打开 **“Microsoft Edge”** 图标的上下文菜单，然后打开一个新的浏览器窗口。

1.  在新的浏览器窗口中，转到你之前在本实验室中记录的 URL。

1.  观察 JSON 数组的结果。

1.  返回显示 Azure 门户的当前打开的浏览器窗口。

1.  查看更新后的 **“实时指标流”** 边栏选项卡。

    > **备注**： **“传入请求”** 部分应该会在几秒钟内更新，其中显示你对 Web 应用发出的请求。

#### 回顾

在本练习中，你将 Web 应用程序部署到 Azure App 服务，并从同一 Application Insights 实例监视指标。

### 练习 4：清理订阅 

#### 任务 1：打开 Azure Cloud Shell

1.  在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**： **“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1.  如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：
    
    1.  对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。 

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，很可能是因为你使用的是本课程实验室中的现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1.  输入以下命令并按 Enter，删除 **MonitoredAssets** 资源组：

    ```
    az group delete --name MonitoredAssets --no-wait --yes
    ```
    
1.  关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动应用程序

1.  关闭当前正在运行的 Microsoft Edge 应用程序。

1.  关闭当前正在运行的 “Visual Studio Code” 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理订阅。
