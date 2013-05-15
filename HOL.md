<a name="title" />
# Introduction to Windows Azure Media Services #

---
<a name="Overview" />
## Overview ##
Windows Azure Media Services allows you to build a media distribution solution that can stream audio and video to Windows, iOS, Android, and other devices and platforms. It offer the flexibility, scalability and reliability of a cloud platform to handle high quality media experiences for a global audience. Media Services includes cloud-based versions of many existing technologies from the Microsoft Media Platform and our media partners, including ingest, encoding, format conversion, content protection and both on-demand and live streaming capabilities. Whether enhancing existing solutions or creating new workflows, you can easily combine and manage Media Services to create custom workflows that fit every need.

![Media Services Overview](Images/media-services-overview.png?raw=true "Media Services Overview")

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

	![Creating a new Media Service](Images/creating-a-media-service.png?raw=true "Creating a new Media Service")

	_Creating a new Media Service_

1. In **NAME**, enter the name of the new account. A Media Services account name is all lower-case numbers or letters with no spaces, and is 3 - 24 characters in length.

1. In **REGION**, select the geographic region that will be used to store the metadata records for your Media Services account. Only the available Media Services regions appear in the dropdown.
 
1. In **STORAGE ACCOUNT**, select a storage account to provide blob storage of the media content from your Media Services account. You can select an existing storage account in the same geographic region as your Media Services account, or you can create a new storage account. A new storage account is created in the same region.
 
1. If you created a new storage account, in **NEW STORAGE ACCOUNT NAME**, enter a name for the storage account. The rules for storage account names are the same as for Media Services accounts.

1. Click **Quick Create** at the bottom of the form.

	You can monitor the status of the process in the message area at the bottom of the window.
The **media services** page opens with the new account displayed. When the status changes to Active, it means the account is successfully created.

	![The recently created Media Service](Images/recently-created-media-service.png?raw=true "The recently created Media Service")

	_The recently created Media Service_

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

	![Uploading Content](Images/uploading-content.png?raw=true "Uploading Content")

	_Uploading Content_
 
1. Click the **Upload** button at the bottom of the portal. 

