# Tetoris PNG Grid Generator

Creates a png grid video of Kasane Teto Spinning 

This project comes from my previous project with [badapple](). But is slightly modified to handle teto and also carries the Python Implementation as the main part since it is easier to run and for this project it only has to process one iteration of the spin and FFMPEG is responsible for processing the rest.

This project requires installing OpenCV and ffmpeg. Can be used in a windows environment but linux is preferred. I use WSL with Ubuntu and it works just fine.

## Setup and Installation (Python)

> [!Note]
> **The following commands are for an Ubuntu/Debian environment. If you are using a different distro then you need to look up the correct command.**

Before doing the commands below make sure that you update apt using the command below:

    sudo apt update

### 1. Setting up [OpenCV](https://opencv.org/)

Install the OpenCV libraries using the command below:

    pip install opencv-python

### 2. Setting up [PyAV](https://github.com/PyAV-Org/PyAV)

Install the PyAV libraries using the command below:

    pip install av
    
### 3. Setting up ffmpeg (for audio)

Install the ffmpeg libraries using the command below:

    sudo apt install libx264-dev ffmpeg

### 4. Running the project

1. Once sucessfully setup, run the program by using the command below:

> [!Note]
> **Command format:** python3 tetoris.py \<input filename> \<pixel size (W/H)> \<black pixel filename> \<white pixel filename> \<output filename>
>
> The following example line uses the included example PNGs called black.png and white.png with a size of 20x20

        python3 tetoris.py teto.mp4 20 black.png white.png output.mp4
		
2. Run the following ffmpeg command to extend the processed spin iteration to the approximate length of the audio

		ffmpeg -stream_loop 52 -i output.mp4 -c copy tetoris.mp4

3. Run the following ffmpeg command if you want to remux the audio to the output video from the program as it will not retain the audio from the input video.
    
        ffmpeg -i tetoris.mp4 -i tetoris.mp3 -c:v copy -c:a aac -b:a 200k -map 0:v:0 -map 1:a:0 -shortest -y tetoris-audio.mp4
