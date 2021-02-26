# UnrealEngine4Documentation

## Pipleine State Object (PSO) Caching

### Android Shader Stable Keys

First, make the file (if it doesn't already exist, assuming you are using Android):
ProjectName/Platforms/Android/Config/AndroidEngine.ini

Add the shader stable keys value to this file:

[DevOptions.Shaders]
NeedsShaderStableKeys=true

### Setting Up Your Platform
Go to Windows->Developer Tools->Device Profiles in the editor.
Find the platforms that you want to enable, and click the … at the end of their name.
Find the rendering section in the console variables, and add r.ShaderPipelineCache.Enabled = 1.
