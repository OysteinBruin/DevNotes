## vcpkg    
C/C++ dependency manager from Microsoft
For all platforms, buildsystems, and workflows

[vcpkg.io](https://vcpkg.io)      
[github](https://github.com/microsoft/vcpkg)

#### Getting started
Clone vcpkg `git clone https://github.com/microsoft/vcpkg.git`    

build vcpkg:   
`cd vcpkg`    
`bootstrap-vcpkg.bat`

Integrate vcpkg with shells and buildsystems. [Microsoft doc](https://learn.microsoft.com/en-us/vcpkg/commands/integrate)
Integrates with Visual Studio (Windows-only), sets the user-wide vcpkg instance, and displays CMake integration help.
`vcpkg integrate install`
