Dualstream
==========

    # record 25 seconds
    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 \
	-t 25 \
	-c:a:0 flac -ac 1 \
	-c:v:0 libx264 -preset ultrafast -qp 0 \
	-c:v:1 libx264 -preset ultrafast -qp 0 \
	-y test.dualstream.mkv \
	-map 1:0 \
	-t 25 \
	-r '1/3' -updatefirst 1 stream00.png \
	-map 2:0 \
	-t 5 \
	-r '1/3' -updatefirst 1 stream01.jpg

    #Three streams
    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-f v4l2 -s 1280x720 -i /dev/video1 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 -map 3:0 \
	-c:a:0 flac -ac 1 \
	-c:v:0 libx264 -preset ultrafast -qp 0 \
	-c:v:1 libx264 -preset ultrafast -qp 0 \
	-c:v:2 libx264 -preset ultrafast -qp 0 \
	-y test.dualstream.mkv \
	-map 1:0 \
	-r '1/3' -updatefirst 1 stream00.png \
	-map 2:0 \
	-r '1/3' -updatefirst 1 stream01.jpg \
	-map 3:0 \
	-r '1/3' -updatefirst 1 stream02.jpg


    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a:0 flac -ac 1 \
	-c:v:0 libx264 -preset ultrafast -qp 0 \
	-c:v:1 libx264 -preset ultrafast -qp 0 \
	-y test.dualstream.mkv \
	-map 1:0 \
	-r '1/3' -updatefirst 1 stream00.png \
	-map 2:0 \
	-r '1/3' -updatefirst 1 stream01.jpg

    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a:0 flac -ac 1 \
	-c:v:0 mpeg2video -q:v:0 1 \
	-c:v:1 mpeg2video -q:v:1 1 \
	-y test.dualstream.mkv \
	-map 1:0 \
	-f image2 -vf select='isnan(prev_selected_t)+gte(t-prev_selected_t\,5)' stream00_%04d.png \
	-map 2:0 \
	-f image2 -vf select='isnan(prev_selected_t)+gte(t-prev_selected_t\,5)' stream01_%04d.png

    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a:0 flac -ac 1 \
	-c:v:0 mpeg2video -q:v:0 1 \
	-c:v:1 mpeg2video -q:v:1 1 \
	-y test.dualstream.mkv

    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 24 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a copy \
	-c:v mpeg2video -q:v 2 \
	-c:v mpeg2video -q:v 2 \
	-y test.dualstream.mkv

    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 30 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a flac \
	-c:v libx264 \
	-c:v libx264 \
	-y test.dualstream.mkv

    ffmpeg \
	-f alsa -ac 2 -i hw:0 \
	-f x11grab -s 1600x900 -i :0.0+0,0 \
	-f v4l2 -s 1280x720 -i /dev/video0 -r 30 \
	-map 0:0 -map 1:0 -map 2:0 \
	-c:a copy \
	-c:v copy \
	-c:v copy \
	-y test.dualstream.mkv

