# git 笔记

1. 安装

	1.1 成功标志

		出现 'Git -> Git Bash' ,说明安装成功

	1.2 设置

		git config --global user.name "yourName"
		git config --global uaer.email "email@xx.com"

		-- global 参数表示本台计算机上所有的Git仓库都会使用这个配置,也可以对某个仓库指定不同的用户名和Email地址

2. 创建一个版本库(repository)

	2.1 创建一个目录

		mkdir xxx
		exp:
			创建一个名为:gitTest的目录
				1.mkdir gitTes

	2.2 将目录变为 Git 可以管理的

		git init
		exp: 
			将gitTest变为 Git 可以管理的
				1. cd gitTest //进入 gitTest目录
				2. git init

		当前目录下会多一个 .get 目录,这个目录是Git用来跟踪管理版本库的,没事千万不要手动修改这个目录里面的文件

3. 管理文件

	3.1 添加文件到仓库

		git add xxx
		exp:
			添加文件gitTest.txt到仓库中
				1.git add gitTest.txt

	3.2 提交文件

		git commit -m '描述信息'
		exp:
			提交
				1.git commit -m 'xxx'


4. 查看仓库当前状态

	4.1 查看仓库当前状态

		git status

	4.2 查看文件改变

		git diff xxx
		exp:
			查看gitTest.txt与版本库中的不同
				1.git diff gitTest.txt

5. 版本控制

	5.1 查看版本
		
		git log

	5.2 版本切换

		1.git reset --hard HEAD^(HEAD为当前版本,HEAD^为上个版本,HEAD~10为上10个版本)
		2.git reset --hard 版本号

	5.3 历史命令查看

		git reflog

6. 撤销修改

	6.1 丢弃工作区的修改

		git checkout -- xxx
		exp:
			撤销工作区gitTest.txt文件的修改
				1.git checkout -- gitgitTest.txt

		撤销结果:与仓库中或缓存区(add)相同

	6.2 撤销缓存区的修改

		git reset HEAD xxx
		exp:
			撤销缓存区gitTest.txt文件的修改
				1.git reset HEAD gitgitTest.txt

7. 删除

	7.1 本地删除

		若本地文件被删除,可通过 git checkout -- xxx 恢复

	7.2 仓库中删除

		git rm xxx

8. 添加远程仓库

	8.1 关联远程仓库
		
		git remote add origin xxx:xxx(git@github.com:michaelliao/learngit.git)

	8.2 删除关联

		git remote rm xxx
		
	8.3 推送

		git push -u origin master(只需在第一次提交加时加 -u 参数)			

9. 克隆仓库

	9.1 克隆仓库

		git clone xxx@xxx(git@github.com:michaelliao/learngit.git)

10. 分支管理

	10.1 创建分支

		git branch xxx
		exp:
			创建名为 dev 的分支
				1.git branch dev

	10.2 切换分支

		git checkout xxx
		exp:
			切换到名为 dev 的分支

	10.3 查看分支

		git branch
		exp:
			* dev
  			  master
              当前分支前标有 * 号

   	10.4 创建并切换分支(10.1 + 10.2)

		 git checkout -b xxx

	10.5 合并分支

		git merge xxx
		exp:
			合并 dev 分支到当前分支
				git merge dev
		会出现分支合并失败的可能,需手动解决冲突后提交成能完成合并
		
	10.6 删除分支

		git branch -d xxx
		exp:
			删除名为 dev 的分支
				git branch -d dev 