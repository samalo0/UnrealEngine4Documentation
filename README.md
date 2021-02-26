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

### Generating PSO Data

Under the launch button, open the project launcher, and create a custom launch profile. Name it the name of your project with PSO in the title.

Point it to your project, leave the configuration as development, then select cooking by the book, and select your platforms (Android and Androd_ASTC, or whichever shows up on your device as default).

Select deploy to your device, and select the variant that matches (ASTC).

Launch with the additional command line parameter -logpso.

Click the arrow to go back.

### Generating the PSO File

