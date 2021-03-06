<a name="title" />
# Introduction to Microsoft Azure Media Services #

---

<a name="Overview" />
## Overview ##
Microsoft Azure Media Services allows you to build a media distribution solution that can stream audio and video to Windows, iOS, Android, and other devices and platforms. It offers the flexibility, scalability and reliability of a cloud platform to handle high quality media experiences for a global audience. Media Services includes cloud-based versions of many existing technologies from the Microsoft Media Platform and media partners including ingest, encoding, format conversion, content protection and both on-demand and live streaming capabilities.

![Media Services Overview](Images/media-services-overview.png?raw=true "Media Services Overview")

In this hands-on lab you will learn how you can use Visual Studio 2013 and Microsoft Azure Media Services to upload, encode, deliver and stream media content, as well as perform these operations from the portal. Additionally, you will learn how to add a media player to your Windows Store applications and how to monetize your application using advertisements in the media player.

<a name="Objectives" />
### Objectives ###

In this hands-on lab, you will learn how to:

- Create a Microsoft Azure Media Service
- Manage media content: upload, encode and stream media
- Programmatically upload, encode and stream content 
- Use the Microsoft Media Platform Player Framework in a Windows 8.1 application
- Add Advertisements support to your Windows 8.1 video application

<a name="prerequisites" />
### Prerequisites ###

The following is required to complete this hands-on lab:

