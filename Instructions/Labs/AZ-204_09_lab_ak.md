---
lab:
    az204Title: 'Lab 09: 发布和订阅事件网格事件'
    az020Title: 'Lab 09: 发布和订阅事件网格事件'
    az204Module: 'Module 09: 开发基于事件的解决方案'
    az020Module: 'Module 09: 开发基于事件的解决方案'
    type: '答案要点'
---
    
# 实验室 09：发布和订阅事件网格事件
# 学生实验室答案要点

## Microsoft Azure 用户界面

鉴于 Microsoft 云工具的动态特性，Azure UI 在此培训内容开发后可能会发生更改。这些更改可能会导致实验室说明和实验室步骤不一致。

当社区要求我们进行更改时，Microsoft 将更新此培训课程。但是，由于云更新频繁发生，因此在此培训内容更新之前，你可能会遇到 UI 更改情况。**如果发生这种情况，请适应这些更改，并根据需要在实验室中熟悉这些更改。**

## 说明

### 准备工作

#### 登录实验室虚拟机

使用以下凭据登录 Windows 10 虚拟机 (VM)：

- 用户名：**Admin**

- 密码：**Pa55w.rd**

> **备注**：你的讲师将提供连接到虚拟实验室环境的说明。

#### 查看已安装的应用程序

在你的 Windows 10 桌面上找到任务栏。任务栏里有本实验室中你将使用的应用程序的图标：

- Microsoft Edge

- Microsoft Visual Studio Code

### 练习 1：创建 Azure 资源

#### 任务 1：打开 Azure 门户

1. 在任务栏上，选择 **“Microsoft Edge”** 图标。

