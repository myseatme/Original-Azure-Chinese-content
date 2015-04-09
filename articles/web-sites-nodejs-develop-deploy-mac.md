<properties linkid="develop-node-create-a-website-mac" urlDisplayName="Web site" pageTitle="在 Mac 上创建 Node.js 网站 - Azure 教程" metaKeywords="Azure create website Node, Azure deploy website Node, website Node.js, Node website" description="了解如何构建 Node.js 网站并在 Azure 中部署。代码示例使用 Java 编写。" metaCanonical="" services="web-sites" documentationCenter="Node.js" title="构建 Node.js 网站并部署到 Azure" authors="larryfr" solutions="" manager="" editor="" />
<tags ms.service="web-sites"
    ms.date=""
    wacn.date=""
    />

# 构建 Node.js 网站并部署到 Azure

本教程将介绍如何创建 [Node] 应用程序并使用 [Git] 将其部署到 Azure 网站。本教程中的说明适用于任何能够运行 Node 的操作系统。

如果您更愿意观看视频，右侧的视频片段提供了与本教程中相同的步骤。

以下是已完成应用程序的屏幕快照：

![显示“Hello World”消息的浏览器。][显示“Hello World”消息的浏览器。]

## 创建 Azure 网站并启用 Git 发布

按照这些步骤操作创建一个 Azure 网站，然后对该网站启用 Git 发布。

<div class="dev-callout">

