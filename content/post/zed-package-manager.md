---
title: Zed包管理器
author: 陈 三
layout: post
date: 2014-05-17T05:50:36+00:00
url: /zed-package-manager.html
views:
  - 945
categories:
  - 前端开发
tags:
  - Zed

---
<div id="toc_container" class="ml-l u-floatRight pure-u-1-1 pure-u-sm-2-5 toc_white no_bullets">
  <nav id="myaffix">
  
  <p class="toc-title">
    目录
  </p>
  
  <ul class="toc-list nav" role="menu">
    <li class="toc-list__item" role="menuitem">
      <a href="#i"><span class="toc_number toc_depth_1">1</span> 安装与管理</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-2"><span class="toc_number toc_depth_1">2</span> 深入</a>
    </li>
    <li class="toc-list__item" role="menuitem">
      <a href="#i-3"><span class="toc_number toc_depth_1">3</span> 开发你自己的应用包</a>
    </li>
  </ul></nav>
</div>

<div class="">
  <p>
    <strong>本文译自<a href="http://zedapp.org/2014/05/zed-package-manager/">Zed Package Manager | Zed</a>。</strong>
  </p>
  
  <p>
    前阵子，我们给Zed加了一个很酷的特性ZPM，不过没有大肆宣传。你可以猜到，ZPM表示&#8221;Zed Package Manager&#8221;，它最初由<a href="https://github.com/TheKiteEatingTree">Andrew Stephan</a>完成。
  </p>
  
  <p>
    可以想知，ZPM在将来会大有改进，但现在，还是让我说说，它是怎么运作的：怎样安装、管理应用包，自己如何开发应用包来扩展Zed的功能。
  </p>
  
  <p>
    让我们先从安装与管理说起。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i">安装与管理</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi" href="#i"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    安装Zed应用包很简单，你所需要的，是一份Zed(废话)和你要安装的应用包的URI地址(关于URI后面会聊更多)。
  </p>
  
  <p>
    想看看现在都安装了哪些应用包？在编辑窗口里运行<code>Tools:Zpm:Installed Packages</code>命令，它会打开一个会话，列出目前安装的所有应用包，你还可以在这里卸载、更新、更新所有应用包，当然，也可以安装新应用包。列表用普通Zed文件当用户界面，你可以用键盘(移动光标到“按钮”然后按<strong>回车</strong>)或鼠标(鼠标直接点击某个“按钮”)操作。需注意的是，Zed预安装的应用包是不能卸载的(界面上确实有一个卸载选项，但其实没用)。
  </p>
  
  <p>
    要安装新应用包，请点击&#8221;Install New&#8221;按钮。你也可以运行<code>Tools:Zpm:Install</code>(任何地方都可以，不强制一定要从已安装应用包界面)。然后，输入应用包URI。你可以试试一个简单的应用包<code>gh:zefhemel/sample-zed-package</code>(后面我们会说明如何开发)。安装完成后，你应该有了一个新命令<code>My Test Command</code>，执行后会弹出&#8221;Hello world&#8221;对话框。
  </p>
  
  <p>
    Awesomeness。
  </p>
  
  <p>
    Zed目前的应用包是分散的，没有Sublime或Atom那样的中心库。不过暂时可以用<a href="https://github.com/zedapp/zed/wiki/Packages">Zed wiki</a>替代。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-2">深入</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-2" href="#i-2"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <p>
    本质上说，应用包不过是提供一种简单方法，帮你安装一些文件到configuration项目。你可以查看Configuration项目下的<code>/packages</code>(这里借助树型结构是最方便的：<code>Command-T/Ctrl-T</code>)文件夹，你能看到一些预安装的应用包。截至写下这篇的时候，以下模式是以Zed应用包形式分发的：
  </p>
  
  <ul>
    <li>
      <a href="https://github.com/zedapp/javascript-mode">JavaScript mode </a>
    </li>
    <li>
      <a href="https://github.com/zedapp/json-mode">JSON mode</a>
    </li>
    <li>
      <a href="https://github.com/zedapp/json5-mode">JSON5 mode</a>
    </li>
    <li>
      <a href="https://github.com/zedapp/php-mode">PHP mode</a>
    </li>
    <li>
      <a href="https://github.com/zedapp/css-mode">CSS mode</a>
    </li>
    <li>
      <a href="https://github.com/zedapp/jsx-mode">JSX mode</a>
    </li>
  </ul>
  
  <p>
    以后，会有更多的内置模式迁移到Zed应用包上，不过这个任务不轻，所以会花些时间。
  </p>
  
  <p>
    如果你打开你的Configuration项目下的<code>/default.json</code>文件，你能看到一个<code>packages</code>键：
  </p>
  
  <pre><code>packages: [
    "gh:zedapp/javascript-mode",
    "gh:zedapp/json-mode",
    "gh:zedapp/json5-mode",
    "gh:zedapp/php-mode",
    "gh:zedapp/css-mode",
    "gh:zedapp/jsx-mode"
]
</code></pre>
  
  <p>
    Zed会确保这里列出的应用包都已安装，并自动更新。如果你自个安装了一个应用包，则可以在你的<code>/user.json</code>文件里找到它。
  </p>
  
  <p>
    那么，这些应用包从哪儿来？一个应用包的URI可以是一个完整的HTTP链接，指向一个目录，目录下包含一个<code>package.json</code>文件。当然，你也可以使用快捷方式。一个快捷URI带有<code>gh:</code>(github)或<code>bb:</code>(bitbucket)前缀(目前是这样)。它们会扩展(举<code>gh:zedapp/javascript-mode</code>来说)成<code>https://raw.githubusercontent.com/zedapp/javascript-mode/master/</code>。ZPM据此补缀<code>package.json</code>，找到一个类似如下的JSON文件：
  </p>
  
  <pre><code>{
    "name": "JavaScript mode",
    "uri": "gh:zedapp/javascript-mode",
    "version": "0.2",
    "description": "JavaScript mode for Zed",
    "files": [
        "beautify-js.js",
        "beautify.js",
        "check.js",
        "index.js",
        "jshint.js"
    ]
}
</code></pre>
  
  <p>
    所需的键如下：
  </p>
  
  <ul>
    <li>
      <code>uri</code>：该URI与人们用来安装你的应用包使用的URI必须一致(否则的话，你可能遭遇不对劲)
    </li>
    <li>
      <code>name</code>：显示在UI中的应用包的名称
    </li>
    <li>
      <code>description</code>：显示在UI中的描述内容
    </li>
    <li>
      <code>version</code>：版本号，你一旦更新这个数字，则那些已安装你应用包的人们就能自动升级它们(ZPM每隔几小时检查一次更新)
    </li>
    <li>
      <code>files</code>：组成应用包的文件的相对路径列表(<code>package.json</code>和<code>config.json</code>会自动包含，你不必自己添加它们到列表)
    </li>
  </ul>
  
  <p>
    每一个应用包，除了<code>package.json</code>文件外，至少还应该有一个<code>config.json</code>文件，文件中包含常见的Zed配置，比如<a href="http://zedapp.org/2014/02/configuration/">定义新命令，模式，样式主题</a>或任何其他你的应用包提供的东西。譬如这个<a href="https://github.com/zedapp/javascript-mode/blob/master/config.json">JavaScript模式的配置</a>。其余的文件多数只是些JavaScript文件，用于落实config文件中列出的命令。
  </p>
  
  <h2 class="storycontent-h2">
    <span id="i-3">开发你自己的应用包</span><a title="标题链接地址" class="u-floatRight hidden" id="heyi-3" href="#i-3"><span class="" aria-hidden="true">#</span></a>
  </h2>
  
  <h3>
    准备
  </h3>
  
  <p>
    你要做的第一件事，是将你的configuration项目保存到一个本地目录(而不是SyncFS，这是Chrome版Zed默认保存的位置)。原因是你可能需要上传或推送你的应用包到诸如Github这样的地方，这样你就需要能直接访问这些文件。在Chrome版中，你可以运行<code>Configuration:Store in Local Folder</code>命令。如果你用的是独立版本的Zed，则Linux下，你的配置文件保存在<code>~/.config/zed/config</code>，Mac下则保存在<code>~/Library/Application Support/zed/config</code>。如果你想把配置文件保存到其他地方，则使用<code>Configuration:Set Configuration Directory</code>命令。我个人是把我的配置保存在我的Dropbox文件夹中。
  </p>
  
  <h3>
    想想在哪儿托管你的应用包
  </h3>
  
  <p>
    我建议你在Gihub或Bitbucket上给你的应用包创建一个公共代码库。本篇中，我们会拿<a href="https://github.com/zefhemel/sample-zed-package">我托管在我<code>zefhemel</code> github账户上的一个叫做<code>sample-zed-package</code>的Github库</a>作例子。
  </p>
  
  <h3>
    创建应用包
  </h3>
  
  <p>
    Configuration项目里有些专为开发者设计的命令，可以让你迅速开工。运行命令<code>Tools:Zpm:Create Package</code>。这会弹出对话框要求你输入应用包的URI。我们且输入<code>gh:zefhemel/sample-zed-package</code>(可替换成你的任一库名)。
  </p>
  
  <p>
    这样我们就在<code>/packages/gh/zefhemel/sample-zed-package/</code>目录下创建了两个文件，<code>package.json</code>和<code>config.json</code>。默认会打开<code>package.json</code>文件。请根据你的意思修改它的默认值，比如：
  </p>
  
  <pre><code>{
    "name": "My First Zed Package",
    "uri": "gh:zefhemel/sample-zed-package",
    "version": "1.0",
    "description": "A useful new package",
    "files": []
}
</code></pre>
  
  <p>
    接下来，让我们打开同一目录下的<code>config.json</code>文件(小贴士：按<kbd>Command-E</kbd>/<kbd>Ctrl-E</kbd>调出Goto后按空格键补全当前目录完整路径，然后选择<code>config.json</code>)。
  </p>
  
  <p>
    就我们的情况，只需定义一个命令样例：
  </p>
  
  <pre><code>commands: {
        "My Test Command": {
            scriptUrl: "./command.js"
        }
    }
}
</code></pre>
  
  <p>
    接下来，让我们新建<code>/packages/gh/zefhemel/sample-zed-package/command.js</code>(同样使用Goto小贴士)：
  </p>
  
  <pre><code>var ui = require("zed/ui");

