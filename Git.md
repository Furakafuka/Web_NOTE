# Git*

## day1

1. 分布式版本控制系统
   1. 服务器保存文件的所有更新版本
   2. 客户端是服务器的完整备份，并不是只保留文件的最新版本
   3. 优点
      * 联网运行，支持多人协作开发
      * 客户端断网后支持离线本地提交版本更新
      * 服务器故障或损坏后，可使用任何一个客户端的备份进行恢复
2. Git
   1. 特性
      1. 直接记录快照，而非差异比较(SVN只记入差异$\triangle$)
      2. 近乎所有操作都是本地执行
      3. Git 快照
         1. 在原有文件版本的基础上重新生成一份新的文件，类似于备份。为了效率
         2. 如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件。
      4. 近乎所有操作都是本地执行
         1. 断网后依旧可以在本地对项目进行版本管理
         2. 联网后，把本地修改的记录同步到云端服务器即可
3. Git区域
   1. 使用 Git 管理的项目，拥有三个区域，分别是工作区、暂存区、Git 仓库。
   2. ![image-20220304175004000](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220304175004000.png)

### Git基础

1. 配置用户信息

   ```bash
   git config --global user.name "username"
   git config --global user.email "emailaddress"
   ```
2. 查看全局配置信息

   ```bash
   ＃查看所有的全局配置项 
   git config --list --global

   ＃ 查看指定的全局配置项
   git config user.name
   git config user.email
   ```
3. 查看帮助

   ```bash
   git help config
   git config -h #在窗口内查看
   ```
4. 获取Git仓库:

   1. 将尚未进行版本控制的本地目录转换为 Git 仓库
   2. 从其它服务器克隆一个已存在的 Git 仓库

   ### 本地目录转换为 Git 仓库


   1. 初始化仓库

      1. 在项目文件夹中打开git bash
      2. 执行 ``git bash``
   2. 检查文件状态

      1. 使用 ``git status``查看
      2. ```bash
         1 ＃ 以精简的方式显示文件状态

         2 git status-s

         3 git status --short
         ```
   3. 跟踪新文件

      1. 使用命令 ``git add``开始跟踪一个文件。
      2. 绿色的A表明文件已被跟踪，并处于暂存状态
   4. 提交更新

      1. 执行 ``git commit``命令进行提交,其中 -m 选项后面是本次的提交消息，用来对提交的内容做进一步的描述
   5. 文件的commit

      1. 已修改但未提交的文件显示的是红色的M

         ```bash
         $ git status -s
         M mytext.txt
         ```
      2. 已修改且提交到暂存区中(绿色的M)

         ```bash
         git add mytext.txt
         ```
      3. 提交到给git仓库

         ```bash
         git commit -m "已修改的txt"
         ```
      4. 撤销对文件的修改

         1. 把对工作区中对应文件的修改，还原成 Git 仓库中所保存的版本。
         2. 所有的修改会丢失，且无法恢复！危险性比较高，请慎重操作！
         3. ```bash
            git checkout -- mytext.txt
            ```
      5. 添加多个文件

         1. ```bash
            git add .
            ```
      6. 移除暂存区文件

         ```bash
         git reset HEAD 
         ```
   6. 跳过暂存区域

      1. ```bash
         git commit -a -m "描述信息"
         ```
   7. 移除文件

      1. ```bash
         1#从Git仓库和工作区中同时移除index.js文件
         2 git rm -f index.js
         3#只从Git仓库中移除index.css，但保留工作区中的index.css文件
         4 git rm --cached index.cSS
         ```
      2. 移除后文件为绿色的D
   8. 忽略文件

      1. 文件 .gitignore 的格式规范如下：

         1. 以 # 开头的是注释
         2. 以 / 结尾的是目录
         3. 以 / 开头防止递归
         4. 以 ! 开头表示取反
         5. 可以使用 glob 模式进行文件和文件夹的匹配（glob 指简化了的正则表达式）
            1. 星号 * 匹配零个或多个任意字符
            2. [abc] 匹配任何一个列在方括号中的字符 （此案例匹配一个 a 或匹配一个 b 或匹配一个 c）
            3. 问号 ? 只匹配一个任意字符
            4. 在方括号中使用短划线分隔两个字符， 表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配
               所有 0 到 9 的数字）
            5. 两个星号 ** 表示匹配任意中间目录（比如 a/**/z 可以匹配 a/z 、 a/b/z 或 a/b/c/z 等）
      2. 示例:![image-20220304191703197](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220304191703197.png)
      3. 查看提交历史

         ```bash
         1＃ 按时间先后顺序列出所有的提交历史，最近的提交排在最上面

         2 git log

         3

         4＃只展示最新的两条提交历史，数字可以按需进行填写

         5 git log -2

         6

         7＃在一行上展示最近两条提交历史的信息

         8 git log -2--pretty-oneline

         9

         10＃在一行上展示最近两条提交历史的信息，并自定义输出的格式

         11＃％h 提交的简写哈希值 ％an作者名字 ％ar作者修订日期，按多久以前的方式显示

         ％s提交说明

         12 git log-2--pretty=format:"%h | %an | %ar | %s"
         ```
   9. 回退版本

      ```bash
      1＃在一行上展示所有的提交历史
      2 git log --pretty=oneline
      3
      4 ＃ 使用 git reset ——hard 命令，根据指定的提交 ID 回退到指定版本
      5 git reset  -hard 
      6
      7＃在旧版本中使用 git reflog --pretty＝oneline 命令，查看命令操作的历史
      8 git reflog -pretty=oneline
      9
      10＃再次根据最新的提交 ID，跳转到最新的版本
      11 git reset --hard 
      ```

