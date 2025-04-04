# VanitySearch
A version support custom range scanning and multi address scanning.

This is a modified version of VanitySearch by [JeanLucPons](https://github.com/JeanLucPons/VanitySearch/).

Performance optimization completed by [aaelick](https://github.com/aaelick). **Only one GPU per instance.**

# Build
## Windows

- Intall CUDA SDK and open VanitySearch.sln in Visual C++ 2017.
- You may need to reset your *Windows SDK version* in project properties.
- In Build->Configuration Manager, select the *Release* configuration.

- Note: The current relase has been compiled with CUDA SDK 10.0, if you have a different release of the CUDA SDK, you may need to update CUDA SDK paths in VanitySearch.vcxproj using a text editor. The current nvcc option are set up to architecture starting at 3.0 capability, for older hardware, add the desired compute capabilities to the list in GPUEngine.cu properties, CUDA C/C++, Device, Code Generation.

## Linux
- Edit the makefile and set up the appropriate CUDA SDK and compiler paths for nvcc.
    ```
    ccap=86
    
    ...
    
    CXX        = g++-9
    CUDA       = /usr/local/cuda-11.8
    CXXCUDA    = /usr/bin/g++-9
    ```

 - Build:
    ```
    $ make all
    ```
- **Attention!!! You need to use g++-9 or a lower version to compile, otherwise the program will not run properly.**

# Usage
- Example for bitcoin puzzle 68
    ```
    ./vanitysearch -t 0 -gpu -gpuId 0 -i in.txt -o out.txt --keyspace 80000000000000000:+FFFFFFFFFF
    ```

    ```
    in.txt
    1DRd8L1KktWwqVLm3myS4vugQV3ai1LPeN /privatekey:80000000000001000
    15oCidgtdDz6VVKiMsZjRvHR9scJvN9GAX /privatekey:80000000000100000
    1MVDYgVaSN6iKKEsbzRUAYFrYJadLYZvvZ /targetaddress
    ```

## CUDA Installation Linux
  ```
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-ubuntu2404.pin
    sudo mv cuda-ubuntu2404.pin /etc/apt/preferences.d/cuda-repository-pin-600
    wget https://developer.download.nvidia.com/compute/cuda/12.8.1/local_installers/cuda-repo-ubuntu2404-12-8-local_12.8.1-570.124.06-1_amd64.deb
    sudo dpkg -i cuda-repo-ubuntu2404-12-8-local_12.8.1-570.124.06-1_amd64.deb
    sudo cp /var/cuda-repo-ubuntu2404-12-8-local/cuda-B2775641-keyring.gpg /usr/share/keyrings/
    sudo apt-get update
    sudo apt-get -y install cuda-toolkit-12-8
 ```
