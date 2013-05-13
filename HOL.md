<a name="title" />
# Introduction to Windows Azure Media Services #

---
<a name="Overview" />
## Overview ##
Windows Azure Media Services allows you to build a media distribution solution that can stream audio and video to Windows, iOS, Android, and other devices and platforms.

In this HOL you will learn how you can use Visual Studio 2012 and Windows Azure Media Services to upload, encode,  deliver and stream media content. Additionally, you will learn how to add a media player to your Windows Store applications and how to monetize your application using advertisements in the player.

<a name="Objectives" />
### Objectives ###
- Create a Windows Azure Media Service
- Manage media content: upload, encode and stream media.
- Programatically uploading, encoding and streaming content 
- Using the Microsoft Media Platform Player Framework in a Windows 8 application
- Adding Advertisements support to your Windows 8 video application

<a name="prerequisites" />
### Prerequisites ###

- Windows Azure subscription - [sign up for a free trial](http://aka.ms/WATK-FreeTrial)
- [Visual Studio Express 2012 for Windows 8](http://www.microsoft.com/visualstudio) or higher

<a name="Exercises" />
## Exercises ##

This hands-on lab includes the following exercises:

1. [Uploading a Job from the Portal for HTML5 playback](#Exercise1)
1. [A Console app using the Media Services SDK that uploads, encodes, and streams a video programmatically](#Exercise2)
1. [Microsoft Media Platform Player Framework for the client](#Exercise3)
1. [Monetization](#Exercise4)

<a name="Exercise1" />
## Exercise 1: Uploading a Job from the Portal for HTML5 playback ##

The Windows Azure Management Portal provides a way to quickly create a Windows Azure Media Services account. You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Windows Azure. At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.

<a name="creating-a-media-service-account" />
### Task 1 - Creating a Media Services Account ###

This task explains how to use the Quick Create method to create a new Media Services account and then associate it with a storage account.

1. Log into the [Windows Azure Management Portal](https://manage.windowsazure.com).

1. Click **New** | **App Services** | **Media Services**, and then click **Quick Create**.

	![Creating a new Media Service](Images/creating-a-media-service.png?raw=true)

1. In **NAME**, enter the name of the new account. A Media Services account name is all lower-case numbers or letters with no spaces, and is 3 - 24 characters in length.

1. In **REGION**, select the geographic region that will be used to store the metadata records for your Media Services account. Only the available Media Services regions appear in the dropdown.
 
1. In **STORAGE ACCOUNT**, select a storage account to provide blob storage of the media content from your Media Services account. You can select an existing storage account in the same geographic region as your Media Services account, or you can create a new storage account. A new storage account is created in the same region.
 
1. If you created a new storage account, in **NEW STORAGE ACCOUNT NAME**, enter a name for the storage account. The rules for storage account names are the same as for Media Services accounts.

1. Click **Quick Create** at the bottom of the form.

You can monitor the status of the process in the message area at the bottom of the window.
The **media services** page opens with the new account displayed. When the status changes to Active, it means the account is successfully created.

![The recently created Media Service](Images/recently-created-media-service.png?raw=true)

<a name="managing-content-in-media-services" />
### Task 2 - Managing Content in Media Services ###

The Windows Azure Media Services content view allows you to manage media content for your Media Services account.
Currently you can perform the following content operations directly from the portal:

- View content information like published state, published URL, size, and datetime of last update. 
- Upload new content 
- Encode content 
- Play content video 
- Publish/Unpublish content 
- Delete content

On this task yu will upload, encode and publish media content from the portal.

**Uploading content**

1. In the [Management Portal](http://go.microsoft.com/fwlink/?linkid=256666&clcid=0x409), click **Media Services** and then click on the Media Services account name.

1. Click the **Content** view at the top of the page. Your view should look similar to the following screen shot.

	![Uploading Content](Images/uploading-content.png?raw=true)
 
1. Click the **Upload** button at the bottom of the portal. 

1. In the Upload Content dialog, click **Browse Your Computer** and browse to the desired asset file. Click the file and then click **Open** or press **Enter**.

	>**Note:** You can use the following short video to try uploading content to Media Services: [Azure_Intro.mp4](<https://cloudnick.blob.core.windows.net/drop/Azure_Intro.mp4>)
 
1. In the Upload Content dialog, click the check button to accept the File and Content Name.

	![Upload Content dialog](Images/upload-content-dialog.png?raw=true)

1. The upload will start and you can track progress from the bottom of the portal. 
 
	![Uploading progress](Images/uploading-progress.png?raw=true)

Once the upload has completed, you will see the new asset listed in the Content list. By convention the name will have "**-Source**" appended at the end to help track new content as source content for encoding tasks.

If the file size value does not get updated after the uploading process stops, press the Sync Metadata button. This synchronizes the asset file size with the actual file size in storage and refreshes the value on the Content page. 

**Encoding content**

1. Click on the desired source video that you have just uploaded, and then click **Encode** at the bottom of the page.

1. In the Windows Azure Media Encoder dialog, choose from one of the common or advanced encoding presets. For this task purposes, choose **Playback via HTML5 (IE/Chrome/Safari)**.

	**Common Presets**

	- **Playback on PC/Mac (via Flash/Silverlight)**. This preset produces a Smooth Streaming asset with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 96 kbps using AAC, and 720p video CBR encoded at 6 bitrates ranging from 3400 kbps to 400 kbps using H.264 Main Profile, and two second GOPs. 

 - **Playback via HTML5 (IE/Chrome/Safari)**. This preset produces a single MP4 file with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 128 kbps using AAC, and 720p video CBR encoded at 4500 kbps using H.264 Main Profile. 

	- **Playback on iOS devices and PC/Mac**. This preset produces an asset with the same characteristics as the Smooth Streaming asset (described above), but in a format that can be used to deliver Apple HLS streams to iOS devices. 

	**Advanced Presets** 
	
	The [Task Preset Strings for Windows Azure Media Encoder](http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409) topic explains what each preset in the Advanced Presets list means. 

	![Encoding Media](Images/encoding-media.png?raw=true)

	Currently, the portal does not support all the encoding formats that are supported by the Media Encoder. It also does not support media asset encryption\decryption. You can perform these tasks programmatically, for more information see [Building Applications with the Media Services SDK for .NET] (http://go.microsoft.com/fwlink/?linkid=270866&clcid=0x409) and [Task Preset Strings for Windows Azure Media Encoder]( http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409).

1. In the **Windows Azure Media Encoder** dialog, enter the desired friendly output content name or accept the default. Then click the check button to start the encoding operation and you can track progress from the bottom of the portal.

**Publishing content**

1. Click an asset which is not published, in this case, the video that was just encoded. Then click the publish button to publish to a public URL. Once the content is published to a URL, the URL can be opened by a client player capable of rendering the encoded content.

**Playing content from the portal**
 
1. Click on the published video content and click the **Play** button at the bottom of the portal. Only content that has been published is playable from the portal. Also, the encoding must be supported by your browser.

---

<a name="Exercise2" />
## Exercise 2: A Console app using the Media Services SDK that uploads, encodes, and streams a video programmatically ##

<INTRO>

<a name="programatically-uploading-a-mp4-video" />
### Task 1 - Programmatically Uploading a Mp4 video ###

1. First step.


<a name="programatically-encoding-a-mp4-video" />
### Task 2 - Programmatically Encoding a Mp4 video using Smooth Streaming ###

1. First step.


<a name="programatically-delivering-and-streaming-a-mp4-video" />
### Task 3 - Programmatically Delivering and Streaming a Mp4 video ###

1. First step.

<a name="Exercise3" />
## Exercise 3: Microsoft Media Platform Player Framework for the client  ##

<INTRO>

<a name="installing-MMPPF" />
### Task 1 - Installing Microsoft Media Platform Player Framework ###

1. First step.

<a name="adding-a-video-player-control-to-a-windows8-app" />
### Task 2 - Adding a video player control to a Windows 8 app ###

1. First step.

<a name="Exercise4" />
## Exercise 4: Monetization ##

<INTRO>

<a name="adding-advertisements-using-a-vmap-file-to-a-windows8-video-app" />
### Task 1 - Adding advertisements using a VMAP file to a Windows 8 video app ###

1. First step.  

<a name="Summary"></a>
## Summary ##
By completing this hands-on lab you have learnt how to:

- XXXXXXXXXXXXXXXXXXXX
- XXXXXXXXXXXXXXXXXXXX

---
