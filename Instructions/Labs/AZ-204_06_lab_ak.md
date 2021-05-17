---
lab:
    az204Title: 'Lab 06: 使用 MSAL 和 .NET SDK 对 Microsoft Graph 进行身份验证和查询'
    az020Title: 'Lab 06: 使用 MSAL 和 .NET SDK 对 Microsoft Graph 进行身份验证和查询'
    az204Module: 'Module 06: 实现用户身份验证和授权'
    az020Module: 'Module 06: 实现用户身份验证和授权'
    type: '答案要点'
---

# 实验室 06：使用 MSAL 和 .NET SDK 对 Microsoft Graph 进行身份验证和查询
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

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

-   Visual Studio Code

### 练习 1：创建 Azure Active Directory (Azure AD) 应用程序注册

#### 任务 1：打开 Azure 门户

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：第一次登录 Azure 门户时，你会看到一个门户教程。选择 **“开始使用”**，以跳过导览并开始使用门户。

#### 任务 2：创建应用程序注册

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“Azure Active Directory”**。

1.  在 **“Azure Active Directory”** 边栏选项卡的 **“管理”** 部分选择 **“应用注册”**。

1.  在 **“应用注册”** 部分，选择 **“新建注册”**。

1.  在 **“注册应用程序”** 部分，执行以下操作：

    1.  在 **“名称”** 文本框，输入 **“graphapp”**。

    1.  在 **“受支持的帐户类型”** 列表中，选中 **“仅限此组织目录中的帐户(仅限默认目录 - 单个租户)”** 复选框。

    1.  在 **“重定向 URI”** 下拉列表中，选择 **“公共客户端/本机(移动设备和桌面设备)”**。

    1.  在 **“重定向 URI”** 文本框中，输入 **“http\://localhost”**。

    1.  选择 **“注册”**。

#### 任务 3：启用默认客户端类型

1.  在 **“graphapp”** 应用程序注册边栏选项卡的 **“管理”** 部分中选择 **“身份验证”**。

1.  在 **“身份验证”** 部分，执行以下操作：

    1.  在 **“高级设置”** 中的 **“允许公共客户端流”** 部分，选择 **“是”**。

    1.  选择 **“保存”**。

#### 任务 4：记录唯一标识符

1.  在 **“graphapp”** 应用程序注册边栏选项卡上，选择 **“概述”**。

1.  在 **“概述”** 部分，找到并记录 **“应用程序(客户端) ID”** 文本框的值。你将在稍后的实验室中使用此值。

1.  在 **“概述”** 部分，找到并记录 **“目录(租户) ID”** 文本框的值。你将在稍后的实验室中使用此值。

#### 回顾

在本练习中，你创建了一个新的应用程序注册，并记录了稍后在实验室中需要的重要值。

### 练习 2：使用 MSAL.NET 库获取令牌

#### 任务 1：创建 .NET 项目

1.  在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。

1.  在 **“文件”** 菜单中，选择 **“打开文件夹”**。

1.  在打开的 **“文件资源管理器”** 窗口中，浏览到 **Allfiles (F):\\Allfiles\\Labs\\06\\Starter\\GraphClient**，然后选择 **“选择文件夹”**。

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令，然后按 Enter 以在当前文件夹中创建一个名为 **GraphClient** 的新 .NET 项目：

    ```
    dotnet new console --name GraphClient --output .
    ```

    > **备注**：**dotnet new** 命令将在与项目同名的文件夹中创建一个新的 **“控制台”** 项目。