- [Microsoft Visual Studio Express 2013 for Windows Desktop](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-desktop) or higher
- [Microsoft Visual Studio Express 2013 for Windows](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) or higher
- A Microsoft Azure subscription
	- Sign up for a [Free Trial](http://aka.ms/watk-freetrial).
	- If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](http://aka.ms/watk-msdn) now to start development and test on Microsoft Azure.
	- [BizSpark](http://aka.ms/watk-bizspark) members automatically receive the Microsoft Azure benefit through their Visual Studio Ultimate with MSDN subscriptions.
	- Members of the [Microsoft Partner Network](http://aka.ms/watk-mpn) Cloud Essentials program receive monthly credits of Microsoft Azure at no charge.

---

<a name="Exercises" />
## Exercises ##

This hands-on lab includes the following exercises:

1. [Uploading a Job from the Portal for HTML5 playback](#Exercise1)
1. [Building a Console app using the Media Services SDK that uploads, encodes, and streams a video programmatically](#Exercise2)
1. [Microsoft Media Platform Player Framework for the Client](#Exercise3)
1. [Monetization](#Exercise4)

<a name="Exercise1" />
### Exercise 1: Uploading a Job from the Portal for HTML5 playback ###

The Microsoft Azure Management Portal provides a way to quickly create a Microsoft Azure Media Services account. You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Microsoft Azure. At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.

<a name="creating-a-media-service-account" />
#### Task 1 - Creating a Media Services Account ####

This task explains how to use the Quick Create method to create a new Media Services account and then associate it with a storage account.

1. Log in to the [Microsoft Azure Management Portal](https://manage.windowsazure.com).

1. Click **New** | **App Services** | **Media Service**, and then click **Quick Create**.

	![Creating a new Media Service](Images/creating-a-new-media-service.png?raw=true "Creating a new Media Service")

	_Creating a new Media Service_

1. In **Name**, enter the name of the new account. A Media Services account name should be all lowercase letters and/or numbers without spaces and 3 to 24 characters long.

1. In **Region**, select the geographic region that will be used to store the metadata records for your Media Services account. Only the available Media Services regions appear in the dropdown menu.
 
1. In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account. You can select an existing storage account, or you can create a new storage account. The storage account should be located in the same geographic region as your Media Services account.
 
1. If you created a new storage account, in **New Storage Account Name**, enter a name for the storage account. The rules for storage account names are the same as for Media Services accounts.

1. Click **Create Media Service** at the bottom of the form.

	You can monitor the status of the process in the message area at the bottom of the window.
The **media services** page opens with the new account displayed. When the status changes to **Active** the account has been successfully created.

	![The recently created Media Service](Images/recently-created-media-service.png?raw=true "The recently created Media Service")

	_The recently created Media Service_

<a name="uploading-content-to-media-services" />
#### Task 2 - Uploading content to Media Services ####

In this task you will upload content to the media service already created using the Microsoft Azure Management Portal.

1. In the [Microsoft Azure Management Portal](http://go.microsoft.com/fwlink/?linkid=256666&clcid=0x409), click **Media Services** and then click the name of the media service created in the previous task.

1. Click the **Content** view at the top of the page and then click **Upload** in the bottom toolbar.

	![Uploading Content](Images/uploading-content.png?raw=true "Uploading Content")

	_Uploading Content_

1. In the **Upload Content** dialog box, click **From Local** and browse to the desired asset file. Click the file and then click **Open** or press **Enter**.

	![Upload Content dialog box](Images/upload-content-dialog.png?raw=true "Upload Content dialog box")

	_Upload Content dialog box_

	>**Note:** You can use the following short video to try uploading content to Media Services: [Azure_Intro.mp4](http://dpeshare.blob.core.windows.net/mediaserviceslabassets/Azure_Intro.mp4)
 
1. Now click the check button to submit the file and content name.

1. The upload will start and you can track its progress in the bottom toolbar of the portal. 
 
	![Uploading progress](Images/uploading-progress.png?raw=true "Uploading progress")

	_Uploading progress_

	Once the upload is complete, you will see the new asset listed in the _Content_ list. By convention, the name will have **-Source** appended at the end to help track new content as source content for encoding tasks.

	If the Size value of the file is not updated after the uploading process finishes, press the **Sync Metadata** button. This synchronizes the asset file size with the actual file size in storage and refreshes the value on the _Content_ page. 

<a name="encoding-content-in-media-services" />
#### Task 3 - Encoding content in Media Services ####

In this task you will encode a video previously uploaded in the Microsoft Azure Management Portal.

1. Click on the desired source video, in this case the one that you have just uploaded, and then click **Encode** in the bottom toolbar.

	![Encode Button](Images/encode-button.png?raw=true "Encode Button")

	_Encode Button_

1. In the **Microsoft Azure Media Encoder** dialog box, choose from one of the common or advanced encoding presets. For the purpose of this task, choose **Playback via HTML5 (IE/Chrome/Safari)**. More information about the presets:

	**Common Presets**

	**Playback on PC/Mac (via Flash/Silverlight)**. This preset produces a Smooth Streaming asset with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 96 kbps using AAC, and 720p video CBR encoded at 6 bitrates ranging from 3400 kbps to 400 kbps using H.264 Main Profile, and two second GOPs. 
 	
 	**Playback via HTML5 (IE/Chrome/Safari)**. This preset produces a single MP4 file with the following characteristics: 44.1 kHz 16 bits/sample stereo audio CBR encoded at 128 kbps using AAC, and 720p video CBR encoded at 4500 kbps using H.264 Main Profile. 
	
	**Playback on iOS devices and PC/Mac**. This preset produces an asset with the same characteristics as the Smooth Streaming asset (described above), but in a format that can be used to deliver Apple HLS streams to iOS devices. 

	**Advanced Presets** 
	
	The [Media Services Encoder System Presets](http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409) topic explains what each preset in the Advanced Presets list means. 

	![Encoding Media](Images/encoding-media.png?raw=true "Encoding Media")

	_Encoding Media_

	>**Note:** Currently, the portal does not support all the encoding formats that are supported by the Media Encoder. It also does not support media asset encryption/decryption. You can perform these tasks programmatically; for more information see [Building Applications with the Media Services SDK for .NET](http://go.microsoft.com/fwlink/?linkid=270866&clcid=0x409) and [Media Services Encoder System Presets]( http://go.microsoft.com/fwlink/?linkid=270865&clcid=0x409).

1. In the **Microsoft Azure Media Encoder** dialog box, enter the desired friendly output content name or accept the default. Then click the check button to start the encoding operation.

	![Encoding media in Microsoft Azure](Images/encoding-media-in-windows-azure.png?raw=true "Encoding media in Microsoft Azure")

	_Encoding media in Microsoft Azure_

<a name="publishing-and-playing-content" />
#### Task 4 - Publishing and Playing content in Media Services ####

In this task, you will publish the previously encoded video and play it directly in the Microsoft Azure Management Portal.

1. Click an asset that is not published - in this case, the video that was just encoded. Then click the **Publish** button in the bottom toolbar to publish the encoded video to a public URL. When asked to confirm the operation, click **Yes**. Once the content is published, the URL can be used by a client player capable of rendering the encoded content.

	![Publishing media in Microsoft Azure](Images/publish-button.png?raw=true "Publishing media in Microsoft Azure")

	_Publishing media in Microsoft Azure_

	>**Note**: It may take some minutes for the video to be available for publishing.

1. Once the publishing process finishes, select the video and click the **Play** button in the bottom toolbar. Only content that has been published is playable from the portal. Also, the encoding must be supported by your browser.

	![Playing media in Microsoft Azure](Images/playing-media.png?raw=true "Playing media in Microsoft Azure")

	_Playing media in Microsoft Azure_

<a name="Exercise2" />
### Exercise 2: Building a Console app using the Media Services SDK that uploads, encodes, and streams a video programmatically ###

In this exercise, you will create a new console application that allows you to perform the different tasks (uploading, encoding, and publishing) on your Azure Media Services subscription. This application uses the Media Services SDK to accomplish these operations.

<a name="programmatically-uploading-a-mp4-video" />
#### Task 1 - Programmatically Uploading an Mp4 video ####

1. Open **Microsoft Visual Studio 2013 Express for Desktop** (or higher) in elevated administrator mode. If the **User Account Control** dialog box appears, click **Yes**.

1. In the **File** menu, choose **New project...**, select the **Templates | Visual C# | Windows** node from the left pane, and then select the **Console Application** template.

1. Enter _MyMediaServicesManager_ as the project **Name**, choose a desired **Location**, and click **Ok**.

1. Open the **Package Manager Console** by clicking **View | Other Windows | Package Manager Console**.

1. In the console, type the following command to download and install the **Microsoft Azure Media Services** NuGet package and its dependencies.

	````Nuget
	Install-Package windowsazure.mediaservices -Version 3.0.0.0
	````

	![Package Manager Console](Images/package-manager-console.png?raw=true "Package Manager Console")

1. In the _Program.cs_ file add the following using statements.

	````C#
	using Microsoft.WindowsAzure.MediaServices.Client;
	using System.IO;
	````

1. Paste the following code in the _Program.cs_ file, inside the **Main** method. This code describes the different steps that the final app will perform, and will aid you in completing the exercise.

	(Code Snippet - _Intro to Media Services - Ex2 - Console Logs_)

	````C#
	Console.WriteLine("Uploading Video");
            
	Console.WriteLine("Uploading Completed");
	Console.WriteLine("Encoding Video");

	Console.WriteLine("Encoding Completed");
	Console.WriteLine("Publishing Video");

	Console.WriteLine("Publishing Completed");
	Console.ReadLine();
	````

1. Go to the **Microsoft Azure Management Portal**, click **Media Services** in the left menu, and then click your **Media Services** name. The quickstart page will be displayed.

1. Make sure that **C#** is selected in the **Choose a language** section. Under the **WRITE SOME CODE** section, click **UPLOAD A VIDEO PROGRAMMATICALLY**.

	![Programmatically uploading a video](Images/programatically-uploading-a-video.png?raw=true "Programmatically uploading a video")

	_Programmatically uploading a video_

1. Copy the code snippet shown in the portal and paste it in inside the **Main** method, between the lines that notify about the uploading process. The resulting code will be similar to the following.

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

1. Update the code you just pasted to point to the video that you want to upload, by replacing the _YOUR FILE PATH_ string. If you use the same video from the previous exercise, it is recommended that you rename the video to differentiate it from the one uploaded in the first exercise.

<a name="programmatically-encoding-an-mp4-video" />
#### Task 2 - Programmatically encoding an MP4 video using Smooth Streaming ####

1. Add the following using statement at the top of the _Program.cs_ file.

	````C#
	using System.Threading;
	````

1. Add the following code between the WriteLine blocks which notifies users of the initiation and termination of the encoding operation.

	(Code Snippet - _Intro to Media Services - Ex2 - Encode Video in Smooth Streaming_)

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
                                                where p.Name == "Microsoft Azure Media Encoder"
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

	The preceding code uses the **CloudMediaContext** instance to create an encoding job with an encoding task to the specified preset. In this case a smooth streaming encoding (H264 Smooth Streaming 720p) is used. Then the job is submitted. Notice that an event handler is attached to the **StateChanged** event of the job, which means that every time the state of the job changes, it will be prompted to the console.

<a name="programmatically-delivering-and-streaming-an-mp4-video" />
#### Task 3 - Programmatically Delivering and Streaming an MP4 video ####

1. Add the following code between the WriteLine blocks which will notify the user of the initiation and termination of the publishing operation.

	(Code Snippet - _Intro to Media Services - Ex2 - Streaming MP4 Video_)

	<!-- mark:3-34 -->
	````C#
    Console.WriteLine("Publishing Video");

    var streamingAssetId = preparedAsset.Id; // "YOUR ASSET ID";
    var daysForWhichStreamingUrlIsActive = 365;
    var streamingAsset = context.Assets.Where(a => a.Id == streamingAssetId).FirstOrDefault();
    var accessPolicy = context.AccessPolicies.Create(streamingAsset.Name, TimeSpan.FromDays(daysForWhichStreamingUrlIsActive), AccessPermissions.Read | AccessPermissions.List);
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

1. Press **F5** to run the console application and wait until the uploading, encoding and publishing finishes.

	![The console application running](Images/the-console-app-running.png?raw=true "The console application running")

	_The console application running_

1. Press any key to close the console application when it shows that the publishing is completed.

1. Go to the Microsoft Azure Management Portal and then to the **Content** section of your Media Services subscription.

	![The portal showing the assets processed by the console app](Images/portal-showing-the-assets-processed-by-the-console-app.png?raw=true "The portal showing the assets processed by the console app")

	_The portal showing the assets processed by the console app_

1. Select the asset that was encoded in smooth streaming and press the play button.

	![The smooth streaming video being played](Images/smooth-streaming-video-being-played.png?raw=true "The smooth streaming video being played")

	_The smooth streaming video being played_

	>**Note:** You may notice that this video plays faster than the one uploaded in _Exercise 1_. This is due to smooth streaming as it encodes the video in several qualities and sends you the best video depending on your bandwidth.

<a name="Exercise3" />
### Exercise 3: Microsoft Media Platform Player Framework for the Client  ###

Microsoft Media Platform is a complete set of technologies for digital media encoding, delivery and playback, for virtually any network-connected device. The Player Framework is an open source video player available for Silverlight, HTML5 and Xbox, as well as Windows 8.1 and Windows Phone apps. It allows you to play both progressive download videos and Smooth Streaming videos.

In this exercise you will first download and install the Microsoft Media Platform Player Framework and then build a simple Store app. Within the app you will consume a video previously uploaded to Microsoft Azure Media Services and play it in a video player control.

<a name="installing-MMPPF" />
#### Task 1 - Installing Microsoft Media Platform Player Framework ####

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
#### Task 2 - Adding a video player control to a Windows 8.1 app ####

In this task you will create a new store app from scratch and add video control linked to a smooth streaming video uploaded to Microsoft Azure Media Services.

1. Download and install the [Microsoft Smooth Streaming Client SDK for Windows 8.1] (http://visualstudiogallery.msdn.microsoft.com/0170c67c-c183-4fee-8dd4-c2b44d710d40).

1. Open **Visual Studio Express 2013 for Windows** and select **New Project...** from the Start Page to start a new solution.

	![Creating a New Project](Images/creating-new-project.png?raw=true "Creating a New Project")

    _Creating a New Project_

1. In the **New Project** dialog box, expand the language tab of your preference (Visual C# or JavaScript), select **Windows Store** and choose the **Blank App** template. Name it _SampleMediaPlayer_, choose a location and click **OK**.

	![New C# Store App](Images/new-cs-store-blank-app.png?raw=true "New C# Store App")

    _New C# Store App_

	![New JavaScript Store App](Images/new-js-store-blank-app.png?raw=true "New JavaScript Store App")

    _New JavaScript Store App_

1. Right-click the project and click **Add | Reference...**. In the **Reference Manager**, select the following references that are located under **Windows | Extensions** and click **OK**.

	- Microsoft Player Framework
	- Microsoft Player Framework Adaptive Streaming Plugin
	- Microsoft Smooth Streaming Client SDK for Windows 8.1
	- Microsoft Visual C++ 2013 Runtime Package for Windows

	![Smooth Streaming C# References](Images/smooth-streaming-cs-references.png?raw=true "Smooth Streaming C# References")

    _Smooth Streaming C# References_

	![Smooth Streaming JavaScript References](Images/smooth-streaming-js-references.png?raw=true "Smooth Streaming JavaScript References")

    _Smooth Streaming JavaScript References_

1. Open **MainPage.xaml** (for the C# project) or **default.html** (for the JavaScript project) to open the markup code for the main page of the app.

1. Add the following namespace references at the top of the **MainPage.xaml** file (for the C# project) or at the end of the head section in the **default.html** file (for the JavaScript project).

	C#

	(Code Snippet - _Intro to Media Services - Ex3 - XAML using statements_)

	<!-- mark:8-9 -->
	````XAML
	<Page
		 x:Class="SampleMediaPlayer.MainPage"
		 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
		 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
		 xmlns:local="using:SampleMediaPlayer"
		 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
		 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
		 xmlns:PlayerFramework="using:Microsoft.PlayerFramework"
		 xmlns:adaptive="using:Microsoft.PlayerFramework.Adaptive"
		 mc:Ignorable="d">
	````

	JavaScript

	(Code Snippet - _Intro to Media Services - Ex3 - PlayerFramework references_)

	<!-- mark:14-19 -->
	````HTML
	<head>
		 <meta charset="utf-8" />
		 <title>SampleMediaPlayer</title>

		 <!-- WinJS references -->
		 <link href="//Microsoft.WinJS.2.0/css/ui-dark.css" rel="stylesheet" />
		 <script src="//Microsoft.WinJS.2.0/js/base.js"></script>
		 <script src="//Microsoft.WinJS.2.0/js/ui.js"></script>

		 <!-- SampleMediaPlayer references -->
		 <link href="/css/default.css" rel="stylesheet" />
		 <script src="/js/default.js"></script>

		 <!-- PlayerFramework references -->
		 <link href="/Microsoft.PlayerFramework.Js/css/PlayerFramework-dark.css" rel="stylesheet">
		 <script src="/Microsoft.PlayerFramework.Js/js/PlayerFramework.js"></script>

		 <!-- PlayerFramework.Adaptive references -->
		 <script src="/Microsoft.PlayerFramework.Js.Adaptive/js/PlayerFramework.Adaptive.js"></script>
	</head>
	````

1. Now you will add a video player control in the **MainPage.xaml** (for the C# project) or in the **default.html** (for the JavaScript project). 

	For C#, open the toolbox in the upper-left corner of the screen and extend the **Common XAML Controls** section. Drag and drop the **MediaPlayer** control into the designer. Notice the markup code generated in the xaml file for this control.

	![Media Player control](Images/media-player-control-cs.png?raw=true "Media Player control")

    _Media Player Control C#_

	Update the styling of the **MediaPlayer** element by adding the following properties to the XAML element

	(Code Snippet - _Intro to Media Services - Ex3 - Media player properties_)

	<!-- mark:2-4 -->
	````XAML
	<PlayerFramework:MediaPlayer 
			  HorizontalAlignment="Left"
			  Height="600" Margin="200,96,0,0"
			  VerticalAlignment="Top" Width="1000" 
	/>
	````

	> **Note:** You may adjust the height and width of the control to the values of your choice.

	For JavaScript, replace the body section with the following highlighted code.
	
	(Code Snippet - _Intro to Media Services - Ex3 - Media Player win-control_)

	<!-- mark:1-9 -->
	````HTML
	<body style="text-align:center">
		<div data-win-control="PlayerFramework.MediaPlayer" 
			data-win-options="{                                 
							  width: 1000,
							  height: 600,
							  autoplay: true,
					  }">
		</div>
	</body>
	````

1. In the media player control, add the **Source** property (for the C# version) or the **src** property (for the JavaScript version) as shown in the following code. Replace the _[YOUR-MEDIA-SERVICE-VIDEO-URL]_ placeholder with the URL of the video encoded in smooth streaming at the end of Exercise 2.

	C#

	<!-- mark:5 -->
	````XAML
	<PlayerFramework:MediaPlayer
		HorizontalAlignment="Left"
		Height="600" Margin="200,96,0,0"
		VerticalAlignment="Top" Width="1000"
		Source ="[YOUR-MEDIA-SERVICE-VIDEO-URL]"
	/>
	````

	JavaScript

	<!-- mark:6 -->
	````HTML
	<div data-win-control="PlayerFramework.MediaPlayer" 
		data-win-options="{                                 
						  width: 1000,
						  height: 600,
						  autoplay: true,
						  src: '[YOUR-MEDIA-SERVICE-VIDEO-URL]',
				  }">
	</div>
	````

1. In the **MainPage.xaml** file of the C# version, modify the MediaPlayer control Xaml to add the Adaptive plugin to the plugins collection on the player framework as shown in the following code.

	(Code Snippet - _Intro to Media Services - Ex3 - Media Player adaptive plugin_)

	<!--mark:7-11-->
	````XAML
	<PlayerFramework:MediaPlayer HorizontalAlignment="Left"
                                Height="600"
                                Margin="200,96,0,0"
                                VerticalAlignment="Top"
                                Width="1000"
								Source ="[YOUR-MEDIA-SERVICE-VIDEO-URL]"
	>
		<PlayerFramework:MediaPlayer.Plugins>
			<adaptive:AdaptivePlugin />
		</PlayerFramework:MediaPlayer.Plugins>
	</PlayerFramework:MediaPlayer>
	````

1. Before compiling the app, target your app to x86, x64, or ARM. Because the IIS Smooth Streaming Client is written in unmanaged code, **Any CPU** will not work and instead you must target and build your app for each platform you wish to support. To do this, go to the **Debug** combobox in the toolbar, expand its options and click **Configuration Manager...**. In the row of your current project, expand the options of the **Platform** combobox and select **x64**. Alternatively, you can choose **x86** or **ARM** if your processor supports them.

	![Targeting the app to build to x64](Images/targeting-app-build-x64-1.png?raw=true "Targeting the app to build to x64")

	![Targeting the app to build to x64](Images/targeting-app-build-x64-2.png?raw=true "Targeting the app to build to x64")

	_Targeting the app to build to x64_

1. Press **F5** to run the app. You should see the video automatically playing in the video player that you inserted before.

	![Store app playing the Smooth Streaming video](Images/store-app-running.png?raw=true "Store app playing the Smooth Streaming video")

    _Store app playing the Smooth Streaming video_

<a name="Exercise4" />
### Exercise 4: Monetization ###

In this exercise you will add support for in-video advertisements to monetize your application by using a VMAP file that defines which ads will be played and when.

Scheduling is the first step to playing ads in the player framework. This allows your app to tell the player framework when to play each ad. Ad scheduling is separate from the ad handling (playing the ad) and is independent of the type of ad you want to play.

One of the scheduling options is the **VMAP** (Digital Video Multiple Ad Playlist). VMAP is an xml schema that defines when ads should play for a given piece of content. The player framework includes a VMAP scheduler plugin that will download, parse and consume to control the timing of ads for you.

<a name="adding-advertisements-using-a-vmap-file-to-a-windows8-video-app" />
#### Task 1 - Adding advertisements using a VMAP file to a Windows 8.1 video app ####

In this task, you will add advertising support to the media player control of the app using the vmap scheduler plugin.

1. If not already open, start **Visual Studio Express 2013 for Windows** and select **Open Project...** from the Start Page. In the **Open Project** dialog box, browse to **Ex4-Advertising** in the **Source** folder of the lab, select **Begin\Begin.sln** in the folder for the language of your preference (C# or JavaScript) and click **Open**. Alternatively, you may continue with the solution that you obtained after completing the previous exercise.

1. Right-click the **References** folder and select **Add Reference...**. Under **Windows | Extensions**, check **Microsoft Player Framework Advertising Plugin** and click **OK**.

	![Adding reference to the Advertising Plugin C#](Images/adding-reference-to-advertising-plugin-cs.png?raw=true "Adding reference to the Advertising Plugin C#")

    _Adding reference to the Advertising Plugin C#_

	![Adding reference to the Advertising Plugin JavaScript](Images/adding-reference-to-advertising-plugin-js.png?raw=true "Adding reference to the Advertising Plugin JavaScript")

    _Adding reference to the Advertising Plugin JavaScript_

1. Add the following namespace reference for the _Microsoft Player Framework Advertising Plugin_ at the top of the **MainPage.xaml** file (for the C# project) or at the end of the head section in the **default.html** file (for the JavaScript project).

	C#

	(Code Snippet - _Intro to Media Services - Ex4 - XAML using statements_)

	<!-- mark:10 -->
	````XAML
	<Page
		 x:Class="SampleMediaPlayer.MainPage"
		 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
		 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
		 xmlns:local="using:SampleMediaPlayer"
		 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
		 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
		 xmlns:PlayerFramework="using:Microsoft.PlayerFramework"
		 xmlns:adaptive="using:Microsoft.PlayerFramework.Adaptive"
		 xmlns:ads="using:Microsoft.PlayerFramework.Advertising"
		 mc:Ignorable="d">
	````

	JavaScript

	(Code Snippet - _Intro to Media Services - Ex4 - Advertising references_)

	<!-- mark:21-23 -->
	````HTML
	<head>
		 <meta charset="utf-8" />
		 <title>SampleMediaPlayer</title>

		 <!-- WinJS references -->
		 <link href="//Microsoft.WinJS.2.0/css/ui-dark.css" rel="stylesheet" />
		 <script src="//Microsoft.WinJS.2.0/js/base.js"></script>
		 <script src="//Microsoft.WinJS.2.0/js/ui.js"></script>

		 <!-- SampleMediaPlayer references -->
		 <link href="/css/default.css" rel="stylesheet" />
		 <script src="/js/default.js"></script>

		 <!-- PlayerFramework references -->
		 <link href="/Microsoft.PlayerFramework.Js/css/PlayerFramework-dark.css" rel="stylesheet">
		 <script src="/Microsoft.PlayerFramework.Js/js/PlayerFramework.js"></script>

		 <!-- PlayerFramework.Adaptive references -->
		 <script src="/Microsoft.PlayerFramework.Js.Adaptive/js/PlayerFramework.Adaptive.js"></script>

		 <!-- PlayerFramework Advertising references -->
		 <link href="/Microsoft.PlayerFramework.Js.Advertising/css/PlayerFramework.Advertising.css" rel="stylesheet">
		 <script src="/Microsoft.PlayerFramework.Js.Advertising/js/PlayerFramework.Advertising.js"></script>
	</head>
	````

1. In the media player control, change the **Source** property (for the C# version) or the **src** property (for the JavaScript version) to point to the URL of the video encoded in smooth streaming at the end of Exercise 2.

	C#

	<!-- mark:6 -->
	````XAML
    <PlayerFramework:MediaPlayer HorizontalAlignment="Left"
								Height="600"
								Margin="200,96,0,0"
								VerticalAlignment="Top"
								Width="1000"
								Source="[YOUR-MEDIA-SERVICE-ENCODED-VIDEO-URL]">
        <PlayerFramework:MediaPlayer.Plugins>
            <adaptive:AdaptivePlugin />
        </PlayerFramework:MediaPlayer.Plugins>
    </PlayerFramework:MediaPlayer>
	````

	JavaScript

	<!-- mark:6 -->
	````HTML
	<div data-win-control="PlayerFramework.MediaPlayer" 
		data-win-options="{                                 
						  width: 1000,
						  height: 600,
						  autoplay: true,
						  src: '[YOUR-MEDIA-SERVICE-ENCODED-VIDEO-URL]',
				  }">
	</div>
	````

1. Now you will insert a new **VmapSchedulerPlugin** plugin to the media player that you added in the previous exercise pointing to the _vmap.xml_ file that you will add to the project's local assets folder in the next task. To do this, update the media player control with the following code:

	C#

	(Code Snippet - _Intro to Media Services - Ex4 - XAML VMap Scheduler plugin_)

	<!-- mark:9-10 -->
	````XAML
	<PlayerFramework:MediaPlayer HorizontalAlignment="Left"
								Height="600"
								Margin="200,96,0,0"
								VerticalAlignment="Top"
								Width="1000"
								Source="[YOUR-MEDIA-SERVICE-VIDEO-URL]">
		<PlayerFramework:MediaPlayer.Plugins>
			<adaptive:AdaptivePlugin />
			<ads:VmapSchedulerPlugin Source="ms-appx:///Assets/vmap.xml" />
			<ads:AdHandlerPlugin />
		</PlayerFramework:MediaPlayer.Plugins>
	</PlayerFramework:MediaPlayer>
	````

	JavaScript

	(Code Snippet - _Intro to Media Services - Ex4 - HTML VMap Scheduler plugin_)

	<!-- mark:7-9 -->
	````HTML
	<div data-win-control="PlayerFramework.MediaPlayer" 
         data-win-options="{                                 
                                width: 1000,
                                height: 600,
                                autoplay: true,
                                src: '[YOUR-MEDIA-SERVICE-VIDEO-URL]',
                                vmapSchedulerPlugin: {
                                    source: 'ms-appx:///Assets/vmap.xml'
                                }
                          }">
    </div>
	````

<a name="exploring-vmap-file-and-running-app" />
#### Task 2 - Exploring the VMAP file and running the app ####

In this task you will add an already pre-configured VMAP file to the local assets folder of the application and explore its main content. Finally, you will run the application to check that the advertisements are displayed at the beginning of the video.

1. In Solution Explorer, right-click the **Assets** folder of the SampleMediaPlayer project and select **Add | Existing Item**. Browse to the **Source/Assets** folder of this lab, select the _vmap.xml_ file and click **Add**.

	> **Note:** For the JavaScript version, you will have to manually create the Assets folder in the project. To do this, right-click the **SampleMediaPlayer** project, select **Add | New Folder** and name it _Assets_.

	![Importing the VMAP file](Images/importing-the-vmap-file.png?raw=true "Importing the VMAP file")

    _Importing the VMAP file_

	> **Note:** The vmap.xml file is inserted in the local assets folder of the solution just for example purposes. However, you should not distribute this file in your solutions because anybody could modify the advertisements that you wish to display. Ideally, this file should be placed in your Advertisement Server along with the advertising content.

1. Open the **vmap.xml** file and explore its content.

	````XML
	<vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
		<vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
			<vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
				<vmap:VASTData>
				  <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
					 <Ad id="115571748">
						<InLine>
						  <AdSystem version="2.0 alpha">Atlas</AdSystem>
						  <AdTitle>Unknown</AdTitle>
						  <Description>Unknown</Description>
						  <Survey></Survey>
						  <Error></Error>
						  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
						  <Creatives>
							 <Creative id="video" sequence="0" AdID="">
								<Linear>
								  <Duration>00:00:32</Duration>
								  <MediaFiles>
									 <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
										<![CDATA[http://dpeshare.blob.core.windows.net/mediaserviceslabassets/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
									 </MediaFile>
									 <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
										<![CDATA[http://dpeshare.blob.core.windows.net/mediaserviceslabassets/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
									 </MediaFile>
									 <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
										<![CDATA[http://dpeshare.blob.core.windows.net/mediaserviceslabassets/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
									 </MediaFile>
									 <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
										<![CDATA[http://dpeshare.blob.core.windows.net/mediaserviceslabassets/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
									 </MediaFile>
								  </MediaFiles>
								</Linear>
							 </Creative>
						  </Creatives>
						</InLine>
					 </Ad>
				  </VAST>
				</vmap:VASTData>
			</vmap:AdSource>
			<vmap:TrackingEvents>
				<vmap:Tracking event="breakStart">
				  http://MyServer.com/breakstart.gif
				</vmap:Tracking>
			</vmap:TrackingEvents>
		</vmap:AdBreak>
	</vmap:VMAP>
	````

	The VMAP standard is used by content owners to describe ad breaks, such as the timing for each break, the number of ads available and which types should be supported. VMAP is very useful when content owners don't have control over the video player.

	**VMAP elements**

	**AdBreak** is used to specify at which moment an ad should be played, whether at the beginning or end of the video, after certain percentage played or at specific hours/minutes/seconds.

	**AdSource** is used to specify which ads should be displayed in an ad break.

	**VASTData** tells video player what to play. All the ads to be displayed should be inside this container.

	**TrackingEvents:** it�s used to track the start and end of an ad break and whether an error occurred during the ad break.

	> **Note:** The media files used in the VMAP file provided are videos already uploaded to a blob storage. Their URIs can be found inside the MediaFile elements of the vmap.xml file.

1. Press **F5** to start the app. Notice that the advertisement is played in the video player according to the information provided in the VMAP file. When it ends, you should see the main content video starting.

	![Advertisement in running app](Images/advertisement-in-running-app.png?raw=true "Advertisement in running app")

    _Advertisement in running app_

	![Main content in running app](Images/store-app-running.png?raw=true "Main content in running app")

    _Main content in running app_

---

## Next Steps ##

To learn more about configuring **Microsoft Azure Media Services**, please refer to the following articles:

**Technical Reference**

This is a list of articles that expand on the technologies explained on this lab:

- [Developing Microsoft Azure Media Services Client Applications](http://aka.ms/S0u1ly): SDKs contain libraries and APIs that allow you to create client applications. Player Frameworks are built on top of the SDKs and contain user controls for common applications scenarios and out-of-the-box sample player applications and documentation. Both SDKs and Player Frameworks are available for multiple platforms.

- [Smooth Streaming Technical Overview ](http://aka.ms/Soeygn): The **Smooth Streaming Technical Overview** provides a comprehensive history, context, introduction, and technical description of Smooth Streaming.

- [Ingesting Assets in Bulk with the Media Services SDK for .NET](http://aka.ms/Fe4bp3): Uploading large asset files can be a bottleneck during asset creation. Ingesting Assets in Bulk or �Bulk Ingesting�, involves decoupling asset creation from the upload process.

- [Inserting Ads into your Media](http://aka.ms/Q3t667): Microsoft Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks. Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.

**Development**

This is a list of developer-oriented articles related to **Microsoft Azure Media Services**:

- [How to: Deliver an Asset by Download](http://aka.ms/Rtzki2): This topic discusses options for delivering media assets uploaded to Media Services. You can deliver Media Services content in numerous application scenarios. You can download media assets, or access them by using a locator. You can send media content to another application or to another content provider.

- [How to: Deliver streaming content](http://aka.ms/Ndbfmn): In addition to downloading media content from Media Services, you can use adaptive bitrate streaming to deliver content. For example, you can create a direct URL, called a locator, to streaming content on a Media Services origin server. Client applications such as Microsoft Silverlight can play the streaming content directly from the locator.

- [How to: Deliver Apple HLS streaming content](http://aka.ms/G6w163): This topic shows how to create a locator to Apple HTTP Live Streaming (HLS) content on a Media Services origin server. Using this approach, you can build a URL to Apple HLS content, and provide it to Apple iOS devices for playback.

- [Copying an Existing Blob into a Media Services Asset](http://aka.ms/X9koyj): This topic shows how to copy blobs from a storage account into a new Microsoft Azure Media Services asset.

---

<a name="Summary"></a>
## Summary ##
In this hands-on lab you have learned how to:

- Create a Media Services subscription.
- Upload, encode, and publish media content from the Microsoft Azure portal.
- Programmatically upload, encode, and publish media content using the Media Services SDK.
- Use the Microsoft Media Platform Player Framework to play smooth streaming content.
- Monetize your media content using ads defined in a VMAP file.
