# .NET Core Support for MonoDevelop and Xamarin Studio

Provides [.NET Core and ASP.NET Core](https://dotnet.github.io/) support for .NET Core .xproj and project.json files in MonoDevelop and Xamarin Studio 6.0 or higher.

Please note that this does not support .NET Core 1.0 and higher which use SDK style .csproj files without an associated project.json file. Visual Studio for Mac and MonoDevelop 7.0 have built-in support .NET Core 1.0 and the new SDK style .csproj files.

This addin uses source code from [OmniSharp](https://github.com/OmniSharp/omnisharp-roslyn) in order to communicate with the .NET Core design time host. It also uses source code from [Roslyn](https://github.com/dotnet/roslyn), [Microsoft.AspNet.Hosting](https://github.com/aspnet/Hosting), [Microsoft.Framework.Logging](https://github.com/aspnet/Logging) and [Microsoft.Framework.OptionsModel](https://github.com/aspnet/Options/), since the Roslyn version of OmniSharp uses types from their corresponding NuGet packages.

# Licenses

 - DNX addin - MIT
 - [Microsoft.AspNet.Hosting](https://github.com/aspnet/Hosting) - Apache 2.0
 - [Microsoft.Framework.Logging](https://github.com/aspnet/Logging) - Apache 2.0
 - [Microsoft.Framework.OptionsModel](https://github.com/aspnet/Options/) - Apache 2.0
 - [OmniSharp](https://github.com/OmniSharp/omnisharp-roslyn) - MIT
 - [Roslyn](https://github.com/dotnet/roslyn) - Apache 2.0

# Building from source

From the src directory run NuGet restore.

    git clone git@github.com:mono/monodevelop.git
    cd monodevelop
    git checkout master
    git submodule update --init --recursive
    make
    rm -rf main/build/tests/
    cd ..

    git clone https://github.com/mhutch/MonoDevelop.AddinMaker
    cd MonoDevelop.AddinMaker
    nuget restore MonoDevelop.AddinMaker.sln
    make install /p:MDBinDir=../monodevelop/main/build/bin /p:MDProfileVersion=6.0

    git clone git@github.com:mrward/monodevelop-dnx-addin.git
    cd monodevelop-dnx-addins
    git checkout roslyn
    cd src
    nuget restore MonoDevelop.Dnx.sln
    xbuild MonoDevelop.Dnx.sln /p:MDProfileVersion=6.0 /p:MDBinDir=../../../monodevelop/main/build/bin
    
The last xbuild step can be replaced by opening the MonoDevelop.Dnx.sln into Xamarin Studio 6.0 and building the solution.

To create the addin .mpack file run:

    mdtool.exe setup pack bin/merged/MonoDevelop.Dnx.dll
    
# Debugging

You can debug the DNX addin if you have the Xamarin Studio 6.0 and the Addin Maker addin installed by selecting Start Debugging from the Run menu.