1.  在命令提示符处，输入以下命令，然后按 Enter 以从 NuGet 导入 4.7.1 版本的 **Microsoft.Identity.Client**：

    ```
    dotnet add package Microsoft.Identity.Client --version 4.7.1
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.Identity.Client** 包。有关详细信息，请转到 [“Microsoft.Identity.Client”](https://www.nuget.org/packages/Microsoft.Identity.Client/4.7.1)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：修改程序类

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡中，删除现有文件中的所有代码。

1.  添加以下代码行，通过从 NuGet 导入的 **Microsoft.Identity.Client** 包导入 **Microsoft.Identity.Client** 命名空间：

    ```
    using Microsoft.Identity.Client;
    ```
    
1.  添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

1.  输入以下代码，创建一个新的 **Program** 类：

    ```
    public class Program
    {
    }
    ``` 
    
1.  在 **Program** 类中，输入以下代码以创建新的异步 **Main** 方法：

    ```
    public static async Task Main(string[] args)
    {
    }
    ```

1.  在 **Program** 类中，输入以下代码行以创建一个名为 **_clientId** 的新字符串常量：

    ```
    private const string _clientId = "";
    ```

1.  通过将字符串常量 **_clientId** 的值设置为你之前在本实验室中记录的应**用程序（客户端）ID** 来更新该字符串常量。

1.  在 **Program** 类中，输入以下代码行以创建一个名为 **_tenantId** 的新字符串常量：

    ```
    private const string _tenantId = "";
    ```

1.  通过将字符串常量 **_tenantId** 的值设置为你之前在本实验室中记录的**目录（租户）ID** 来更新该字符串常量。

1.  查看 **Program.cs** 文件，该文件现在应包括：

    ```
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;

    public class Program
    {
        private const string _clientId = "<app-reg-client-id>";        
        private const string _tenantId = "<aad-tenant-id>";

        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 任务 3：获取 Microsoft 身份验证库 (MSAL) 令牌

1.  在 **Main** 方法中，添加以下代码行，以创建名为 *app* 且类型为 **[IPublicClientApplication](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication)** 的新变量：

    ```
    IPublicClientApplication app;
    ```

1.  在 **Main** 方法中，执行以下操作以使用静态 **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** 类生成公共客户端应用程序实例，然后将其存储在 app 变量中：

    1.  添加以下代码行以访问静态 **[PublicClientApplicationBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder)** 类：

        ```
        PublicClientApplicationBuilder
        ```

    1.  通过添加另一行代码来更新上一行代码，以使用 **PublicClientApplicationBuilder** 类的 **[Create()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.create)** 方法，从而以参数形式传入 *_clientId* 变量：

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
        ```

    1.  通过添加另一行代码来更新上一行代码以使用基 **[AbstractApplicationBuilder<>](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1)** 类的 **[WithAuthority()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withauthority)** 方法，从而以参数形式传入枚举值 **[AzureCloudInstance.AzurePublic](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.azurecloudinstance)** 和变量 *_tenantId*：

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
        ```

    1.  通过添加另一行代码来更新上一行代码以使用基 **AbstractApplicationBuilder<>** 类的 **[WithRedirectUri()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractapplicationbuilder-1.withredirecturi)** 方法，从而传入 **http://localhost** 的字符串值：

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
        ```

    1.  通过添加另一行代码来更新上一行代码，以使用 **PublicClientApplication** 类的 **[Build()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.publicclientapplicationbuilder.build)** 方法：

        ```
        PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

    1.  通过添加更多代码来更新上一行代码，以将表达式的结果存储在 *app* 变量中：

        ```
        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();
        ```

1.  在 **Main** 方法中，添加以下代码行以使用单个 **user.read** 值创建新的通用字符串 **[List<>](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)**：

    ```
    List<string> scopes = new List<string> 
    { 
        "user.read" 
    };
    ```

1.  在 **Main** 方法中，添加以下代码行，以创建名为 *result* 且类型为 **[AuthenticationResult](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult)** 的新变量：

    ```
    AuthenticationResult result;
    ```

1.  在 **Main** 方法中，执行以下操作以交互方式获取令牌并将输出存储在 *result* 变量中：

    1.  添加以下代码行以访问 *app* 变量：

        ```
        app
        ```

    1.  通过添加另一行代码来更新上一行代码以使用 **IPublicClientApplicationBuilder** 接口的 **[AcquireTokenInteractive()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.ipublicclientapplication.acquiretokeninteractive)** 方法，从而以参数形式传入 *scopes* 变量：

        ```
        app
            .AcquireTokenInteractive(scopes)
        ```

    1.  通过添加另一行代码来更新上一行代码，以使用 **[AbstractAcquireTokenParameterBuilder](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1)** 类的 **[ExecuteAsync()](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.abstractacquiretokenparameterbuilder-1.executeasync)** 方法：

        ```
        app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  通过添加更多代码来更新上一行代码，以使用 **await** 关键字异步处理表达式：
    
        ```
        await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

    1.  通过添加更多代码来更新上一行代码，以将表达式的结果存储在 *result* 变量中：
    
        ```
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();
        ```

1.  在 **Main** 方法中，添加以下代码行以使用 **Console.WriteLine** 方法将 **[AuthenticationResult.AccessToken](https://docs.microsoft.com/dotnet/api/microsoft.identity.client.authenticationresult.accesstoken)** 成员的值呈现到控制台：

    ```
    Console.WriteLine($"Token:\t{result.AccessToken}");
    ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };

        AuthenticationResult result;
        
        result = await app
            .AcquireTokenInteractive(scopes)
            .ExecuteAsync();

        Console.WriteLine($"Token:\t{result.AccessToken}");
    }
    ```

1.  保存 **Program.cs** 文件。

#### 任务 4：测试已更新的应用程序

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看 **Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** 文件夹中的 **Program.cs** 文件。

1.  正在运行的控制台应用程序将自动打开默认浏览器的实例。

1.  在“打开浏览器”窗口中，执行以下操作：

    1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

    1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：可以利用选项选择现有的 Microsoft 帐户，而不是重新登录。

1.  浏览器窗口将自动打开 **“请求的权限”** 网页。在网页上，执行以下操作：

    1.  查看请求的权限。

    1.  选择 **“接受”**。

1.  返回到当前正在运行的 Visual Studio Code 应用程序。

1.  观察当前运行的控制台应用程序在输出中呈现的预付码。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，你使用 MSAL.NET 库从 Microsoft 标识平台获取了令牌。

### 练习 3：使用 .NET SDK 查询 Microsoft Graph

#### 任务 1：从 NuGet 导入 Microsoft Graph SDK

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在命令提示符处，输入以下命令，然后 Enter 以从 NuGet 导入 1.21.0 版本的 **Microsoft.Graph**：

    ```
    dotnet add package Microsoft.Graph --version 1.21.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.Graph** 包。有关详细信息，请转到 [“Microsoft.Graph”](https://www.nuget.org/packages/Microsoft.Graph/1.21.0)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以从 NuGet 中导入 1.0.0-preview.2 版本的 **Microsoft.Graph.Auth**：

    ```
    dotnet add package Microsoft.Graph.Auth --version 1.0.0-preview.2
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.Graph.Auth** 包。有关详细信息，请转到 [“Microsoft.Graph.Auth”](https://www.nuget.org/packages/Microsoft.Graph.Auth/1.0.0-preview.2)。

1.  在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```
    dotnet build
    ```

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：修改程序类

1.  在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1.  在 **Program.cs** 文件的代码编辑器选项卡中，添加以下代码行，以通过从 NuGet 导入的 **Microsoft.Graph** 包导入 **Microsoft.Graph** 命名空间：

    ```
    using Microsoft.Graph;
    ```
    
1.  添加以下代码行，以通过从 NuGet 导入的 **Microsoft.Graph.Auth** 包导入 **Microsoft.Graph.Auth** 命名空间：

    ```
    using Microsoft.Graph.Auth;
    ```

1.  查看 **Program.cs** 文件，该文件现在应包括以下 **using** 指令：

    ```
    using Microsoft.Graph;    
    using Microsoft.Graph.Auth;
    using Microsoft.Identity.Client;
    using System;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    ```

#### 任务 3：使用 Microsoft Graph SDK 查询用户配置文件信息

1.  在 **Main** 方法中，执行以下操作以删除不必要的代码：

    1.  删除以下代码行：

        ```
        AuthenticationResult result;
        ```
    
    1.  删除以下代码组：

        ```
        result = await app
                .AcquireTokenInteractive(scopes)
                .ExecuteAsync();
        ```
    
    1.  删除以下代码行：

        ```
        Console.WriteLine($"Token:\t{result.AccessToken}");
        ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read"
        };
    }
    ```

1.  在 **Main** 方法中，添加以下代码行以创建名为 *provider* 且类型为 **DeviceCodeProvider** 的新变量，该变量以构造参数的形式传入变量 *app* 和 *scopes*：

    ```
    DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);
    ```

1.  在 **Main** 方法中，添加以下代码行以创建名为 *client* 且类型为 **GraphServiceClient** 的新变量，该变量以构造函数的形式传入变量 *provider*：

    ```
    GraphServiceClient client = new GraphServiceClient(provider);
    ```

1.  在 **Main** 方法中，执行以下操作以使用 **GraphServiceClient** 实例异步获取向 REST API 的相对 **/Me** 目录发出 HTTP 请求的响应：

    1.  添加以下代码行以获取 *client* 变量的 **Me** 属性：

        ```
        client.Me
        ```

    1.  通过添加另一行代码来更新上一行代码，以便使用 **Request()** 方法获取表示 HTTP 请求的对象：

        ```
        client.Me
            .Request()
        ```

    1.  通过添加另一行代码来更新上一行代码，以使用 **GetAsync()** 方法异步发出请求：

        ```
        client.Me
            .Request()
            .GetAsync()
        ```

    1.  通过添加更多代码来更新上一行代码，以使用 **await** 关键字异步处理表达式：

        ```
        await client.Me
            .Request()
            .GetAsync()
        ```

    1.  通过添加更多代码来更新上一行代码，以将表达式的结果存储在名为 *myProfile* 且类型为 **User** 的新变量中：

        ```
        User myProfile = await client.Me
            .Request()
            .GetAsync();
        ```

1.  在 **Main** 方法中，添加以下代码行以使用 **Console.WriteLine** 方法将 **User.DisplayName** 成员的值呈现到控制台：

    ```
    Console.WriteLine($"Name:\t{myProfile.DisplayName}");
    ```

1.  在 **Main** 方法中，添加以下代码行以使用 **Console.WriteLine** 方法将 **User.Id** 成员的值呈现到控制台：

    ```
    Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    ```

1.  查看 **Main** 方法，该方法现在应包括：

    ```
    public static async Task Main(string[] args)
    {
        IPublicClientApplication app;

        app = PublicClientApplicationBuilder
            .Create(_clientId)
            .WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
            .WithRedirectUri("http://localhost")
            .Build();

        List<string> scopes = new List<string> 
        { 
            "user.read" 
        };

        DeviceCodeProvider provider = new DeviceCodeProvider(app, scopes);

        GraphServiceClient client = new GraphServiceClient(provider);

        User myProfile = await client.Me
            .Request()
            .GetAsync();

        Console.WriteLine($"Name:\t{myProfile.DisplayName}");
        Console.WriteLine($"AAD Id:\t{myProfile.Id}");
    }
    ```

1.  保存 **Program.cs** 文件。

#### 任务 4：测试已更新的应用程序

1.  在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1.  在打开的命令提示符处，输入以下命令并按 Enter 键，以运行 .NET Web 应用程序：

    ```
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看 **Allfiles (F):\\Allfiles\\Labs\\06\\Solution\\GraphClient** 文件夹中的 **Program.cs** 文件。

1.  查看当前运行的控制台应用程序输出中的消息。在消息中记录代码的值。你将在稍后的实验室中使用此值。

1.  在任务栏上，选择 **“Microsoft Edge”** 图标。

1.  在打开的浏览器窗口中，转到 <https://microsoft.com/devicelogin>。

1.  在 **“输入代码”** 网页上，执行以下操作：

    1.  在 **“代码”** 文本框中，输入你之前在本实验室中复制的代码值。

    1.  选择 **“下一步”**。  

1.  在“登录”网页上，执行以下操作：

    1.  输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

    1.  输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：可以利用选项选择现有的 Microsoft 帐户，而不是重新登录。

1.  返回到当前正在运行的 Visual Studio Code 应用程序。

1.  在当前运行的控制台应用程序中查看 Microsoft Graph 请求的输出。

1.  选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 回顾

在本练习中，你使用 SDK 和基于 MSAL 的身份验证查询了 Microsoft Graph。

### 练习 4：清理订阅 

#### 任务 1：删除 Azure AD 中的应用程序注册

1.  返回 Azure 门户的浏览器窗口。

1.  在 Azure 门户的“导航”窗格中，选择 **“所有服务”**。

1.  在 **“所有服务”** 边栏选项卡中，选择 **“Azure Active Directory”**。

1.  在 **“Azure Active Directory”** 边栏选项卡的 **“管理”** 部分选择 **“应用注册”**。

1.  在 **“应用注册”** 部分，选择你之前在本实验室中创建的 **graphapp** Azure AD 应用程序注册。

1.  在 **“graphapp”** 部分，执行以下操作：

    1.  选择 **“删除”**。

    1.  在确认弹出对话框中，选择 **“是”**。

#### 任务 2：关闭活动应用程序

1.  关闭当前正在运行的 Microsoft Edge 应用程序。

1.  关闭当前正在运行的 “Visual Studio Code” 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的应用程序注册清理了订阅。
