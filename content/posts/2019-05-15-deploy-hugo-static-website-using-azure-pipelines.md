---
template: post
title: Deploy Hugo Static Website Using Azure Pipelines
slug: /posts/2019/deploy-hugo-static-website-using-azure-pipelines/
draft: false
date: 2019-03-16T10:32:08.253Z
description: >-
  Goodbye wordpress and hello [Hugo](https://gohugo.io), finaly switched over to
  static Website and ligthspeed! Why use static website?
category: blog
tags:
  - Hugo
  - Azure
  - DevOps
---
Goodbye wordpress and hello [Hugo](https://gohugo.io), finaly switched over to static Website and ligthspeed! Why use static website?

Improved performance, security and ease of use are just a few of the reasons static site generators are so appealing. The purpose of website generators is to render content into HTML files.

Today this conten is on Azure blobs and Static website, so I will show you how I managed to get this site up and running.
##### Setup Static Website on Azure
1. Crete an Storage account where your contes is gona live on.
2.  Open your Storage account and Static Website

![](/img/2019/Azure1.png)

Provide your domain where your blog is using.

![](/img/2019/Azure18.png)

3. Enable Static Website, type index.html and 404.html and click save.

![](/img/2019/Azure2.png)
Now our blobs will create an special folder named __$web__, here will our contens live.

##### Setup Azure Pipelines
1. Go to [Azure DevOps](https://dev.azure.com/) login or create an free account.
2. Create new project
3. Choose a name and what visibility your project should be.
![](/media/hugo/Azure3.png)
Congratulations, you have an empty project!

4. You should decide where you want to store your raw data, you could have them on GitHub or Azure Repos. I did choose Azure Repos for my project. Do not uploade your __public__ folder, this is bacause our pipeline will create one for us later on.
5. Go to Pipelines and releases.
![](/media/hugo/Azure4.png)
6. There is no Pipelines created yet, so go ahead and create an new. Click __New Pipeline.__
7. Next you choose __Empty job__
![](/media/hugo/Azure5.png)
8. Next you could change name on the stage name to something different.
![](/media/hugo/Azure6.png)
9. Click on __Add an artifact__
![](/media/hugo/Azure7.png)
10. Choose where your repo is, here we are using Azure repos
![](/media/hugo/Azure8.png)
11. Next we will add the task it self, click view stage tasks.
![](/media/hugo/Azure9.png)
12. At this stage we can see our stage is pretty boring, so press the __+ Add__
![](/media/hugo/Azure10.png)
13. Go to the __Markedplace__ and search after __Hugo__ and install the job, after its installed add it to your stage.
![](/media/Azure20.png)
14. Add your sorce and destination, an important note here is in your source you need to add ```$(System.DefaultWorkingDirectory)/_My blog``` and in the destination you add ```$(System.DefaultWorkingDirectory)/_My blog\publish```
![](/img/2019/Azure11.png)
15. Next we will add an job for uploade our contents to Azure blob storage. Press the __+ Add__ sign and search after __Azure File Copy__
![](/img/2019/Azure19.png)
16. Now open our newly created job for __Azure File Copy__ and choose the source and add __\public__ at the end. And then add your blob storage where you want the site to be on. And the last step is to add __$web__ under conteinar name and click save.
![](/img/2019/Azure12.png)
17. You should have two jobs like this:
![](/img/2019/Azure13.png)
18. You should have something like this now in your pipeline:
![](/img/2019/Azure14.png)
19. You could try to run your pipeline by deploying it and after it have run all the mark should be green
![](/img/2019/Azure15.png)
20. But I would have this pipeline to run automatic when new files is added to my repo, so lets add an Continuous deployment trigger to our pipeline. Go back to your pipeline and press the lighting icone.
![](/img/2019/Azure16.png)
21. Enable Continuous deployment trigger:
![](/img/2019/Azure17.png)
Next time you update your repo our pipeline will generete contents for our blog!
