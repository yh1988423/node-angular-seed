#使用说明

##获取yeoman-bootstrap3-angular-express-seed

    使用Webstorm7，启动时选择check out from version control:
    1.git的url：https://github.com/by90/yeoman-bootstrap3-angular-express-seed.git
    2.本地路径：E:\
    3.项目名称：yeoman-bootstrap3-angular-express-seed
    注意，我们的默认分支是develop，此后需要将master分支pull到本地。
    Webstorm7集成了karma，可在terminal中执行命令，我们无需切换到命令窗口，Terminal窗口本身是在项目的根目录下

##运行yeoman-bootstrap3-angular-express-seed

    1.全局安装yeoman及相应的npm包：
        npm install -g yo bower grunt-cli karma karma-ng-scenario jasmine phantomjs
    2.在yeoman-bootstrap3-angular-express-seed目录下，打开命令行窗口
        npm install
        bower install
    3.设置环境变量：
        为了访问全局安装的npm模块，需要环境变量NODE_PATH，本机为：C:\Users\Administrator\AppData\Roaming\npm\node_modules
        对使用phantomjs浏览器，需要增加环境变量PHANTOMJS_BIN：C:/Users/Administrator/AppData/Roaming/npm/node_modules/phantomjs/lib/phantom/phantomjs.exe
        为使用chorme浏览器，需增加环境变量CHROME_BIN："C:\Program Files (x86)\Google\Chrome\Application\CHROME\chrome.exe"
    4.运行app.js，相关运行配置已经创建
    5.运行e2e测试：命令窗口下执行grunt E2eTest
    6.运行前端单元测试：命令窗口下执行grunt UnitTest  
    7.同时执行前端单元测试、e2e测试和服务端单元测试：命令窗口下执行grunt test
    8.局域网访问：
    windows下，进入控制面板\所有控制面板项\Windows 防火墙，然后在左侧选择：允许应用通过windows防火墙进行通信。  
    此后，选node.js，在网络类型中将专用和共用都勾上。通过手机的安卓浏览器访问，本模版的字体非常小，后面需要使用bootstrap3  
    优化。不过angular的表现不错，导航按钮能正常工作。这样测试下，能增进些感性的认知。  

##Bower介绍：

###使用的前端包：
    1.Angular最新版本(稳定版1.08,1.2rc2版本需要指明commit)注意写法："1.2.0-rc.2"，命令方式为：  
        bower install angular#1.2.0-rc.2 -S  
    2.bootstrap最新版本(3.0)已经是正式版，直接处理即可  
    3.angular-bootstrap最新版本,这个比较麻烦，我们指定git所在位置，然后重新编译  
 
###Bower的要点：
    1.项目根目录bower的两个配置文件含义：  
       .bowerrc  描述bower下载回来的库，放在哪个文件夹，这个文件夹我们将在.gitignore文件中忽略掉  
        bower.json  描述我们需要的是哪些包，类似"~1.0.8"的写法表示大于1.08版  
    2.安装指定的Commit和指定的zip：  
        bower从0.93版本开始支持安装指定的commit和zip，由于angular-bootstrap不支持bs3，这里使用的是其/bootstrap3_bis2分支：  
    指明zip包，在配置文件中这么写：  
    "angular-bootstrap":"https://github.com/angular-ui/bootstrap/archive/bootstrap3_bis2.zip"  
    或者指明commit的id，这么写：  
    "angular-bootstrap":"https://github.com/angular-ui/bootstrap.git#8cbeff0ffe960f5f46b9b886fa3db2d0c1ff2a9f"  
    需要重新build，在E:\Queue\app\lib\angular-bootstrap目录中打开命令窗体，然后npm install，再然后grunt build即可,重新  
    编译的结果在E:\Queue\app\lib\angular-bootstrap\dist目录里。  
    3.安装命令写入到json  
        我们使用bower命令，均在项目根目录下。该目录由bower.json，只要我们加上-F，可写入依赖。加-D，可写入开发依赖。 

##Karma介绍：

###Karma是什么？
    首先会想到，既然同是使用jasmine，那么服务端测试是否也需要使用karma呢？
    请注意：karma是前端的测试运行器，主要的概念是前端使用何种浏览器、使用何种框架格式来写单元测试,方便不同人以不同格式书写
    单元测试、在不同浏览器上测试。但服务端测试，我们安装的jasmine-node，实际上是无需指定浏览器的、当然也根本用不着指定何种
    单元测试格式。所以追求同样使用karma来运行测试是无意义的。