1. In the Upload Content dialog, click **Browse Your Computer** and browse to the desired asset file. Click the file and then click **Open** or press **Enter**.

	>**Note:** You can use the following short video to try uploading content to Media Services: [Azure_Intro.mp4](<https://cloudnick.blob.core.windows.net/drop/Azure_Intro.mp4>)
 
1. In the Upload Content dialog, click the check button to accept the File and Content Name.

	![Upload Content dialog](Images/upload-content-dialog.png?raw=true "Upload Content dialog")

	_Upload Content dialog_

1. The upload will start and you can track progress from the bottom of the portal. 
 
	![Uploading progress](Images/uploading-progress.png?raw=true "Uploading progress")

	_Uploading progress_

	Once the upload has completed, you will see the new asset listed in the Content list. By convention the name will have **-Source** appended at the end to help track new content as source content for encoding tasks.

	If the file size value does not get updated after the uploading process stops, press the Sync Metadata button. This synchronizes the asset file size with the actual file size in storage and refreshes the value on the Content page. 

**Encoding content**

1. Click on the desired source video that you have just uploaded, and then click **Encode** at the bottom of the page.

1. In the Windows Azure Media Encoder dialog, choose from one of the common or advanced encoding presets. For this task purposes, choose **Playback via HTML5 (IE/Chrome/Safari)**.

	**Common Presets**

	**Playback on PC/Mac (via Flash/Silverlight)**. This preset produces a Smooth Streaming asset with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 96 kbps using AAC, and 720p video CBR encoded at 6 bitrates ranging from 3400 kbps to 400 kbps using H.264 Main Profile, and two second GOPs. 
 	
 	**Playback via HTML5 (IE/Chrome/Safari)**. This preset produces a single MP4 file with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 128 kbps using AAC, and 720p video CBR encoded at 4500 kbps using H.264 Main Profile. 
	
	**Playback on iOS devices and PC/Mac**. This preset produces an asset with the same characteristics as the Smooth Streaming asset (described above), but in a format that can be used to deliver Apple HLS streams to iOS devices. 

	**Advanced Presets** 
	
	The [Task Preset Strings for Windows Azure Media Encoder](http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409) topic explains what each preset in the Advanced Presets list means. 

	![Encoding Media](Images/encoding-media.png?raw=true "Encoding Media")

	_Encoding Media_

	Currently, the portal does not support all the encoding formats that are supported by the Media Encoder. It also does not support media asset encryption\decryption. You can perform these tasks programmatically, for more information see [Building Applications with the Media Services SDK for .NET] (http://go.microsoft.com/fwlink/?linkid=270866&clcid=0x409) and [Task Preset Strings for Windows Azure Media Encoder]( http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409).

1. In the **Windows Azure Media Encoder** dialog, enter the desired friendly output content name or accept the default. Then click the check button to start the encoding operation and you can track progress from the bottom of the portal.

**Publishing content**

1. Click an asset which is not published, in this case, the video that was just encoded. Then click the publish button to publish to a public URL. Once the content is published to a URL, the URL can be opened by a client player capable of rendering the encoded content.

**Playing content from the portal**
 
1. Click on the published video content and click the **Play** button at the bottom of the portal. Only content that has been published is playable from the portal. Also, the encoding must be supported by your browser.

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

1. Paste the following code in the _program.cs_ file, inside the **Main** method. This code prompts the user about the different steps that the final app will perform, and will aid you in completing the exercise.

	````C#
	Console.WriteLine("Uploading Video");
            
	Console.WriteLine("Uploading Completed");
	Console.WriteLine("Encoding Video");

	Console.WriteLine("Encoding Completed");
	Console.WriteLine("Publishing Video");

	Console.WriteLine("Publishing Completed");
	Console.ReadLine();
	````

1. Go to the **Windows Azure Management Portal**, click **Media Services** in the left menu, and then click your **Media Services** name. The quickstart page will be displayed.

1. Under the **WRITE SOME CODE** section, click **UPLOAD A VIDEO PROGRAMMATICALLY**.

	![Programmatically uploading a video](Images/programatically-uploading-a-video.png?raw=true "Programmatically uploading a video")

	_Programmatically uploading a video_

1. Copy this code an paste it in inside the **Main** method, between the lines that notify about the uploading process. The resulting code will be similar to the following one.

	<!-- mark:5-9 -->
	````C#
    static void Main(string[] args)
    {
		Console.WriteLine("Uploading Video");

		var uploadFilePath = @"[YOUR FILE PATH]";
		var context = new CloudMediaContext("[YOUR-MEDIA-SERVICE-ACCOUNT-NAME]", "[YOUR-MEDIA-SERVICE-ACCOUNT-KEY]");
		var uploadAsset = context.Assets.Create(Path.GetFileNameWithoutExtension(uploadFilePath), AssetCreationOptions.None);
		var assetFile = uploadAsset.AssetFiles.Create(Path.GetFileName(uploadFilePath));
		assetFile.Upload(uploadFilePath);

		Console.WriteLine("Uploading Completed");
		Console.WriteLine("Encoding Video");

		Console.WriteLine("Encoding Completed");
		Console.WriteLine("Publishing Video");

		Console.WriteLine("Publishing Completed");
		Console.ReadLine();
		}
	}
	````
	The preceding code uses the **CloudMediaContext** class to create an _asset file_ using the provided file path. Once the asset file is created, the **Upload** method is called to start the uploading operation.

1. Update the code you just pasted to point to the video that you want to upload, by replacing the _YOUR FILE PATH_ string. It could be the same video used in the previous exercise. If you are going to do that it is recommended that you rename the video to differentiate it from the one uploaded in the first exercise of this lab.

<a name="programmatically-encoding-a-mp4-video" />
### Task 2 - Programmatically Encoding a Mp4 video using Smooth Streaming ###

1. Add the following using statement at the top of the _program.cs_ file.

	````C#
	using System.Threading;
	````

1. Add the following code inside the WriteLine blocks that notify about the initiation and termination of the encoding operation.

	<!-- mark:3-26 -->
	````C#
    Console.WriteLine("Encoding Video");

    var encodeAssetId = uploadAsset.Id; // "YOUR ASSET ID";
    var encodingPreset = "H264 Smooth Streaming 720p";
    var assetToEncode = context.Assets.Where(a => a.Id == encodeAssetId).FirstOrDefault();
    if (assetToEncode == null)
    {
        throw new ArgumentException("Could not find assetId: " + encodeAssetId);
    }

    IJob job = context.Jobs.Create("Encoding " + assetToEncode.Name + " to " + encodingPreset);

    IMediaProcessor latestWameMediaProcessor = (from p in context.MediaProcessors
                                                where p.Name == "Windows Azure Media Encoder"
                                                select p).ToList()
                                                .OrderBy(wame => new Version(wame.Version)).LastOrDefault();
    ITask encodeTask = job.Tasks.AddNew("Encoding", latestWameMediaProcessor, encodingPreset, TaskOptions.None);
    encodeTask.InputAssets.Add(assetToEncode);
    encodeTask.OutputAssets.AddNew(assetToEncode.Name + " as " + encodingPreset, AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>((sender, jsc) =>
        Console.WriteLine(string.Format("{0}\n State: {1}\n Time: {2}\n\n", ((IJob)sender).Name, jsc.CurrentState, DateTime.UtcNow.ToString(@"yyyy_M_d_hhmmss"))));
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

    var preparedAsset = job.OutputMediaAssets.FirstOrDefault();


    Console.WriteLine("Encoding Completed"); 
	````

	The preceding code uses the **CloudMediaContext** instance to create an encoding job with an enconding task to the specified preset. In this case a smooth streaming encoding (H264 Smooth Streaming 720p) is used.
	Then the job is submited. Notice that an event handler is attached to the **StateChanged** event of the job, what means that every time the stats of the job changes that will be prompted to the console.

<a name="programmatically-delivering-and-streaming-a-mp4-video" />
### Task 3 - Programmatically Delivering and Streaming a Mp4 video ###

1. Add the following code inside the WriteLine blocks that notify about the initiation and termination of the publishing operation.

	<!-- mark:3-32 -->
	````C#
    Console.WriteLine("Publishing Video");

    var streamingAssetId = preparedAsset.Id; // "YOUR ASSET ID";
    var daysForWhichStreamingUrlIsActive = 365;
    var streamingAsset = context.Assets.Where(a => a.Id == streamingAssetId).FirstOrDefault();
    var accessPolicy = context.AccessPolicies.Create(streamingAsset.Name, TimeSpan.FromDays(daysForWhichStreamingUrlIsActive),
                                                AccessPermissions.Read | AccessPermissions.List);
    string streamingUrl = string.Empty;
    var assetFiles = streamingAsset.AssetFiles.ToList();
    var streamingAssetFile = assetFiles.Where(f => f.Name.ToLower().EndsWith("m3u8-aapl.ism")).FirstOrDefault();
    if (streamingAssetFile != null)
    {
        var locator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin, streamingAsset, accessPolicy);
        Uri hlsUri = new Uri(locator.Path + streamingAssetFile.Name + "/manifest(format=m3u8-aapl)");
        streamingUrl = hlsUri.ToString();
    }
    streamingAssetFile = assetFiles.Where(f => f.Name.ToLower().EndsWith(".ism")).FirstOrDefault();
    if (string.IsNullOrEmpty(streamingUrl) && streamingAssetFile != null)
    {
        var locator = context.Locators.CreateLocator(LocatorType.OnDemandOrigin, streamingAsset, accessPolicy);
        Uri smoothUri = new Uri(locator.Path + streamingAssetFile.Name + "/manifest");
        streamingUrl = smoothUri.ToString();
    }
    streamingAssetFile = assetFiles.Where(f => f.Name.ToLower().EndsWith(".mp4")).FirstOrDefault();
    if (string.IsNullOrEmpty(streamingUrl) && streamingAssetFile != null)
    {
        var locator = context.Locators.CreateLocator(LocatorType.Sas, streamingAsset, accessPolicy);
        var mp4Uri = new UriBuilder(locator.Path);
        mp4Uri.Path += "/" + streamingAssetFile.Name;
        streamingUrl = mp4Uri.ToString();
    }
    Console.WriteLine("Streaming Url: " + streamingUrl);

    Console.WriteLine("Publishing Completed");
    Console.ReadLine();
	````

	The preceding code locates the asset and creates a locator URI that will be used to access the asset publicly.

1. Press **F5** to run the console application, and wait until the uploading, encoding and publishing finishes.

	![The console application running](Images/the-console-app-running.png?raw=true "The console application running")

	_The console application running_

1. Press any key to close the console application when it shows that the publishing is completed.

1. Go to the portal, and to the **Content** section of your Media Services subscription.

	![The portal showing the assets processed by the console app](Images/portal-showing-the-assets-processed-by-the-console-app.png?raw=true "The portal showing the assets processed by the console app")

	_The portal showing the assets processed by the console app_

1. Select the asset that was encoded in smooth streaming and press the play button.

	![The smooth streaming video being played](Images/smooth-streaming-video-being-played.png?raw=true "The smooth streaming video being played")

	_The smooth streaming video being played_

	>**Note:** You may notice that this video plays faster that the one uploaded in exercise one. This is due to smooth streaming, as it encodes the video in several qualities and will send you the better video according to your bandwith.

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

In this task you will create a new C# Store app from scratch and add video control linked to a smooth streaming video uploaded to Windows Azure Media Services.

1. Download and install the [Visual Studio Extension SDK for the Smooth Streaming Client] (http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6).

1. Open **Visual Studio Express 2012 for Windows 8** and select **New Project...** from the Start Page to start a new solution.

	![Creating a New Project](Images/creating-new-project.png?raw=true "Creating a New Project")

    _Creating a New Project_

1. In the **New Project** dialog, select **Blank App (XAML)** under the **Visual C# | Windows Store** tab. Name it _SampleMediaPlayer_, choose a location and click **OK**.

	![New C# Store App](Images/new-store-blank-app.png?raw=true "New C# Store App")

    _New C# Store App_

	
	![New Store App Solution Explorer](Images/new-store-app-solution-explorer.png?raw=true "New Store App Solution Explorer")

    _New Store App Solution Explorer_

1. Add **Microsoft Player Framework Adaptive Streaming Plugin**, **Microsoft Smooth Streaming Client SDK for Windows 8**, and **Microsoft Visual C++ Runtime Package** to your project References. To do this, right-click the project, click **Add References**. In the **Reference Manager**, select the aforementioned references that are located under **Windows | Extensions** and click **Ok**.

	![Smooth Streaming references](Images/smooth-streaming-references.png?raw=true "Smooth Streaming references")

    _Smooth Streaming references_

1. Open **MainPage.xaml** to open the markup code for the main page of the app.

1. At the top of the file, add the following XML namespace reference.

	````XML
	xmlns:adaptive="using:Microsoft.PlayerFramework.Adaptive"
	````

1. Open the toolbox at the left corner of the screen and extend the **Common XAML Controls** section. Drag and drop the **MediaPlayer** control into the designer. Notice the markup code generated in the xaml file for this control.

	> **Note:** You may adjust the height and width of the control to values of your choice.

	![Media Player control](Images/media-player-control.png?raw=true "Media Player control")

    _Media Player control_

	![Generated Code for Media Player Control](Images/generated-code-for-media-player-control.png?raw=true "Generated Code for Media Player Control")

    _Generated Code for Media Player Control_

1. In the MediaPlayer element of the **MainPage.xaml** file, add the **x:Name** property with the value _videoPlayer_, and add the **Source** property, pointing to the URL of the video enconded in smooth streaming at the end of exercise 2.

	````XML
	<PlayerFramework:MediaPlayer x:Name="videoPlayer"  HorizontalAlignment="Left"
	Height="600" Margin="200,96,0,0" VerticalAlignment="Top" Width="1000"
 Source ="[YOUR-MEDIA-SERVICE-VIDEO-URL]"/>
	````

1. Modify the MediaPlayer control Xaml to add the Adaptive plugin to the plugins collection on the player framework, as shown in the following code.

	````XML
	<PlayerFramework:MediaPlayer x:Name="videoPlayer"
                                HorizontalAlignment="Left"
                                Height="600"
                                Margin="200,96,0,0"
                                VerticalAlignment="Top"
                                Width="1000"
								Source ="[YOUR-MEDIA-SERVICE-VIDEO-URL]">
		<PlayerFramework:MediaPlayer.Plugins>
			<adaptive:AdaptivePlugin />
		</PlayerFramework:MediaPlayer.Plugins>
	</PlayerFramework:MediaPlayer>
	````

1. Before compiling the app, target your app to x86, x64, or ARM. Because the IIS Smooth Streaming Client is written in unmanaged code, **AnyCPU** will not work and instead you must target and build your app for each platform you wish to support. To do this, go to the **Debug** combobox in the toolbar, expand its options and click **Configuration Manager**. In the row of your current project, expand the options of the **Platform** combobox and select **x64**. Alternatively, you can choose **x86** or **ARM** if your processor supports them.

	![Targeting the app to build to x64](Images/targeting-the-app-to-build-to-x64.png?raw=true "Targeting the app to build to x64")

	_Targeting the app to build to x64_

1. Press **F5** to start the app. You should see the video automatically playing in the video player that you inserted before.

	![Store app playing the Smooth Streaming video](Images/store-app-running.png?raw=true "Store app playing the Smooth Streaming video")

    _Store app playing the Smooth Streaming video_

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
