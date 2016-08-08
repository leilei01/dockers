FROM 192.168.217.40:5000/audio-tools
MAINTAINER leilei "leilei@taihe.com"

RUN mkdir -p /home/tools

#安装BOS SDK
RUN yum install -y unzip
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/bce-python-sdk-0.8.8.zip \
	&& unzip bce-python-sdk-0.8.8.zip \
	&& cd ./bce-python-sdk-0.8.8 \
	&&  python setup.py install

#安装orc-0.4.14
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/orc-0.4.14.tar.gz \
	&& tar xzf orc-0.4.14.tar.gz \
	&& cd orc-0.4.14 \
	&& /bin/sh ./configure \
	&& make && make install

#安装杜比工具
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/aac.tar.gz \
	&& tar zxf aac.tar.gz && cd aac \
	&& chmod a+x DolbyMediaGenerator-3.5.1-594907-Linux64.bin \ 
	&& echo accept | ./DolbyMediaGenerator-3.5.1-594907-Linux64.bin \
	&& dmg-license --add license.txt

#辅助工具安装
#安装gstreamer
WORKDIR /home/tools/
RUN yum install -y flex libgnomeui-devel
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/gstreamer-0.10.35.tar.gz \
	&& tar zxf gstreamer-0.10.35.tar.gz && cd gstreamer-0.10.35 \
	&& ./configure && make -j4 && make install 
RUN echo 'export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH' >> ~/.bashrc
RUN echo 'export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
RUN echo 'export PATH=/usr/local/bin:$PATH' >> ~/.bashrc
RUN source ~/.bashrc

#安装flump3dec（支持mp3格式
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/fluendo-mp3-17.x86_64.tar \
	&& tar -xf fluendo-mp3-17.x86_64.tar && cp -f codecs/libgstflump3dec.so /usr/local/lib/gstreamer-0.10 
RUN touch /etc/ld.so.conf.d/gstreamer.conf \
	&& echo '/usr/local/lib' >> /etc/ld.so.conf.d/gstreamer.conf \
	&& echo '/usr/local/lib/gstreamer-0.10' >> /etc/ld.so.conf.d/gstreamer.conf 
RUN ldconfig

#安装gst-plugins-base
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/gst-plugins-base-0.10.35.tar.gz \
	&& tar -zxf gst-plugins-base-0.10.35.tar.gz && cd gst-plugins-base-0.10.35 \
	&& ./configure && make -j4 && make install 

#安装gst-plugins-good
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/gst-plugins-good-0.10.30.tar.gz \
	&& tar -zxf gst-plugins-good-0.10.30.tar.gz && cd gst-plugins-good-0.10.30 \
	&& ./configure &&  make -j4 && make install 
RUN echo 'export GST_PLUGIN_PATH=/usr/local/lib/gstreamer-0.10:$GST_PLUGIN_PATH' >> ~/.bashrc
RUN source ~/.bashrc

#安装eyeD3
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/eyeD3-0.6.17.tar.gz \
	&& tar -zxf eyeD3-0.6.17.tar.gz && cd eyeD3-0.6.17 \
	&& ./configure &&  make -j4 && make install 

#libogg
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/libogg-1.3.2.tar.gz \
	&& tar -zxf libogg-1.3.2.tar.gz && cd libogg-1.3.2 \
	&& ./configure &&  make -j4 && make install 
RUN echo 'export C_INCLUDE_PATH=/usr/local/include/ogg:$C_INCLUDE_PATH' >> ~/.bashrc
RUN source ~/.bashrc

#libvorbis
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/libvorbis-1.3.4.tar.gz \
	&& tar -zxf libvorbis-1.3.4.tar.gz && cd libvorbis-1.3.4 \
	&& ./configure &&  make -j4 && make install 
RUN echo 'export C_INCLUDE_PATH=/usr/local/include/vorbis:$C_INCLUDE_PATH' >> ~/.bashrc
RUN source ~/.bashrc

#安装lame
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/lame-3.99.tar.gz \
	&& tar -zxf lame-3.99.tar.gz && cd lame-3.99 \
	&& ./configure --enable-shared &&  make -j4 && make install 
RUN echo 'export C_INCLUDE_PATH=/usr/local/include/lame:$C_INCLUDE_PATH' >> ~/.bashrc
RUN source ~/.bashrc

#ffmpeg
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/ffmpeg-0.8.5.tar.gz \
	&& tar -zxf ffmpeg-0.8.5.tar.gz && cd ffmpeg-0.8.5 \
	&& ./configure --enable-gpl --enable-shared --disable-demuxer=v4l --disable-demuxer=v4l2 --disable-muxer=v4l --disable-muxer=v4l2 --disable-indev=v4l --disable-indev=v4l2 --enable-libvorbis --enable-pthreads --enable-libmp3lame --disable-yasm \
	&& make -j4 && make install 

#flac
WORKDIR /home/tools/
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/flac-1.2.1.tar.gz \
	&& tar -zxf flac-1.2.1.tar.gz && cd flac-1.2.1 \
	&& sed -i '31a #include <string.h>' examples/cpp/encode/file/main.cpp
	&& ./configure  &&  make -j4 && make install 

#PIL
RUN  yum install -y tcl tcl-devel zlib zlib-devel libtiff libtiff-devel
RUN yum install -y libjpeg libjpeg-level libfreetype libfreetype-devel libjpeg-devel 
#RUN yum install -y littlecms littlecms-devel tkinter
RUN wget ftp://quku:quku0725f@192.168.219.85/quku/audio-tools/Imaging-1.1.7.tar.gz \
	&& tar -zxf Imaging-1.1.7.tar.gz && cd Imaging-1.1.7 
RUN 

#清理安装文件 
WORKDIR /home
RUN rm -rf /home/tools

USER work
CMD ["/bin/bash"]
 
         