module.exports = function(info) {
    return ui.prompt("Hello world!");
};
</code></pre>
  
  <p>
    如你所见，Zed的命令是用CommonJS风格模块化的。它导出一个函数，该函数接收一个变量(info)。取决于你的配置，变量会包含一些命令执行环境的有用信息。Zed不断有增加API，允许你与编辑器互动，所有的这些API都可以通过<code>require</code> <code>zed/*</code>模块取得。你可以看看你Configuration项目里<code>/api/zed</code>目录下有什么。我得承认，这些API的文档还很欠缺，因此在文档完善前，建议多看些示例。比如Configuration项目：所有的已安装的应用包，模式，主题样式和各种命令的代码都在那儿，随你查阅。如果你有特定的问题，请加入<a href="https://groups.google.com/forum/#!forum/zed-user">Zed Google Group</a>提问！
  </p>
  
  <p>
    为测试我们新创建的项目，我们需要将它添加到<code>/user.json</code>里的应用包列表：
  </p>
  
  <pre><code>packages: [
    "gh:zefhemel/sample-zed-package"
]
</code></pre>
  
  <p>
    你的配置会自动重载，因此新命令已经可用。你可以运行<code>My Test Command</code>命令验证一下。如果没有，可以使用<code>Configuration:Reload</code>命令强制重载你的配置。如果你改的是<code>config.json</code>文件，则每次都需要强制重载。另一个你会经常用到的命令是<code>Sandbox:Reset</code>，它会确保你的JavaScript代码在下一次它被调用时重载。
  </p>
  
  <h3>
    发布你的应用包
  </h3>
  
  <p>
    在发布你的应用包前，我们需要记住一个重要的事情：更新我们的<code>package.json</code>文件，引入所有其余的文件(指除开package.json与config.json外的文件)。好在Zed有提供一个便利的命令：切换到你的<code>package.json</code>文件，然后执行<code>Tools:Zpm:Update Package.json File List</code>。这个命令会自动扫描你的项目，然后更新<code>package.json</code>文件来引用<code>command.js</code>文件。
  </p>
  
  <p>
    Zed方面就这些了。总之，剩下要做的，就是把我们的应用包目录变成一个git目录，commit所有文件，然后push到github。
  </p>
  
  <p>
    首先，打开命令窗口，<code>cd</code>到你的Zed Configuration目录，然后<code>cd</code>到我们的应用包目录：
  </p>
  
  <pre><code>$ cd packages/gh/zefhemel/sample-zed-package
</code></pre>
  
  <p>
    在目录下初始化一个git库，然后添加所有文件并commit：
  </p>
  
  <pre><code>$ git init
$ git add *
$ git commit -m "Initial checkin"
</code></pre>
  
  <p>
    将我们之前创建的github库配置为远程并把代码推上去。我的情况：
  </p>
  
  <pre><code>$ git remote add origin git@github.com:zefhemel/sample-zed-package.git
$ git push -u origin master
</code></pre>
  
  <p>
    就这样。
  </p>
  
  <h3>
    测试你的应用包
  </h3>
  
  <p>
    在告知我们所有的朋友前，我们还需要测试下应用包。我通常是另外备一份Zed(我或者是用独立版本做开发，Chrome版本做测试或者反过来，或者是使用安装在Chrome Canary上的Zed)。此外你也可以切换你的Zed配置到一个全新、干净的目录，随后再切换回来。目的就只是准备一个还没有安装过你的应用包的Zed。你甚至可以换一台电脑(比如你的Chromebook）。
  </p>
  
  <p>
    要安装你的应用包，请在你干净版的Zed运行<code>Tools:Zpm:Install</code>命令，然后输入应用包URI。如果一切顺利，你的命令应该已经可用了。除了执行<code>Tools:Zpm:Install</code>命令外，你也可以手动更新配置中的<code>packages</code>列表，增加你的应用包URI。效果是一样的。
  </p>
  
  <p>
    管用？恭喜，请务必将你的应用包添加到我们的<a href="https://github.com/zedapp/zed/wiki/Packages">维基页面</a>。
  </p>
  
  <h3>
    开发与调试贴士
  </h3>
  
  <p>
    为了开发Zed应用包，你最好把Configuration项目当成一个开发环境。我通常是先添加新模式与命令到<code>/user.json</code>文件里，如果没问题，再迁移到应用包里。
  </p>
  
  <p>
    <strong>Logging</strong>：每个项目都有一个<code>zed::log</code>文件，会列出Zed给出的提示，错误与警告以及沙箱代码。如果你的应用包或脚本不能正常运行，请先检查<code>zed::log</code>找找头绪，看哪里可能出错了。你也可以在你的JavaScript中使用<code>console.log</code>等来调试，它们输出的结果也会显示在<code>zed::log</code>中(<code>[Sandbox]</code>前缀)。
  </p>
  
  <p>
    <strong>重载/重启</strong>：通过沙箱运行的方式，Zed严格地把所有应用包和扩展代码从编辑器本身区分开来，这样你无需重启或重开编辑器窗口就可以编辑应用包并马上测试结果。只是你需要重载你的配置文件(<code>config.json</code>)，为此你可以运行<code>Configuration:Reload</code>命令。如果你修改你的JavaScript代码，运行<code>Sandbox:Reset</code>命令，Zed会重载这些文件，你就可以看到修改的情况。
  </p>
  
  <p>
    <strong>Protip</strong>：如果你要做很多Zed应用包的开发工作，最好是把<code>Configuration:Reload</code>和<code>Sandbox:Reset</code>命令绑定给键组合。譬如我在我的<code>/user.json</code>文件里：
  </p>
  
  <pre><code>keys: {
    "Sandbox:Reset": "Ctrl-Shift-S",
    "Configuration:Reload": "Ctrl-Alt-Shift-S"
}
</code></pre>
  
  <p>
    <strong>常见问题</strong>：
  </p>
  
  <ul>
    <li>
      如果在你添加你的应用包到<code>/user.json</code>文件中的<code>packages</code>键后，配置一直在重载，一个可能的原因是，<code>package.json</code>中定义的URI与应用包的路径不匹配。换句话说，如果你的的应用包URI是<code>gh:abc/def</code>，则你的<code>package.json</code>必须放在<code>/packages/gh/abc/def/package.json</code>位置。如果不是，循环的问题就会出现。
    </li>
    <li>
      如果安装或运行应用包时，你在<code>zed::log</code>里看到404错误，则问题很可能出在你<code>package.json</code>文件中的<code>files</code>列表。如果安装应用包时出现404,请确保<code>package.json</code>里<code>files</code>键列出的文件均存在。如果404出现在安装后的测试中，则确保Zed声称找不到的文件出现在你的<code>package.json</code>文件里的<code>files</code>键下。
    </li>
  </ul>
  
  <p>
    这就好了！让我们看看你能开发出什么！
  </p>
</div>