## GITHUB

1. 开源协议

   1. BSD（Berkeley Software Distribution）
   2. Apache Licence 2.0
   3. GPL（GNU General Public License）
      * 具有传染性的一种开源协议，不允许修改后和衍生的代码做为闭源的商业软件发布和销售
      * 使用 GPL 的最著名的软件项目是：Linux
   4. LGPL（GNU Lesser General Public License）
   5. MIT（Massachusetts Institute of Technology, MIT）
      * 是目前限制最少的协议，唯一的条件：在修改后的代码或者发行包中，必须包含原作者的许可信息
      * 使用 MIT 的软件项目有：jquery、Node.js
2. Github

   1. 关注自己喜欢的开源项目，为其点赞打 call
   2. 为自己喜欢的开源项目做贡献（Pull Request）
   3. 和开源项目的作者讨论 Bug 和提需求 （Issues）
   4. 把喜欢的项目复制一份作为自己的项目进行修改（Fork）
3. 远程仓库访问

   1. HTTPS：零配置；但是每次访问仓库时，需要重复输入 Github 的账号和密码才能访问成功
   2. SSH：需要进行额外的配置；但是配置成功后，每次访问仓库时，不需重复输入 Github 的账号和密码
   3. HTTP:![image-20220304200902107](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220304200902107.png)

      1. 第二次及之后只需要运行 ``git push``就可同步
   4. SSH Key

      1. 免登录的加密数据传输
      2. 组成

         1. id_rsa（私钥文件，存放于客户端的电脑中即可）
         2. id_rsa.pub（公钥文件，需要配置到 Github 中)
      3. 配置:

         1. ```bash
            # 运行如下命令
            ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
            ```
         2. ```bash
            # 检测是否配置成功
            ssh -T git@github.com

            Hi Furakafuka! You've successfully authenticated, but GitHub does not provide shell access.
            ```
         3. 连接Github

            ```bash
            git remote add origin git@github.com:Furakafuka/test02.git
            git branch -M main
            git push -u origin main
            ```
   5. 克隆到本地

      1. ```bash
         git clone @address
         ```
4. 分支

   1. 在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发

      ![image-20220304203901664](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220304203901664.png)
   2. 本地分支

      1. 本地分支:``git branch``
      2. 创建分支:``git branch 新分支的名字``
      3. 切换分支:``git checkout 分支名``
      4. 分支的快速创建和切换:``git checkout -b 分支名称``
      5. 合并分支:

         ```bash
         1＃切换到 master 分支
         2 git checkout master
         3＃在 master 分支上运行 git merge 命令，将 login 分支的代码合并到 master 分支
         4 git merge login
         ```
         ![image-20220304204732440](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220304204732440.png)
      6. 删除分支:``git branch -d 分支名称``

         1. 要在主分支上执行命令
      7. 分支冲突

         1. 对同一个文件进行了不同的修改，Git 就没法干净的合并它们
         2. ```bash
            1＃ 假设：在把 reg 分支合并到 master 分支期间，代码发生了冲突
            2 git checkout master
            3 git merge reg
            4
            5＃打开包含冲突的文件，手动解决冲突之后，再执行如下的命令
            6 git add.
            7 git commit —m“解决了分支合并冲突的问题＂
            ```
      8. 推送分支

         1. ```bash
            1＃—u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带—u参数
            2 git push—u 远程仓库的别名 本地分支名称：远程分支名称
            3
            4＃ 实际案例：
            5 git push -u origin payment:pay
            6
            7＃如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化：
            8 git push -u origin payment
            ```
      9. 跟踪分支

         1. 从远程仓库中，把远程分支下载到本地仓库中
         2. ```bash
            1＃从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
            2 git checkout 远程分支的名称
            3＃示例：
            4 git checkout pay
            5
            6＃从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
            7 git checkout —b 本地分支名称 远程仓库名称／远程分支名称
            8＃ 示例：
            9 git checkout -b payment origin/pay
            ```
      10. 拉取远程分支的最新的代码:``git pull``
      11. 删除分支 ``git push 远程仓库名称 --delete 远程分支名称``
