## Low Latency CUVID FFmpeg

Reference URL
1. https://developer.nvidia.com/ffmpeg

Reference Documents
1. Using_FFmpeg_with_NVIDIA_GPU_Hardware_Acceleration_v01.4.pdf

Reference Version
1. NVIDIA CUDA Version : 10.2
2. NVIDIA Video Codec SDK Version : 9.1.23
3. FFmpeg Version : 4.2.2
4. Microsoft Visual Studio 2015

libavcodec\cuviddec.c

/* 
    20200106 lcj
    LowLatency
    Set flag CUVID_PKT_ENDOFPICTURE to signal that a complete packet has been sent to decode
*/
cupkt.flags |= CUVID_PKT_ENDOFPICTURE;

Compiling for Windows

1. Install msys2 from www.msys2.org

2. Clone ffnvcodec
`git clone https://git.videolan.org/git/ffmpeg/nv-codec-headers.git`

3. Clone FFmpeg's public GIT repository
`git clone https://git.ffmpeg.org/ffmpeg.git`

4. Create a folder named nv_sdk in the parent directory of FFmpeg

5. Copy all the header files from
`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\include`
`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2\lib\x64`

6. Launch VS2015 x64 Native Tools Command Prompt

7. From the Visual Studio x64 Native Tools Command Prompt, launch the MinGW64 environment by running mingw64.exe from the msys2 installation folder

8. In the MinGW64 environment, install the necessary packages
`pacman -S diffutils make pkg-config yasm`

9. Add the following paths by running the commands.
`export PATH="/c/Program Files (x86)/Microsoft Visual Studio 14.0/VC/bin/amd64/":$PATH`
`export PATH="/c/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v10.2/bin/":$PATH`

10. Goto nv-codec-headers directory and install ffnvcodec
`cd /f/nv_ffmpeg/nv-codec-headers/`
`make install PREFIX=/usr`

11. Go to the FFmpeg installation folder and run the following command
`cd ../ffmpeg/`
`./configure --enable-nonfree --enable-shared --enable-static --enable-cuda-nvcc --enable-cuvid --enable-nvenc --enable-libnpp --toolchain=msvc` `--extra-cflags=-I../nv_sdk/include --extra-ldflags=-libpath:../nv_sdk/x64`

12. Compile the code by executing the following command
`make -j 8`

