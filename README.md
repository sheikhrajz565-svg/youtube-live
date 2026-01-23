name: YouTube Live Stream

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Install ffmpeg
        run: sudo apt update && sudo apt install -y ffmpeg

      - name: Stream to YouTube
        run: |
          ffmpeg -re -i "https://docs.google.com/uc?export=download&id=1Wf7w-oI0QIr5fHF-g2RX20JM73NTmaxe" \
          -c:v libx264 -preset veryfast -b:v 3000k -maxrate 3000k -bufsize 6000k \
          -pix_fmt yuv420p -g 50 -c:a aac -b:a 128k -f flv \
          "rtmp://a.rtmp.youtube.com/live2/${{ secrets.STREAM_KEY }}"
