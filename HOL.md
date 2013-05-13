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

---

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

---

<a name="Exercise2" />
## Exercise 2: A Console app using the Media Services SDK that uploads, encodes, and streams a video programmatically ##

In this exercise, you will create a new console application that allows you to perform the different tasks on your Azure Media Services subscription.

<a name="programmatically-uploading-a-mp4-video" />
### Task 1 - Programmatically Uploading a Mp4 video ###

1. Open **Microsoft Visual Studio 2012 Express for Web** (or higher) in elevated administrator mode. If the **User Account Control** dialog appears, click **Yes**.

1. In the **File** menu, choose **New** and then **Project/Solution**. In the New Project dialog, select the **Templates | C#** node from the left pane, and then select the **Console Application** template.

1. Enter _MyMediaServicesManager_ as the project **Name**, choose a desired **Location**, and click **Ok**.

1. Open the **Package Manager Console** by clicking **View | Other Windows | Package Manager Console**.

1. In the console, type _Install-Package windowsazure.mediaservices_ to download and install the **Windows Azure Media Services** NuGet package and its dependencies.

1. In the _program.cs_ file add the following using statements.

	````C#
	using Microsoft.WindowsAzure.MediaServices.Client;
	using System.IO;
	````

1. Go to the **Windows Azure Management Portal**, click **Media Services** in the left menu, and then click your **Media Services** name. The quickstart page will be displayed.

1. Under the **WRITE SOME CODE** section, click **UPLOAD A VIDEO PROGRAMMATICALLY**.

	![Programmatically uploading a video](Images/programatically-uploading-a-video.png?raw=true).

1. Copy this code an paste it in the _program.cs_ file, inside the **Main** method.

1. Update the code you just pasted to point to a video that you want to upload, by replacing the _YOUR FILE PATH_ string. It could be the same video used in the previous exercise.

1. Press **F5** to run the solution and wait until the console app closes.

1. Go to the portal, and notice that video is being uploaded.

	![The programmatically uploaded video](Images/the-programmatically-uploaded-video.png?raw=true).

<a name="programmatically-encoding-a-mp4-video" />
### Task 2 - Programmatically Encoding a Mp4 video using Smooth Streaming ###

1. First step.


<a name="programmatically-delivering-and-streaming-a-mp4-video" />
### Task 3 - Programmatically Delivering and Streaming a Mp4 video ###

1. First step.

---

<a name="Exercise3" />
## Exercise 3: Microsoft Media Platform Player Framework for the client  ##

Microsoft Media Platform is a complete set of technologies for digital media encoding, delivery, and playback for virtually any network-connected device. The Player Framework is an open source video player available for Silverlight, HTML5, and Xbox, as well as Windows 8 apps and Windows Phone apps. It allows you to play both progressive download videos and Smooth Streaming videos. In this exercise you will first download and install the Microsoft Media Platform Player Framework and then build a simple Store app that will consume a video previously uploaded to Windows Azure Media Services and play it in a video player control.

<a name="installing-MMPPF" />
### Task 1 - Installing Microsoft Media Platform Player Framework ###

In this task you will download and install the latest version of the Microsoft Media Platform Player Framework.

1. Browse to <http://playerframework.codeplex.com/releases> and download the latest version of the Player Framework.

1. Once the download completes, open **Microsoft.PlayerFramework.vsix**.

1. In the **VSIX Installer** window, read the Microsoft Public License and click **Install**.

	![Microsoft Media Platform Player Framework Installation](Images/mmpf-installation.png?raw=true "Microsoft Media Platform Player Framework Installation")

    _Microsoft Media Platform Player Framework Installation_

1. Once the installation finishes, click **Close**.

	![Microsoft Media Platform Player Framework Installation Complete](Images/mmpf-installation-complete.png?raw=true "Microsoft Media Platform Player Framework Installation Complete")

    _Microsoft Media Platform Player Framework Installation Complete_

<a name="adding-a-video-player-control-to-a-windows8-app" />
### Task 2 - Adding a video player control to a Windows 8 app ###

In this task you will create a new C# Store app from scratch and add video control linked to a video uploaded to Windows Azure Media Services.

1. Open **Visual Studio Express 2012 for Windows 8** and select **New Project...** from the Start Page to start a new solution.

	![Creating a New Project](Images/creating-new-project.png?raw=true "Creating a New Project")

    _Creating a New Project_

1. In the **New Project** dialog, select **Blank App (XAML)** under the **Visual C# | Windows Store** tab. Name it _SampleMediaPlayer_, choose a location and click **OK**.

	![New C# Store App](Images/new-store-blank-app.png?raw=true "New C# Store App")

    _New C# Store App_

	
	![New Store App Solution Explorer](Images/new-store-app-solution-explorer.png?raw=true "New Store App Solution Explorer")

    _New Store App Solution Explorer_

1. Open **MainPage.xaml** to open the markup code for the main page of the app.

1. Open the toolbox at the left corner of the screen and extend the **Common XAML Controls** section. Drag and drop the **MediaPlayer** control into the designer. Notice the markup code generated in the xaml file for this control.

	> **Note:** You may adjust the height and width of the control to values of your choice.

	![Media Player control](Images/media-player-control.png?raw=true "Media Player control")

    _Media Player control_

	![Generated Code for Media Player Control](Images/generated-code-for-media-player-control.png?raw=true "Generated Code for Media Player Control")

    _Generated Code for Media Player Control_

1. In the MediaPlayer element of the **MainPage.xaml** file, add the **x:Name** property with the value _videoPlayer_.

	````XML
	<PlayerFramework:MediaPlayer x:Name="videoPlayer"  HorizontalAlignment="Left" Height="600" Margin="200,96,0,0" VerticalAlignment="Top" Width="1000"/>
	````

1. Open the **MainPage.xaml.cs** file and add the following code in the **OnNavigatedTo** event. Make sure you replace the _YOUR-MEDIA-SERVICE-VIDEO-URL_ placeholder with the URL of the encoded video that you uploaded in Exercise 1.

	<!-- mark:3 -->
	````C#
	protected override void OnNavigatedTo(NavigationEventArgs e)
	{
		this.videoPlayer.Source = new Uri(@"{YOUR-MEDIA-SERVICE-ENCODED-VIDEO-URL}");
	}
	````

1. Press **F5** to start the app. You should see the video automatically playing in the video player that you inserted before.

	![Store app running](Images/store-app-running.png?raw=true "Store app running")

    _Store app running_

---

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
