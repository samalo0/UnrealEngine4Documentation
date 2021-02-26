# Unreal Engine 4 Documentation

## Pipleine State Object (PSO) Caching

### Enable Android Shader Stable Keys (Needed Later)

First, make the file (if it doesn't already exist, assuming you are using Android):
ProjectName/Platforms/Android/Config/AndroidEngine.ini

Add the shader stable keys value to this file:

[DevOptions.Shaders]
NeedsShaderStableKeys=true

### Setting Up Your Platform

Second, go to Windows->Developer Tools->Device Profiles in the editor. Find the platforms that you want to enable (for example, Android), and click the … at the end of their name.
Find the rendering section in the console variables, and add r.ShaderPipelineCache.Enabled = 1.

Make sure to use the "Save as Default" button on the top to create the file, which will be located in ProjectName/Config/DefaultDeviceProfiles.ini.

### Setting Up Project Launcher

Under the launch button, open the project launcher, and create a custom launch profile. Name it the name of your project with PSO in the title.

Point it to your project, leave the configuration as development, then select cooking by the book, and select your platforms (Android and Androd_ASTC, or whichever shows up on your device as default).

Select deploy to your device, and select the variant that matches (ASTC).

Launch with the additional command line parameter -logpso.

Click the arrow to go back.

### Generating the PSO File

Use the project launcher to launch the custom launch profile on your device. Play the game for a few minutes (we are just checking that it generates the file currently, normally you'd have to play through the entire game to generate the full file). Once you've finished playing, look in the device in UE4Game/ProjectName/ProjectName/Saved/CollectedPSOs for the file.

If the folder does not exist, then you can look in Saved/Logs and see what happened, if it failed saving the file. This can occur if you don't have the console variable set properly or the command line argument set; make sure both are present in the log.

### Building PSO File

Copy the file from the device to C:/PSOCaching (make the folder).
Copy the shader stable keys from ProjectName/Saved/Cooked/Platform/ProjectName/MetaData/PipelineCaches to that folder. If they don't appear, the shader stable keys have not been enabled properly.

We need to execute an engine binary file to combine the files. Below is an example of how to do this; make sure that the final argument, which is the name of the output file, matches the type of the input files.

D:\UnrealEngine\UE_4.26\Engine\Binaries\Win64\UE4Editor-Cmd.exe "D:\p4v\Siderite\Siderite.uproject" -run=ShaderPipelineCacheTools expand C:/PSOCaching/*.rec.upipelinecache C:/PSOCaching/*.scl.csv Siderite_SF_VULKAN_ES31_ANDROID_NOUB.stablepc.csv

### Placing the File

Go back to where the engine binaries are in the file explorer, and find your created CSV file in that folder. Move it to ProjectName/Build/Platform/PipelineCaches folder. You may have to make the folder.
Example:

D:/p4v/Siderite/Build/Android/PipelineCaches

### Checking

Now run the build on your device, and check that the log file says that it loaded and used the file.
