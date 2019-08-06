# alfalfa

### following the instruction via github page

https://github.com/excamera/alfalfa

### Install all the package by apt-get install


    g++ >= 5.0
    yasm
    libxinerama-dev
    libxcursor-dev
    libglu1-mesa-dev
    libboost-all-dev
    libx264-dev
    libxrandr-dev
    libxi-dev
    libglew-dev
    libglfw3-dev


### Install libjpeg

    apt-get install libjpeg9
    git clone https://github.com/LuaDist/libjpeg.git
    ./configure
    make && make install

### Change source code, incase gcc version not match (the source code is too old)

```
	diff --git a/src/input/jpeg.cc b/src/input/jpeg.cc
	index 9ceff65..f45de48 100644
	--- a/src/input/jpeg.cc
	+++ b/src/input/jpeg.cc
	@@ -62,11 +62,11 @@ void JPEGDecompresser::begin_decoding( const Chunk & chunk )
			 const_cast<uint8_t *>( chunk.buffer() ),
			 chunk.size() );
	 
	-  if ( JPEG_HEADER_OK != jpeg_read_header( &decompresser_, true ) ) {
	+  if ( JPEG_HEADER_OK != jpeg_read_header( &decompresser_, TRUE) ) {
	     throw runtime_error( "invalid JPEG" );
	   }
	 
	-  decompresser_.raw_data_out = true;
	+  decompresser_.raw_data_out = TRUE;
```

### Turn on the receiver

	salsify-receiver [PORT] 1280 720

### Turn on the sender

	salsify-sender --device [CAMERA, usually /dev/video0] --pixfmt YUYV [HOST] [PORT] 1337

	- My Thinkpad Camera could only use YUYV/YU12 pix format wrtten in src/input/camera.hh


!!! Not understand why the camera frames without color
