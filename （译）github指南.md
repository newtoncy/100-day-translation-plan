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

- ## **Step 1. Create a Repository**

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

- ## **Step 2. Create a Branch**

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
     3. 在新分支的文本框中输入分支名“readme-edits”
     4. 选择蓝色的创建新分支框或者按下回车键

     现在你有了两个分支master和readme-edits。他们看起来一样不过以后就不会了！我们现在在新分支上修改

- ## Step 3. Make and commit changes

     Bravo! Now, you’re on the code view for your `readme-edits` branch, which is a copy of `master`. Let’s make some edits.

     On GitHub, saved changes are called *commits*. Each commit has an associated *commit message*, which is a description explaining why a particular change was made. Commit messages capture the history of your changes, so other contributors can understand what you’ve done and why.

     #### Make and commit changes

     1. Click the `README.md` file.
     2. Click the  pencil icon in the upper right corner of the file view to edit.
     3. In the editor, write a bit about yourself.
     4. Write a commit message that describes your changes.
     5. Click **Commit changes** button.

     ![commit](https://guides.github.com/activities/hello-world/commit.png)

     These changes will be made to just the README file on your `readme-edits` branch, so now this branch contains content that’s different from `master`.

- 提交一个更改

     1. 点击readme.md文件
     2. 点击文件视图右上角的铅笔按钮
     3. 在编辑器中写一些有关于自己的东西
     4. 写一个提交信息来描述你的更改
     5. 点击提交更改按钮

     这个更改仅作用于 ``readme-edits``分支，现在，这个分支容纳的内容就和``master``分支不同了

- ## Step 4. Open a Pull Request

     Nice edits! Now that you have changes in a branch off of `master`, you can open a *pull request*.

     Pull Requests are the heart of collaboration on GitHub. When you open a *pull request*, you’re proposing your changes and requesting that someone review and pull in your contribution and merge them into their branch. Pull requests show *diffs*, or differences, of the content from both branches. The changes, additions, and subtractions are shown in green and red.

     As soon as you make a commit, you can open a pull request and start a discussion, even before the code is finished.

     By using GitHub’s [@mention system](https://help.github.com/articles/about-writing-and-formatting-on-github/#text-formatting-toolbar) in your pull request message, you can ask for feedback from specific people or teams, whether they’re down the hall or 10 time zones away.

     You can even open pull requests in your own repository and merge them yourself. It’s a great way to learn the GitHub flow before working on larger projects.

- **步骤四，建立一个pull request**

     写的不错！现在你在master分支以外的分支做了修改。你可以建立一个*pull request*了。

     Pull Request是github协作的核心。当你建立一个pull request的时候，你是在提交你的修改并请求某个人审查，拉取你的贡献并合并到他们的分支中。pull requeset展示了两个分支的*diff*，或者说是"不同"。更改，增加和删除用绿色和红色展示了出来。

     在你提交的同时，你可以建立一个pull request并开始一个讨论。即使你还没完成代码。

     通过在你的pull request中使用github的提示系统[@mention system](https://help.github.com/articles/about-writing-and-formatting-on-github/#text-formatting-toolbar) 不管和他们是共处一室还是在十个时区之外你都可以得到反馈。

     你甚至可以给自己的仓库建立拉取请求然后自己合并。在你进入大团队之前，这是一个学习github流程的好方法。

- #### Open a Pull Request for changes to the README

     *Click on the image for a larger version*

     | Step                                                         | Screenshot                                                   |
     | ------------------------------------------------------------ | ------------------------------------------------------------ |
     | Click the  **Pull Request** tab, then from the Pull Request page, click the green **New pull request** button. | [![pr-tab](https://guides.github.com/activities/hello-world/pr-tab.gif)](https://guides.github.com/activities/hello-world/pr-tab.gif) |
     | In the **Example Comparisons**box, select the branch you made, `readme-edits`, to compare with `master` (the original). | [![branch](https://guides.github.com/activities/hello-world/pick-branch.png)](https://guides.github.com/activities/hello-world/pick-branch.png) |
     | Look over your changes in the diffs on the Compare page, make sure they’re what you want to submit. | [![diff](https://guides.github.com/activities/hello-world/diff.png)](https://guides.github.com/activities/hello-world/diff.png) |
     | When you’re satisfied that these are the changes you want to submit, click the big green **Create Pull Request**button. | [![create-pull](https://guides.github.com/activities/hello-world/create-pr.png)](https://guides.github.com/activities/hello-world/create-pr.png) |
     | Give your pull request a title and write a brief description of your changes. | [![pr-form](https://guides.github.com/activities/hello-world/pr-form.png)](https://guides.github.com/activities/hello-world/pr-form.png) |

     When you’re done with your message, click **Create pull request**!

     ------

     > **Tip**: You can use [emoji](https://help.github.com/articles/basic-writing-and-formatting-syntax/#using-emoji) and [drag and drop images and gifs](https://help.github.com/articles/file-attachments-on-issues-and-pull-requests/) onto comments and Pull Requests.

- #### 建立拉取请求来更改readme

  点击图片获得大图

  | 步骤                                                         | 截屏                                                         |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 点击**Pull Request**标签然后在拉取请求页点击绿色的new pull request 按钮 | [![pr-tab](https://guides.github.com/activities/hello-world/pr-tab.gif)](https://guides.github.com/activities/hello-world/pr-tab.gif) |
  | 在示例比较框？？中选择你的readme-edits,与master比较          | [![branch](https://guides.github.com/activities/hello-world/pick-branch.png)](https://guides.github.com/activities/hello-world/pick-branch.png) |
  | 在Compare page查看你的更改，确认这是你想要提交的             | [![diff](https://guides.github.com/activities/hello-world/diff.png)](https://guides.github.com/activities/hello-world/diff.png) |
  | 你很满意你要提交的更改，点击绿色的大按钮**Create Pull Request** | [![create-pull](https://guides.github.com/activities/hello-world/create-pr.png)](https://guides.github.com/activities/hello-world/create-pr.png) |
  | 为你的提交给一个标题和描述                                   | [![pr-form](https://guides.github.com/activities/hello-world/pr-form.png)](https://guides.github.com/activities/hello-world/pr-form.png) |

  当你写完了你的消息， 点 **Create pull request**!

  ------

  > **Tip**: 你可以加emoji和拖放图片

- ## Request

  In this final step, it’s time to bring your changes together – merging your `readme-edits` branch into the `master`branch.

  1. Click the green **Merge pull request** button to merge the changes into `master`.
  2. Click **Confirm merge**.
  3. Go ahead and delete the branch, since its changes have been incorporated, with the **Delete branch** button in the purple box.

  ![merge](https://guides.github.com/activities/hello-world/merge-button.png)![delete](https://guides.github.com/activities/hello-world/delete-button.png)

  ### Celebrate!

  By completing this tutorial, you’ve learned to create a project and make a pull request on GitHub! ![:tada:](https://assets-cdn.github.com/images/icons/emoji/unicode/1f389.png) ![:octocat:](https://assets-cdn.github.com/images/icons/emoji/octocat.png) ![:zap:](https://assets-cdn.github.com/images/icons/emoji/unicode/26a1.png)

  Here’s what you accomplished in this tutorial:

  - Created an open source repository
  - Started and managed a new branch
  - Changed a file and committed those changes to GitHub
  - Opened and merged a Pull Request

  Take a look at your GitHub profile and you’ll see your new [contribution squares](https://help.github.com/articles/viewing-contributions)!

  To learn more about the power of Pull Requests, we recommend reading the [GitHub flow Guide](http://guides.github.com/overviews/flow/). You might also visit [GitHub Explore](http://github.com/explore) and get involved in an Open Source project ![:octocat:](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

  ------

  > **Tip**: Check out our other [Guides](http://guides.github.com/), [YouTube Channel](http://youtube.com/githubguides) and [On-Demand Training](https://services.github.com/on-demand/) for more on how to get started with GitHub.

- 步骤5，合并你的拉取请求

  在最后一步，是时候将你的修改合并到主分支了。

  1. 点击**Merge pull request**合并主分支
  2. 点**Confirm merge**.
  3. 因为它们已经合并，所以继续并删除分支，删除按钮在紫色框内

  **可喜可贺**！

  完成了这个教程，你已经学会了在github上创建项目，建立拉取请求。

  以下是你在教程中掌握的：

  - 创项目
  - 建分支
  - 修改和提交
  - 拉取请求

  在github个人资料中你会看到一个新贡献

  为了更好的了解拉取请求的强大，我们建议你看一看github流程，你也许想访问github探索，并涉足一个开源项目
