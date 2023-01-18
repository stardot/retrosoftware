# RS Mercurial DVCS Repository

## Introduction

Retro Software projects can make use of our *[Mercurial](http://mercurial.selenic.com/)* (aka hg) Distributed Version Control System (DVCS) repositories. *Mercurial* was chosen over the popular and more widely-known *Subversion* project because of the reported improvements in workflow, esp. in the area of merging. A good place to start investigating *Mercurial*, is the [hginit.com](http://hginit.com/) tutorial which also compares the system with *Subversion* and describes the issues *Mercurial* was designed to address.

Whilst not quite as widely-supported as *Subversion*, *Mercurial* tool support is good enough for most purposes. There is a *[Mercurial Eclipse](http://www.vectrace.com/mercurialeclipse/)* plugin as well as *[TortoiseHg](http://tortoisehg.bitbucket.org/)*, a GUI tool which integrates directly into Windows Explorer. Other RS forum members have also reported that there is a plugin to add integrated support into Microsoft's *Visual Studio*.

## Browse the RS *Mercurial* repositories online (read-only)

<http://www.retrosoftware.co.uk/hg/>

## Getting Started with the RS *Mercurial* repository and *TortoiseHg*

1.  Post your request in the [Retro Software Feedback and Site-Specific Chat](http://www.retrosoftware.co.uk/forum/viewforum.php?f=3) forum for either write access to an existing project, or to request a new project repository to be setup - include a short one-word name for the project (e.g. "mynewrsproject").
2.  When contacted, PM your preferred password to the RS administrator to allow the access to your requested projects to be configured.
3.  When you've confirmed you have the correct username / password and that your access to the repository has been configured, download and install *[TortoiseHg](http://tortoisehg.bitbucket.org/)* (requires a reboot). When Windows has been rebooted, you should be able to right-click in Windows Explorer and see the *TortoiseHg* context menu:
    ![](./images/Hgcontextmenu.png)
4.  If you need to (e.g. you're behind a corporate firewall), configure a proxy server now by selecting Global Settings from the *TortoiseHg* context menu and opening the Proxy settings:
    ![](./images/Hgproxysettings.png)
5.  Now configure your RS username used when committing by selecting Global Settings from the *TortoiseHg* context menu and opening the Commit settings. The Username field should be filled in with the form "**RetroSoftwareForumName <youremailaddress>**":
    ![](./images/Hgcommitsettings.png)
6.  Create a directory within Windows Explorer with the name of the project you are accessing. Clone the repository from the Retro Software server by selecting Clone... off the *TortoiseHg* context menu from within that directory, which will therefore be used as the base of your local repository. The Destination path should be automatically filled in, so enter the Source path in the form "**<http://www.retrosoftware.co.uk/hg/projectname>**". Check the Use proxy server box, if required and click the Clone button:
    ![](./images/Hgclonerepository.png)
    After a short time of downloading the contents of the repository, the local directory should look something like this:
    ![](./images/Hgrepocloned.png)
    ***Note:*** If the repository has been newly created for you, this step is still required and even though there are no other files until you create and commit them, you will still find a .hg directory is created to store the *Mercurial* meta-data for the repository.

## Quick Usage Reference

It is strongly advised that you at least read through the brief [hginit.com](http://hginit.com/) tutorial, if not the rest of the [*Mercurial* documentation](http://mercurial.selenic.com/guide/), which includes the O'Reilly text *[Mercurial: The Definitive Guide](http://hgbook.red-bean.com/read/)* by Bryan O'Sullivan, to understand how a typical DVCS workflow can be applied with *Mercurial*. Documented below, however, are a few of the initial operations which you may require at first, to give you an idea of how you can interact with the repository on the RS server.

### Adding files / directories

<table>
<tbody>
<tr class="odd">
<td><p>![](./images/Hgaddfile.png)
<em>1. From the context menu, select Add Files</em></p></td>
<td><p>![](./images/Hgaddfile2.png)
<em>2. Select the objects you wish to add to your local repository, click Add</em></p></td>
</tr>
</tbody>
</table>

This will cause the new items to be added to the local repository, which is indicated with a blue plus sign added to their icons in the Explorer view.

### Committing files / directories

|                                                                                                                                                      |                                                                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| ![](./images/Hgcommitfiles2.png) |

Right-click, and select **Hg Commit...** to bring up the *TortoiseHg* commit dialogue box. Enter a new commit message in the box at the top, select all the files and directories you wish to commit to the local repository and click the Commit button in the top left corner. This will cause all the Added items with the blue plus sign on their icons in the Explorer view, to be committed to the local repository and therefore displayed with a green check mark instead. Close the dialogue box.

### Pushing changes to the RS repository

|                                                                                                                                                                                                              |                                                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](./images/Hgpushchangesets.png) | ![Screenshot of TortoiseHg Repository Explorer - Push Outgoing Changesets \#2](./images/Hgpushchangesets2.png "Screenshot of TortoiseHg Repository Explorer - Push Outgoing Changesets #2") |

Adding and committing files and directories, are performed on the local repository and will not be available to anyone else working on the project. Eventually, however, you will want to push back some of the code changes you have made to the main RS repository and anyone else working on the project. This is done by right-clicking, and selecting **Hg Repository Explorer** to bring up the *TortoiseHg* Repository Explorer dialogue box. From here you can click the up-arrow-beneath-a-line button to Push Outgoing Changesets - including all new additions and modifications that you have committed locally. A dialogue box will ask you to confirm by clicking Push again, and then the *TortoiseHg* client will connect to the RS repository. You will be asked to supply your username and password, to authenticate with the server and then all new changesets will be pushed to the remote repository on the server. Close the dialogue box. You can then [browse](#Browse_the_RS_Mercurial_repositories_online_.28read-only.29 "wikilink") the repository online and view the changesets that you have pushed.

### Adding/removing a release tag

|                                                                                                                                                                                                 |                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](./images/Hgaddremovetag1.png) |

When you have reached a stage in the code where you wish to label it as a release, you can add a tag, perhaps of the form v1.01. Anyone who browses the repository can then download that particular tagged version of the code as a standalone bz2, zip or gz archive with their web browser, direct from the [web view of the repository](#Browse_the_RS_Mercurial_repositories_online_.28read-only.29 "wikilink"). Other *Mercurial* users with access to the project can also download that particular release of the code. To add a tag, right-click and select **Hg Repository Explorer** to bring up the *TortoiseHg* Repository Explorer dialogue box again. Select the changeset you wish to tag from the list, then right-click and select Tag -&gt; Add/Remove Tag. This will bring up the Tag dialogue box which will allow you to add or remove a tag. Remember that such a tag change must also then be pushed back to the main RS repository, if you want others to see it!
