## SDL Version 1.2.15

Downloaded from https://github.com/SDL-mirror/SDL/archive/release-1.2.15.zip
Possible other location: https://www.libsdl.org/release/SDL-1.2.15.zip from this page: https://www.libsdl.org/download-1.2.php

Extraced Zip file

Moved contents out of extracted directory and called it SDL-1.2.15

Opened .\SDL-1.2.15\VisualC\SDL.sln in Visual Studio and did the update prompt

Needed to bring open the properties for SDL and SDLmain project and change General setting of Windows SDK Version to 10.0.17134.0
This is because of a macro in winnt.h tries to verify an alignment and has a bug that makes it so Win32 doesn't build.
Could have done retarget solution.

Didn't need to do this with the download I did; but might need to depending on which download.
Copied SDL-1.2.15\include\SDL_config.h.default to SDL-1.2.15\include\SDL_config.h

Batch build everything

## SDL-ttf Version 2.0.11 (Yes it works with SDL 1.2.15)

Downloaded from https://github.com/SDL-mirror/SDL_ttf/archive/release-2.0.11.zip
Other location https://www.libsdl.org/projects/SDL_ttf/release/SDL_ttf-2.0.11.zip from this page: https://www.libsdl.org/projects/SDL_ttf/release-1.2.html

Extracted Zip file

Moved contents out of extracted directory and called it SDL_ttf-2.0.11

Opened .\SDL_ttf-2.0.11\VisualC\SDL_ttf.sln in Visual Studio and did the update prompt

Retarget solution and set Windows SDK Version to 10.0.17134.0 to match SDL

Added $(ProjectDir)..\..\SDL-1.2.15\include to the Additional Include Directories for SDL_ttf project
and $(ProjectDir)..\..\..\SDL-1.2.15\include to the Additional Include Directories for glfont and showfont projects

Added $(ProjectDir)..\..\..\SDL-1.2.15\VisualC\$(Configuration) and $(ProjectDir)..\..\..\SDL-1.2.15\VisualC\SDLmain\$(Configuration) to the Additional Library Directories for glfont and showfont projects for Win32 platform
And $(ProjectDir)..\..\..\SDL-1.2.15\VisualC\$(Platform)\$(Configuration) and $(ProjectDir)..\..\..\SDL-1.2.15\VisualC\SDLmain\$(Platform)\$(Configuration) for x64 platform

Added $(ProjectDir)..\..\SDL-1.2.15\VisualC\$(Configuration); and $(ProjectDir)..\..\SDL-1.2.15\VisualC\SDLmain\$(Configuration) 
   to the Additional Library Directories for SDL_ttf Win32 platform
and $(ProjectDir)..\..\SDL-1.2.15\VisualC\$(Platform)\$(Configuration); and $(ProjectDir)..\..\SDL-1.2.15\VisualC\SDLmain\$(Platform)\$(Configuration)
   for the x64 platform.
   
Batch build everything.
   
## SDL_gfx (Primatives)

Git clone of https://github.com/ferzkopp/SDL_gfx or download https://github.com/ferzkopp/SDL_gfx/archive/master.zip

Open SDL_gfx\SDL_gfx.sln in Visual Studio.  Upgrade the solution and project and retarget Windows SDK Version to 10.0.17134.0

Replace Additional Include Directories to be $(ProjectDir)..\SDL-1.2.15\include

Replace Additional Link Directories to be $(ProjectDir)..\SDL-1.2.15\VisualC\$(Configuration)

Change the Build Events Post-Build Events to be:
copy "$(TargetPath)" "$(SolutionDir)\Test\$(Configuration)"
copy "$(ProjectDir)\..\SDL-1.2.15\VisualC\SDL\$(Configuration)\SDL.dll" "$(SolutionDir)\Test\$(Configuration)"

Change each test project's Additional Include Directories to be ..\..\sdl_gfx;..\..\SDL-1.2.15\include;

Change each test project's Additional Link Directories to be:
..\..\sdl_gfx\$(Configuration);..\..\SDL-1.2.15\VisualC\SDLmain\$(Configuration);..\..\SDL-1.2.15\VisualC\$(Configuration);

The TestFonts test project will need it's Build Events Post-Build Event to be updated to:
copy $(<ProjectDir>)..\..\sdl_gfx\$(Configuration)\SDL_gfx.dll $(<TargetDir>)
copy $(<ProjectDir>)..\..\SDL-1.2.15\VisualC\SDL\$(Configuration)\SDL.dll $(<TargetDir>)

Delete Debug and Release files if they exist in the Test directory.

Make an x64 platform.

In x64 configurations remove the preprocessor define of USE_MMX that is in the debug configuration for SDL_gfx project.

Change the C/C++ Output Files path for ASM List Location to be $(IntDir) for SDL_gfx Debug|x64
Change the C/C++ Output Files path for Object File Name to be $(IntDir) for SDL_gfx Debug|x64
Change the C/C++ Output Files path for Program Database File name to be $(IntDir)vc$(PlatformToolsetVersion).pdb for SDL_gfx Debug|x64

Change the test Additional Link Directories to be ..\..\sdl_gfx\$(Platform)\$(Configuration);..\..\SDL-1.2.15\VisualC\SDLmain\$(Platform)\$(Configuration);..\..\SDL-1.2.15\VisualC\$(Platform)\$(Configuration); for the x64 platform.

Change the Linker Advanced setting of Import Library to be $(OutDir)$(TargetName).lib for x64 Platform configurations.

Batch build will work but not build solution because that builds multiple project simulaneously which uses the same PDB for the test projects

## For Cross-platform with NSpire

Copy SDL-1.2.15\include\*.h into a new folder called SDL: SDL-1.2.15\include\SDL (I did .* files)

Copy SDL_gfx\SDL_*.h into SDL-1.2.15\include\SDL

Copy SDL_ttf\SDL_*.h into SDL-1.2.15\include\SDL

