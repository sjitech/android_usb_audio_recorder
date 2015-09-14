# android_usb_audio_recorder

This is an experimental project aimed to record Android(4.4+) audio losslessly from PC via usb cable.<br>
####Not yet successful but fantastic. Welcome to join in and study together!<br>
This will be done by pretend PC as an USB audio device for android.<br>
This project use pyusb and libusb, tested on Mac OS X + usb cable + Android 4.4<br><br>

Most preparation work have been done such as pretending as an USB audio by raw usb communication (known as Android Accessory Mode).<br>
####But the output audio's quality is bad due to some reason, it's not fast enough to read PCM data from usb buffer, there are many 0x0 data.<br><br>


##Usage
####install <a href=https://github.com/walac/pyusb>pyusb</a>
####follow the pyusb instruction, install libusb or some other usb lib for pyusb.
####run audio.py

    ./audio.py > test.pcm

####The output file test.pcm contains data of PCM 16bit Little endian, 44100HZ
Example: A0 09 C0 01 A1 09 C2 01 .... means <br>
L Channel: 0x09A0, 0x09A1, ...<br>
R Channel: 0x01C0, 0x01C2, ...<br>
<br>
####to convert output to mp3 you can run command

    ffmpeg -f u16le -ar 44100 -ac 2 -i test.pcm test.mp3 -y

####If you want extract left channel only, then please uncomment following line

    buf_l = usb.util.create_buffer(cl/2) #left channel
    
####then you can convert to mp3 by following command
    ffmpeg -f u16le -ar 44100 -ac 1 -i test.pcm test.mp3 -y