1. 在打开的浏览器窗口中，转到 Azure 门户 (<https://portal.azure.com>)。

1. 输入你的 Microsoft 帐户的电子邮件地址，然后选择 **“下一步”**。

1. 输入 Microsoft 帐户的密码，然后选择 **“登录”**。

    > **备注**：第一次登录 Azure 门户时，你会看到一个门户教程。选择 **“开始使用”**，以跳过导览并开始使用门户。

#### 任务 2：打开 Azure Cloud Shell

1. 在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**： **“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1. 如果这是你首次使用订阅打开 Cloud Shell，则可使用**欢迎使用 Azure Cloud Shell 向导**配置 Cloud Shell。在向导中执行以下操作：

    - 当对话框提示你创建一个新的存储帐户以开始使用 shell 时，接受默认设置，然后选择 **“创建存储”**。

    > **备注**：等待 Cloud Shell 完成初始设置过程后，再继续本实验室。如果 **Cloud Shell** 配置选项未显示，很可能是因为你使用的是本课程实验室中的现有订阅。实验是假设你使用的是新订阅的情况下编写的。

1. 在 Azure 门户中，在 **Cloud Shell** 命令提示符处输入以下命令，然后选择 “Enter” 获取 Azure 命令行接口 (Azure CLI) 工具的版本：

    ```bash
    az --version
    ```

#### 任务 3：查看 Microsoft.EventGrid 提供程序注册

1. 在门户中的 **“Cloud Shell”** 命令提示符处，执行以下操作：

    1. 输入以下命令并选择 “Enter” 以获取 Azure CLI 根级别的子组和命令列表：

        ```bash
        az --help
        ```

    1. 输入以下命令，然后选择 “Enter” 以获取资源提供程序可用的命令列表：

        ```bash
        az provider --help
        ```

    1. 输入以下命令，然后按 “Enter” 键以列出所有当前注册的提供程序：

        ```bash
        az provider list
        ```

    1. 输入以下命令，然后按 “Enter” 键以仅列出当前注册的提供程序的命名空间：

        ```bash
        az provider list --query "[].namespace"
        ```

    1. 查看当前注册的提供程序列表。请注意，**Microsoft.EventGrid** 提供程序当前包含在提供程序列表中。

1. 关闭 Cloud Shell 窗格。

#### 任务 4：创建自定义事件网格主题

1. 在 Azure 门户的导航窗格上，选择 **“创建资源”**。

1. 在 **“新建”** 边栏选项卡，找到 **“搜索市场”** 文本框。

1. 在搜索框中输入 **“事件网格主题”**，然后按 Enter。

1. 在 **“全部内容”** 搜索结果边栏选项卡中，选择 **“事件网格主题”** 结果。

1. 在 **“事件网格主题”** 边栏选项卡中，选择 **“创建”**。

1. 在 **“创建主题”** 边栏选项卡上，执行以下操作：

    1. 在 **“名称”** 文本框中，输入 **hrtopic*[yourname]***。

    1. 在 **“资源组”** 部分，选择 **“新建”**，输入 **“PubSubEvents”**，然后选择 **“确定”**。

    1. 在 **“位置”** 下拉列表中，选择 **“(US) 美国东部”** 区域。

    1. 从 **“事件架构”** 下拉列表中，选择 **“事件网格架构”**，然后选择 **“创建”**。
  
    > **备注**：等待 Azure 完成创建主题，再继续本实验室操作。创建主题时会收到通知。

#### 任务 5：将 Azure 事件网格查看器部署到 Web 应用

1. 在 Azure 门户的导航窗格上，选择 **“创建资源”**。

1. 在 **“新建”** 边栏选项卡，找到 **“搜索市场”** 文本框。

1. 在搜索框中，输入 **“Web”**，然后按 Enter。

1. 在 **“全部内容”** 搜索结果边栏选项卡中，选择 **“Web 应用”** 结果。

1. 在 **“Web 应用”** 边栏选项卡上，选择 **“创建”**。

1. 在第二个 **“Web 应用”** 边栏选项卡中，找到边栏选项卡中的选项卡，如 **“基本”**。

    > **备注**：每个选项卡都代表在工作流中新建 Web 应用的一个步骤。你可以随时选择 **“查看 + 创建”** 跳过其余选项卡。

1. 在 **“基本信息”** 选项卡上，执行以下操作：

    1. 将 **“订阅”** 文本框设置为默认值。

    1. 在 **“资源组”** 部分，选择 **“PubSubEvents”**。

    1. 在 **“名称”** 文本框中，输入 **eventviewer*[yourname]***。

    1. 在 **“发布”** 部分，选择 **“Docker 容器”**。

    1. 在 **“操作系统”** 部分，选择 **“Linux”**。

    1. 在 **“区域”** 下拉列表中，选择 **“美国东部”** 区域。

    1. 在 **“Linux 计划(美国东部)”** 部分，选择 **“新建”**。 

    1. 在 **“名称”** 文本框中，输入值 **“EventPlan”**，然后选择 **“确定”**。

    1. 将 **“SKU 和大小”** 部分保留设置为默认值。

    1. 选择 **“下一步: Docker”**。

1. 在 **“Docker”** 选项卡上，执行以下操作：

    1. 在 **“选项”** 下拉列表中，选择 **“单个容器”**。

    1. 在 **“映像源”** 下拉列表中，选择 **“Docker 中心”**。

    1. 在 **“访问类型”** 下拉列表中，选择 **“公共”**。

    1. 在 **“映像和标记”** 文本框中，输入 **“microsoftlearning/azure-event-grid-viewer:latest”**。

    1. 选择 **“查看 + 创建”**。

1. 在 **“查看 + 创建”** 选项卡中，查看在上述步骤中选择的选项。

1. 选择 **“创建”**，使用指定的配置创建 Web 应用。 
  
    > **备注**：等待 Azure 完成 Web 应用的创建后再继续本实验室。你将会在应用创建完毕后收到通知。

#### 回顾

在本练习中，你创建了在本实验剩余时间里将用到的“事件网格主题”和“Web 应用”。

### 练习 2：创建事件网格订阅

#### 任务 1：访问事件网格查看器 Web 应用程序

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1. 在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“PubSubEvents”** 资源组。

1. 在 **“PubSubEvents”** 边栏选项卡上，选择你之前在本实验室中创建的 **eventviewer*[yourname]*** Web 应用。

1. 在 **“应用服务”** 边栏选项卡的 **“设置”** 部分，选择 **“属性”** 链接。

1. 在 **“属性”** 部分，记录 **“URL”** 文本框的值。你将在稍后的实验室中使用此值。

1. 选择 **“概述”**。

1. 在 **“概述”** 部分，选择 **“浏览”**。

1. 查看当前运行的 **“Azure 事件网格查看器”** Web 应用程序。在接下来的实验室中，请保持 Web 应用程序的运行状态。

    > **备注**：当事件发送到终结点后，该 Web 应用程序将启动实时更新。我们将在整个实验过程中用它来监视事件。

1. 返回显示 Azure 门户的当前打开的浏览器窗口。

#### 任务 2：创建新的订阅

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1. 在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“PubSubEvents”** 资源组。

1. 在 **“PubSubEvents”** 边栏选项卡上，选择你之前在本实验室中创建的 **hrtopic*[yourname]*** 事件网格主题。

1. 在 **“事件网格主题”** 边栏选项卡，选择 **“+ 事件订阅”**。

1. 在 **“创建事件订阅”** 边栏选项卡中，执行以下操作：

    1. 在 **“名称”** 文本框中，输入 **“basicsub”**。

    1. 在 **“事件架构”** 列表中，选择 **“事件网格架构”**。

    1. 在 **“终结点类型”** 列表中，选择 **“Web Hook”**。

    1. 选择 **“终结点”**。

    1. 在 **“选择 Web Hook”** 对话框的 **“订阅者终结点”** 文本框中，输入之前记录的 **“Web 应用 URL”** 值，请确保使用 **“https://”** 前缀，然后添加后缀 **“/api/updates”**，最后选择 **“确认选择”**。

        > **备注**：例如，如果 **Web 应用 URL** 值为 ``http://eventviewerstudent.azurewebsites.net/``，则**订阅者终结点**将为 ``https://eventviewerstudent.azurewebsites.net/api/updates``。

    1. 选择 **“创建”**。
  
    > **备注**：等待 Azure 完成创建订阅再继续本实验室操作。创建订阅时会收到通知。

#### 任务 3：观察订阅验证事件

1. 返回该浏览器窗口，其中显示 **“Azure 事件网格查看器”** Web 应用程序。

1. 查看在订阅创建过程中创建的 **Microsoft.EventGrid.SubscriptionValidationEvent** 事件。

1. 选择事件并查看其 JSON 内容。

1. 返回到当前打开显示 Azure 门户的浏览器窗口。

#### 任务 4：记录订阅凭据

1. 在 Azure 门户的“导航”窗格中，选择 **“资源组”**。

1. 在 **“资源组”** 边栏选项卡中，选择之前在本实验室中创建的 **“PubSubEvents”** 资源组。

1. 在 **“PubSubEvents”** 边栏选项卡上，选择你之前在本实验室中创建的 **hrtopic*[yourname]*** 事件网格主题。

1. 在 **“事件网格主题”** 边栏选项卡中，记录 **“主题终结点”** 字段的值。你将在稍后的实验室中使用此值。

1. 在 **“设置”** 类别中，选择 **“访问密钥”** 链接。

1. 在 **“访问密钥”** 部分，记录 **“密钥 1”** 文本框的值。你将在稍后的实验室中使用此值。

#### 回顾

在本练习中，你创建了一个新的订阅并进行了注册验证，然后记录了将新事件发布到该主题所需的凭据。

### 练习 3：在 .NET 上发布事件网格事件

#### 任务 1：创建 .NET 项目

1. 在 **“启动”** 屏幕上，选择 **“Visual Studio Code”** 磁贴。

1. 在 **“文件”** 菜单上，选择 **“打开文件夹”**。

1. 在打开的 **“文件资源管理器”** 窗口中，前往 **“Allfiles (F):\\Allfiles\\Labs\\09\\Starter\\EventPublisher”**，然后选择 **“选择文件夹”**。

1. 在 **“Visual Studio Code”** 窗口中，右键单击或激活 **“资源管理器”** 窗格的快捷菜单，然后选择 **“在终端中打开”**。

1. 在打开的命令提示符窗口中，输入以下命令并选择“Enter”以在当前文件夹中新建一个名为 **“EventPublisher”** 的 .NET 项目：

    ```powershell
    dotnet new console --name EventPublisher --output .
    ```

    > **备注**：**dotnet new** 命令将在与项目同名的文件夹中创建一个新的 **“控制台”** 项目。

1. 在命令提示符处，输入以下命令并按 Enter，从 NuGet 导入 4.1.0 版本的 **“Azure.Messaging.EventGrid”**：

    ```powershell
    dotnet add package Azure.Messaging.EventGrid --version 4.1.0
    ```

    > **备注**：**dotnet add package** 命令将从 NuGet 添加 **Microsoft.Azure.EventGrid** 包。有关详细信息，请前往 [Azure.Messaging.EventGrid](https://www.nuget.org/packages/Azure.Messaging.EventGrid/4.1.0)。

1. 在命令提示符处，输入以下命令，然后按 Enter 以生成 .NET Web 应用程序：

    ```powershell
    dotnet build
    ```

1. 选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 2：修改 Program 类以连接到事件网格

1. 在 **“Visual Studio Code”** 窗口的“资源管理器”窗格中，打开 **Program.cs** 文件。

1. 在 **Program.cs** 文件的代码编辑器选项卡中，删除现有文件中的所有代码。

1. 添加以下代码行，通过从 NuGet 导入的 **“Azure.Messaging.EventGrid”** 包导入 **“Azure”** 和 **“Azure.Messaging.EventGrid”** 命名空间：

    ```csharp
    using Azure;
    using Azure.Messaging.EventGrid;
    ```

1. 添加以下代码行，为此文件将使用的内置命名空间添加 **using** 指令：

    ```csharp
    using System;
    using System.Threading.Tasks;
    ```

1. 输入以下代码，创建一个新的 **Program** 类：

    ```csharp
    public class Program
    {
    }
    ```

1. 在 **“Program”** 类中，输入以下代码行以创建一个名为 **“topicEndpoint”** 的新字符串常数：

    ```csharp
    private const string topicEndpoint = "";
    ```

1. 将字符串常数 **“topicEndpoint”** 的值设置为你之前在本实验室中所记录事件网格主题的 **“主题终结点”**，从而将其更新。

1. 在 **Program** 类中，输入以下代码行以创建一个名为 **topicKey** 的新字符串常量：

    ```csharp
    private const string topicKey = "";
    ```

1. 将字符串常量 **topicKey** 的值设置为你之前在本实验室中记录的事件网格主题的**密钥**，从而将其更新。

1. 在 **Program** 类中，输入以下代码以创建新的异步 **Main** 方法：

    ```csharp
    public static async Task Main(string[] args)
    {
    }
    ```

1. 查看 **“Program.cs”** 文件，现在应该包含以下代码行：

    ```csharp
    using System;
    using System.Threading.Tasks;
    using Azure;
    using Azure.Messaging.EventGrid;

    public class Program
    {
        private const string topicEndpoint = "<topic-endpoint>";
        private const string topicKey = "<topic-key>";
        
        public static async Task Main(string[] args)
        {
        }
    }
    ```

#### 任务 3：发布新事件

1. 在 **Main** 方法中，执行以下操作以将事件列表发布到你的主题终结点：

    1. 添加以下代码行，使用 **topicEndpoint** 字符串常量作为构造函数参数创建类型为 **Uri** 的新变量 **endpoint**：

        ```csharp
        Uri endpoint = new Uri(topicEndpoint); 
        ```

    1. 添加以下代码行，使用 **topicKey** 字符串常量作为构造函数参数创建类型为 **[AzureKeyCredential](https://docs.microsoft.com/dotnet/api/azure.azurekeycredential)** 的新变量 **credential**：

        ```csharp
        AzureKeyCredential credential = new AzureKeyCredential(topicKey);
        ```

    1. 添加以下代码行，使用 **endpoint** 和 **credential** 变量作为构造函数参数创建类型为 **[EventGridPublisherClient](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient)** 的新变量 **client**：

        ```csharp
        EventGridPublisherClient client = new EventGridPublisherClient(endpoint, credential);
        ```

    1. 添加以下代码块，创建类型为 **[EventGridEvent](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridevent)** 的新变量 **firstEvent**，并使用示例数据填充该变量：

        ```csharp
        EventGridEvent firstEvent = new EventGridEvent(
            subject: $"New Employee: Alba Sutton",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alba Sutton",
                Address = "4567 Pine Avenue, Edison, WA 97202"
            }
        );
        ```

    1. 添加以下代码块，创建类型为 **[EventGridEvent](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridevent)** 的新变量 **secondEvent**，并使用示例数据填充该变量：

        ```csharp
        EventGridEvent secondEvent = new EventGridEvent(
            subject: $"New Employee: Alexandre Doyon",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alexandre Doyon",
                Address = "456 College Street, Bow, WA 98107"
            }
        );
        ```

    1. 添加以下代码行以异步调用 **[EventGridPublisherClient.SendEventAsync](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient.sendeventasync)** 方法，将 **firstEvent** 变量用作参数：

        ```csharp
        await client.SendEventAsync(firstEvent);
        ```

    1. 添加以下代码行，在控制台显示 **“首个事件已发布”** 消息：

        ```csharp
        Console.WriteLine("First event published");
        ```

    1. 添加以下代码行以异步调用 **[EventGridPublisherClient.SendEventAsync](https://docs.microsoft.com/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient.sendeventasync)** 方法，将 **secondEvent** 变量用作参数：

        ```csharp
        await client.SendEventAsync(secondEvent);
        ```

    1. 添加以下代码行，在控制台显示 **“第二个事件已发布”** 消息：

        ```csharp
        Console.WriteLine("Second event published");
        ```

1. 查看 **Main** 方法，现在应包括：

    ```csharp
    public static async Task Main(string[] args)
    {
        Uri endpoint = new Uri(topicEndpoint);
        AzureKeyCredential credential = new AzureKeyCredential(topicKey);
        EventGridPublisherClient client = new EventGridPublisherClient(endpoint, credential);
        
        EventGridEvent firstEvent = new EventGridEvent(
            subject: $"New Employee: Alba Sutton",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alba Sutton",
                Address = "4567 Pine Avenue, Edison, WA 97202"
            }
        );

        EventGridEvent secondEvent = new EventGridEvent(
            subject: $"New Employee: Alexandre Doyon",
            eventType: "Employees.Registration.New",
            dataVersion: "1.0",
            data: new
            {
                FullName = "Alexandre Doyon",
                Address = "456 College Street, Bow, WA 98107"
            }
        );

        await client.SendEventAsync(firstEvent);
        Console.WriteLine("First event published");

        await client.SendEventAsync(secondEvent);
        Console.WriteLine("Second event published");
    }
    ```

1. 保存 **Program.cs** 文件。

1. 在 **“Visual Studio Code”** 窗口中，右键单击或激活“资源管理器”窗格的快捷菜单，然后选择 **“在终端中打开”**。

1. 在打开的命令提示符处，输入以下命令并按 “Enter” 键，以运行 .NET Web 应用程序：

    ```powershell
    dotnet run
    ```

    > **备注**：如果出现任何生成错误，请查看位于 **“Allfiles (F):\\Allfiles\\Labs\\09\\Solution\\EventPublisher”** 文件夹中的 **Program.cs** 文件。

1. 观察从当前正在运行的控制台应用程序中输出的成功消息。

1. 选择 **“终止终端”** 或者 **“回收站”** 图标以关闭当前打开的终端和所有关联的进程。

#### 任务 4：查看发布的事件

1. 使用 **“Azure 事件网格查看器”** Web 应用程序返回到浏览器窗口。

1. 查看由控制台应用程序创建的 **Employees.Registration.New** 事件。

1. 选择任何事件并查看其 JSON 内容。

1. 返回 Azure 门户。

#### 回顾

在本练习中，使用 .NET 控制台应用程序将新事件发布到事件网格主题上。

### 练习 4：清理订阅

#### 任务 1：打开 Azure Cloud Shell

1. 在 Azure 门户中，选择 **“Cloud Shell”** 图标以打开一个新的 shell 实例。

    > **备注**：**“Cloud Shell”** 图标使用大于符号 (\>) 和下划线字符 (\_) 表示。

1. 如果这是你第一次使用订阅打开 Cloud Shell，则可以使用 **“欢迎使用 Azure Cloud Shell 向导”** 来配置 Cloud Shell，以便首次使用。在向导中执行以下操作：

    1. 对话框提示你配置 shell。选择 **“Bash”**，查看选定的订阅，然后选择 **“创建存储”**。

    > **备注**：等待 Cloud Shell 完成首次设置过程后，再继续本实验室。如果 Cloud Shell 配置选项未显示，很可能是因为你使用的是本课程实验室中的现有订阅。实验是假设你使用的是新订阅的情况下编写的。

#### 任务 2：删除资源组

1. 输入以下命令，然后按 Enter 删除 **PubSubEvents** 资源组：

    ```bash
    az group delete --name PubSubEvents --no-wait --yes
    ```

1. 关闭门户中的 Cloud Shell 窗格。

#### 任务 3：关闭活动应用程序

1. 关闭当前正在运行的 Microsoft Edge 应用程序。

1. 关闭当前正在运行的 “Visual Studio Code” 应用程序。

#### 回顾

在本练习中，你通过删除本实验室中使用的资源组清理订阅。