**说明**
若要完成本教程，你需要一个 Azure 帐户。如果你没有帐户，只需花费几分钟就能创建一个免费试用帐户。有关详细信息，请参阅 \<a href="http://www.windowsazure.cn/zh-cn/pricing/free-trial/\>Azure 免费试用版\</a\>。\</p\> \</div\> \<ol\> \<li\>\<p\>登录到 \<a href="http://manage.windowsazure.cn"\>Azure 管理门户\</a\>。\</p\>\</li\> \<li\>\<p\>单击门户左下方的“+ 新增”图标。\<strong\>\</strong\>\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/plus-new.png" alt="突出显示“+ 新增”链接的 Azure 门户。"/\>\</p\>\</li\> \<li\>\<p\>单击“网站”，然后单击“快速创建”。\<strong\>\</strong\>\<strong\>\</strong\>.输入 \<strong\>URL\</strong\> 值，并在“地区”下拉类表中选择网站数据中心。\<strong\>\</strong\>单击对话框底部的复选标记。\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/create-quick-website.png" alt="“快速创建”对话框" /\>\</p\>\</li\> \<li\>\<p\>网站状态更改为“正在运行”之后，\<strong\>\</strong\>单击网站名称以访问“仪表板”。\<strong\>\</strong\>\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/go\_to\_dashboard.png" alt="打开网站仪表板" /\>\</p\>\</li\> \<li\>\<p\>在“快速启动”页面的右下方，选择“从源代码控制设置部署”。\<strong\>\</strong\>\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/setup\_git\_publishing.png" alt="设置 Git 发布" /\>\</p\>\</li\> \<li\>\<p\>当系统询问“您的源代码在哪里？”时，选择“本地 Git 存储库”，然后单击箭头。\<strong\>\</strong\>\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/where\_is\_code.png" alt="您的源代码在哪里" /\>\</p\>\</li\> \<li\>\<p\>要启用 Git 发布，您必须提供用户名和密码。如果您先前已对某个 Azure 网站启用了发布，则系统不会提示您输入用户名或密码。而是用您先前指定的用户名和密码创建一个 Git 存储库。记下此用户名和密码，因为它们将用于您创建的所有 Azure 网站的 Git 发布。\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/git-deployment-credentials.png" alt="提示输入用户名和密码的对话框。"/\>\</p\>\</li\> \<li\>\<p\>Git 存储库准备就绪后，会显示有关用于设置本地存储库并将文件推送到 Azure 的 Git 命令的说明。\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/git-instructions.png" alt="创建网站存储库后返回的 Git 部署说明。"/\>\</p\>\</li\> \</ol\> \<h2 id="build-and-test-your-application-locally"\>构建和测试本地应用程序\</h2\> \<p\>在此部分中，您将从 [nodejs.org] 创建包含“hello world”示例的 \<strong\>server.js\</strong\> 文件。通过添加 process.env.PORT 作为在 Azure 网站中运行时要侦听的端口，对原始示例进行修改得到了此示例。\</p\> \<ol\> \<li\>使用文本编辑器在 \<strong\>helloworld\</strong\> 目录中创建名为 \<strong\>server.js\</strong\> 的新文件。如果 \<strong\>helloworld\</strong\> 目录不存在，请创建一个。\</li\> \<li\>\<p\>添加以下内容作为 \<strong\>server.js\</strong\> 文件的内容，并进行保存：\</p\> \<pre\>\<code\>var http = require('http') var port = process.env.PORT || 1337; http.createServer(function(req, res) { res.writeHead(200, { 'Content-Type':'text/plain' }); res.end('Hello World\\n'); }).listen(port);\</code\>\</pre\>\</li\> \<li\>\<p\>打开命令行，并使用以下命令在本地启动网页：\</p\> \<pre\>\<code data-inline="1"\>node server.js\</code\>\</pre\> \<p\>[WACOM.INCLUDE \<a href="../includes/install-dev-tools.md"\>install-dev-tools\</a\>]\</p\>\</li\> \<li\>\<p\>打开 Web 浏览器，导航到 http://localhost:1337。将出现一个显示“Hello World”的网页，如下面的屏幕截图所示：\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/helloworldlocal.png" alt="显示“Hello World”消息的浏览器。"/\>\</p\>\</li\> \</ol\> \<h2 id="publish-your-application"\>发布应用程序\</h2\> \<ol\> \<li\>\<p\>在命令行中，将目录更改为 \<strong\>helloworld\</strong\> 目录，然后输入以下命令来初始化本地 Git 存储库。\</p\> \<pre\>\<code data-inline="1"\>git init\</code\>\</pre\> \<div class="dev-callout"\>\<strong\>Git 命令不可用？\</strong\> \<p\>\<a href="http://git-scm.com/" target="\_blank"\>Git\</a\> 是分布式版本控制系统，可用于部署 Azure 网站。有关平台的安装说明，请参阅 \<a href="http://git-scm.com/download" target="\_blank"\>Git 下载页面\</a\>。\</p\> \</div\>\</li\> \<li\>\<p\>使用以下命令将文件添加到存储库中：\</p\> \<pre\>\<code\>git add . git commit -m "initial commit"\</code\>\</pre\>\</li\> \<li\>\<p\>使用以下命令添加 Git remote，以便将更新推送到您之前创建的 Azure 网站：\</p\> \<pre\>\<code data-inline="1"\>git remote add azure [URL for remote repository]\</code\>\</pre\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/git-instructions.png" alt="创建网站存储库后返回的 Git 部署说明。"/\>\</p\>\</li\> \<li\>\<p\>使用以下命令将所做的更改推送到 Azure：\</p\> \<pre\>\<code data-inline="1"\>git push azure master\</code\>\</pre\> \<p\>系统会提示您输入之前创建的密码，然后您将看到以下输出：\</p\> \<pre\>\<code\>Password for 'testsite.scm.chinacloudsites.cn': Counting objects:3, done. Delta compression using up to 8 threads. Compressing objects:100% (2/2), done. Writing objects:100% (3/3), 374 bytes, done. Total 3 (delta 0), reused 0 (delta 0) remote:New deployment received. remote:Updating branch 'master'. remote:Preparing deployment for commit id '5ebbe250c9'. remote:Preparing files for deployment. remote:Deploying Web.config to enable Node.js activation. remote:Deployment successful. To https://user@testsite.scm.chinacloudsites.cn/testsite.git \* [new branch] master -\> master\</code\>\</pre\> \<p\>如果您在管理门户内导航到 Azure 网站的部署选项卡，您将在部署历史记录中看到您的第一个部署：\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/git\_deployments\_first.png" alt="门户上的 Git 部署状态" /\>\</p\>\</li\> \<li\>\<p\>在管理门户中，使用您的 Azure 网站上的“浏览”按钮浏览到您的站点\<strong\>\</strong\>。\</p\>\</li\> \</ol\> \<h2 id="publish-changes-to-your-application"\>将更改发布到您的应用程序\</h2\> \<ol\> \<li\>在文本编辑器中打开 \<strong\>server.js\</strong\> 文件，将“Hello World\\n”更改为“Hello Azure\\n”。保存文件。\</li\> \<li\>\<p\>在命令行中，将目录更改为 \<strong\>helloworld\</strong\> 目录，并运行以下命令：\</p\> \<pre\>\<code\>git add . git commit -m "changing to hello azure" git push azure master\</code\>\</pre\> \<p\>系统将提示您输入之前创建的密码。如果您在管理门户内导航到 Azure 网站的部署选项卡，您会看到更新的部署历史记录：\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/git\_deployments\_second.png" alt="门户上更新的 Git 部署状态" /\>\</p\>\</li\> \<li\>\<p\>使用“浏览”按钮浏览到您的站点\<strong\>\</strong\>，您将发现已应用上述更新。\</p\> \<p\>\<img src="./media/web-sites-nodejs-develop-deploy-mac/helloazure.png" alt="显示“Hello Azure”的网页" /\>\</p\>\</li\> \<li\>\<p\>通过在管理门户内在 Azure 网站的“部署”选项卡中选择一个之前的部署，并使用“重新部署”按钮，可以还原到之前的部署。\<strong\>\</strong\>\</p\>\</li\> \</ol\> \<h2 id="next-steps"\>后续步骤\</h2\> \<p\>尽管本文中的步骤使用 Azure 门户创建网站，但您还可以使用\<a href="/zh-cn/documentation/articles/xplat-cli/"\>针对 Mac 和 Linux 的 Azure 命令行工具\</a\>来执行同一操作。\</p\> \<p\>Node.js 提供了大量可供您的应用程序使用的模块。要了解 Azure 网站如何使用模块，请参阅\<a href="/zh-cn/documentation/articles/nodejs-use-node-modules-azure-apps/"\>结合使用 Node.js 模块和 Azure 应用程序\</a\>。\</p\> \<p\>要了解有关随 Azure 提供的 Node.js 版本的更多信息以及如何指定要与您的应用程序结合使用的版本，请参阅\<a href="/zh-cn/documentation/articles/nodejs-specify-node-version-azure-apps/"\>在 Azure 应用程序中指定 Node.js 版本\</a\>。\</p\> \<p\>如果您将应用程序部署到 Azure 后遇到问题，有关如何诊断问题的信息，请参阅\<a href="/zh-cn/documentation/articles/web-sites-nodejs-debug/"\>如何在 Azure 网站中调试 Node.js 应用程序\</a\>。\</p\> \<h2 id="additional-resources"\>其他资源\</h2\> \<ul\> \<li\>\<a href="/zh-cn/documentation/articles/install-configure-powershell/"\>Azure PowerShell\</a\>\</li\> \<li\>\<a href="/zh-cn/documentation/articles/xplat-cli/"\>针对 Mac 和 Linux 的 Azure 命令行工具\</a\>\</li\> \</ul\>

</div>

  [显示“Hello World”消息的浏览器。]: ./media/web-sites-nodejs-develop-deploy-mac/helloazure.png