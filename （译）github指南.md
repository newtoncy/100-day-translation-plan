# （译）github指南——仿照某如的100天翻译计划

- The **Hello World** project is a time-honored tradition in computer programming. It is a simple exercise that gets you started when learning something new. Let’s get started with GitHub!

- hello world 项目是电脑编程历史悠久的传统。这是一个简单的练习，当你学习一些新的东西的时候。让我们开始使用github吧

- 

  **You’ll learn how to:**

  - Create and use a repository
  - Start and manage a new branch
  - Make changes to a file and push them to GitHub as commits
  - Open and merge a pull request

- 

  **你将会学到：**

  - 创建和使用仓库
  - 开始和管理一个新的分支
  - 对文件进行更改和提交到github
  - 打开和合并一个pull request

- **What is GitHub?**

  GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

  This tutorial teaches you GitHub essentials like *repositories*, *branches*, *commits*, and *Pull Requests*. You’ll create your own Hello World repository and learn GitHub’s Pull Request workflow, a popular way to create and review code.

- **什么是github**

  Github是一个用于版本控制与合作开发的代码托管平台，它能让你和你的小伙伴在任何地方协同工作。

  这个教程会教你github的要点，包括仓库，分支，提交，和拉取请求。你将创建你的Hello World 仓库，学习拉取请求的工作流，一种流行的方式创建和审核代码

- #### No coding necessary

  To complete this tutorial, you need a [GitHub.com account](http://github.com/) and Internet access. You don’t need to know how to code, use the command line, or install Git (the version control software GitHub is built on).

  > **Tip:** Open this guide in a separate browser window (or tab) so you can see it while you complete the steps in the tutorial.

- **没有码代码的必要**

  为了完成这个教程你需要有一个[github的账号](http://github.com/) 和网络许可。你不需要懂代码和命令行或者安装安装Git（github基于此）

  > **提示：**当你照着教程做的时候，你可以开一个新的浏览器窗口来看这篇教程。这样你就可以一边看教程一边做了

- **Step 1. Create a Repository**

     A **repository** is usually used to organize a single project. Repositories can contain folders and files, images, videos, spreadsheets, and data sets – anything your project needs. We recommend including a *README*, or a file with information about your project. GitHub makes it easy to add one at the same time you create your new repository. *It also offers other common options such as a license file.*

     Your `hello-world` repository can be a place where you store ideas, resources, or even share and discuss things with others.

- **步骤1，创建一个仓库**

     一个**仓库**通常被用来开始一个项目。仓库可以包含文件夹，文件，图片，视频，电子表单，和数据库——任何你项目需要的东西。我们推荐包含一个README,或者一个包含你项目信息的文件。github可以简单的在你创建新仓库的时候加上一个。它也会提供给你一些常用的选项比如许可文件

     你的```hello-world```仓库可以成为你储藏想法，资源甚至和别人分享和讨论东西的地方

- ### To create a new repository

  1. In the upper right corner, next to your avatar or identicon, click  and then select **New repository**.
  2. Name your repository `hello-world`.
  3. Write a short description.
  4. Select **Initialize this repository with a README**.

  ![new-repo-form](https://guides.github.com/activities/hello-world/create-new-repo.png)

  Click **Create repository**. ![:tada:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f389.png)

- **创建一个新仓库**

  1. 在右上方的角落，你头像和id的右边，点击加号然后选新仓库
  2. 命名你的仓库为```hello-world```
  3. 写一个短小的描述
  4. 选择初始化仓库，并附一个readme

  点击创建仓库![:tada:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f389.png)

- **Step 2. Create a Branch**

     **Branching** is the way to work on different versions of a repository at one time.

     By default your repository has one branch named `master`which is considered to be the definitive branch. We use branches to experiment and make edits before committing them to `master`.

     When you create a branch off the `master` branch, you’re making a copy, or snapshot, of `master` as it was at that point in time. If someone else made changes to the `master`branch while you were working on your branch, you could pull in those updates.

- 步骤二，创建一个分支

     分支是一种同一时间在不同的版本上工作的方法。在默认情况下，你的仓库有一个叫``master``的分支，我们认为这个分支应该是一个明确的分支。在提交到master之前，我们在分支上实验和编辑。

     当你从master分支创建分支时。你实际上是建立了一个master当前的拷贝或者说快照。当你在工作在分支上时，其他人修改了master分支，你可以拉取他们对master做的修改

- This diagram shows:

     - The `master` branch
     - A new branch called `feature` (because we’re doing ‘feature work’ on this branch)
     - The journey that `feature` takes before it’s merged into `master`

     ![a branch](https://guides.github.com/activities/hello-world/branching.png)

     Have you ever saved different versions of a file? Something like:

     - `story.txt`
     - `story-joe-edit.txt`
     - `story-joe-edit-reviewed.txt`

     Branches accomplish similar goals in GitHub repositories.

     Here at GitHub, our developers, writers, and designers use branches for keeping bug fixes and feature work separate from our `master` (production) branch. When a change is ready, they merge their branch into `master`.

- 这个图片显示了：

     - master分支
     - 一个新的名叫feature的分支（因为我们在这个分支上做“功能开发”）
     - feature在提交到服务器之前经历的

     ![a branch](https://guides.github.com/activities/hello-world/branching.png)

     你之前有没有保存过不同版本的文件，类似这种：

     - 故事.txt
     - 故事-joe-编辑.txt
     - 故事-joe-编辑-审核.txt

     在github上，分支实现了相同的目标

     在github上，我们的开发者，作者，和设计师使用分支来使修理bug和开发功能从master分支分离。当修改就绪，我们合并分支到master

- ### To create a new branch

     1. Go to your new repository `hello-world`.
     2. Click the drop down at the top of the file list that says **branch: master**.
     3. Type a branch name, `readme-edits`, into the new branch text box.
     4. Select the blue **Create branch** box or hit “Enter” on your keyboard.

     ![branch gif](https://guides.github.com/activities/hello-world/readme-edits.gif)

     Now you have two branches, `master` and `readme-edits`. They look exactly the same, but not for long! Next we’ll add our changes to the new branch.

- 创建一个新分支

     1. 进入你的新仓库hello-world
     2. 点击文件列表顶部写着branch:master的下拉表
     3. 输入分支名，
