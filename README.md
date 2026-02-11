name: YouTube Live Stream
on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install FFmpeg
      run: sudo apt update && sudo apt install -y ffmpeg

    - name: Stream to YouTube
      run: |
        ffmpeg -re -stream_loop -1 -i "1204.mp4" -vcodec libx264 -preset veryfast -b:v 3000k -maxrate 3000k -bufsize 6000k -pix_fmt yuv420p -g 50 -c:a aac -b:a 128k -ar 44100 -f flv "rtmp://a.rtmp.youtube.com/live2/${{ secrets.STREAM_KEY }}"