###karma能否全局安装？
    我们全局安装karma后，前端项目中缺少karma-ng-scenario，当然，在项目的开发依赖中加上的话，karma也会全套的安装在项目根目录。
    我们将karma-ng-scenario全局安装，则单元测试和e2e测试会报错：找不到karma
    这是很常见的问题，解决方法是设置系统环境变量NODE_PATH,其值为全局npm目录，如下：
    C:\Users\Administrator\AppData\Roaming\npm\node_modules
    重启后，在项目本地不安装karma的情形下，单元测试顺利运行。


###Webstorm7集成karma
    以运行e2e测试为例：
        Run|Edit configuration
        然后点加号，增加karma运行配置
        config file设为：E:\yeoman-bootstrap3-angular-express-seed\config\karma-e2e.conf.js
        这是我们实际设置的。要注意：需要加入phantomjs的环境变量，加入后需要重启电脑确认。同时，测试运行前应启动express
        服务器。我们没有在项目目录安装karma，所以运行配置中，使用的-g安装的karma，其目录路径预设为：
        karma node package：C:\Users\Administrator\AppData\Roaming\npm\node_modules\karma


       
##grunt介绍

###grunt是什么
    grunt是一个任务执行工具。grunt目前是0.41版本，与0.3版的区别是，grunt已经分成grunt-cli、grunt和grunt-init三个部分。
    其中grunt-cli必须全局安装，用来执行各项目中的grunt，只是个执行器。grunt必须在每个项目中本地安装，这是为了避免不同
    项目中因为插件不同导致冲突。grunt-init我们暂时用不到。
###安装grunt
    首先全局安装grunt-cli
        npm install -g grunt-cli
        当然，这部分我们在yeoman整体安装的时候已经解决，所以忽略。
    然后在项目根目录下本地安装grunt，并写入项目的开发依赖，注意：此时IDE不可打开package.json文件，否则不会自动写入依赖。
        npm install grunt  --save-dev
    最后安装我们所需的Grunt插件,比如，为了运行express服务器，需要安装两个grunt插件：
        npm install grunt-contrib-watch --save-dev
        npm install grunt-express-server --save-dev
    为了简化npm任务的初始化，我们需要第三个包：
        npm install matchdep --save-dev
    这样我们能在GruntFile.js中用一行代码载入需要的任务：
        require('matchdep').filterDev('grunt-*').forEach(grunt.loadNpmTasks);

###GruntFile.js中的路径问题
    GruntFile.js的watch的写法,我们出现一个问题：
    watch: {
            express: {
                files: [
                    './server/app.js'
                ],
                tasks: ['express:dev'],
                options: {
                    livereload: true,
                    nospawn: true //Without this option specified express won't be reloaded
                }
            }
        }//watch
    这导致watch不停报错以至堆栈溢出。'./server/app.js'改为 'server\\app.js'后正常。之后应改为正常的path写法以适应windows和
    linux两种情形。   
     
###Grunt与WebStorm集成：
    file|settings|external tools，然后点+增加一个工具
    1、group填写grunt，表示这类任务均归于grunt菜单
    2、name：default
    3、program填写：C:\Users\Administrator\AppData\Roaming\npm\grunt.cmd
    4、parameters：default   当然，默认任务可以不填写参数
    5、woring directory：$ProjectFileDir$   表示以项目根目录为主
    添加之后，在编辑器中右键，可以看到group菜单组，有一个字菜单名为default，点击则可正常运行。

##服务端测试的执行步骤
    1.全局安装jasmine-node
    2.创建服务端单元测试运行配置：
        node.js路径：默认
        working dir：项目根目录，默认。
        js文件路径：C:\Users\Administrator\AppData\Roaming\npm\node_modules\jasmine-node\bin\jasmine-node
        aplication参数：./test/server/ --verbose
    3、我们约定将服务端测试放在项目的test\server目录下，后缀为*spec.js
    4、grunt执行jasmine-node测试：这个是需要处理的，各类测试灵活配置、前后端一次跑完...

###grunt运行jasmine-node的测试：
    GruntFile.js里的initConfig部分，那些键值定义任务，其名称不能修改，根据相应的插件命名。使用grunt-jasmine-node的时候，任务  
    的定义，其名称为jasmine_node，注意是下划线，这和使用grunt-contrib-jasmine-node的时候变量名为jasmine-node不同。
    这个简单的细节折腾了不少时间。

##V0.1 ChangeLog
    使用bower管理前端依赖的包
    使用express server取代angular-seed项目中的简单脚本，原有的测试均能运行    
    使用Grunt运行前端单元测试、e2e测试和服务端测试
    运行前端测试时自动启动express服务器 

#Todo...    
##v0.2 build
    运行单元测试、清理、html压缩、css压缩、图片压缩、拷贝。
    合并，考虑到angular页面或有不妥，暂不处理
    我们使用build创建一个可马上拷贝、部署、运行的版本。

##v0.3 前端页面使用bootstrap 3
处理导航
处理页面布局
