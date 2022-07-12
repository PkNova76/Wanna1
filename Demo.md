# **Demo các tool** <!-- omit in toc -->

# CLI Tools

Table of contents:
- [CLI Tools](#cli-tools)
  - [AudioStego (hideme)](#audiostego-hideme)
  - [jphide/jpseek](#jphidejpseek)
  - [jsteg](#jsteg)
  - [mp3stego](#mp3stego)
  - [openstego](#openstego)
  - [outguess](#outguess)
  - [stegano](#stegano)
  - [steghide](#steghide)
  - [cloackedpixel](#cloackedpixel)
  - [LSBSteg](#lsbsteg)
  - [f5](#f5)
  - [stegpy](#stegpy)

## AudioStego (hideme)

Giấu data
```
giấu string: hideme [input_file] "'message'" (nháy đôi bên ngoài nháy đơn)
giấu file: hideme [input_file] [secret_file]
```

Lấy data
```
hideme [input_file] -f
```

**Demo**
<pre>
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3  output.txt
root@65b55b89edc2:/data/examples/stego-files/mp3# <b><em>hideme hideme.mp3 -f</em></b>
Doing it boss! 
Looking for the hidden message...
File detected. Retrieving it...
Message recovered size: 31 bytes
File has been saved as: output.txt
Recovering process has finished successfully.
Cleaning memory...
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3  <b><em>output.txt</em></b>
root@65b55b89edc2:/data/examples/stego-files/mp3# cat output.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## jphide/jpseek

Giấu data
```
jphide [input_file] [output_file] [file_to_hide]

Input passphrase
```

Lấy data
```
jpseek [input_file] [output_file]
```

**Demo**
<pre>
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3  output.txt
root@65b55b89edc2:/data/examples/stego-files/mp3# <b><em>hideme hideme.mp3 -f</em></b>
Doing it boss! 
Looking for the hidden message...
File detected. Retrieving it...
Message recovered size: 31 bytes
File has been saved as: <b><em>output.txt</em></b>
Recovering process has finished successfully.
Cleaning memory...
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3  output.txt
root@65b55b89edc2:/data/examples/stego-files/mp3# cat output.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## jsteg

Giấu data
```
jsteg hide [input_file] [secret_file] [output_file]
```

Lấy data
```
jsteg reveal [input_file] [output_file]
```

**Demo**
<pre>
root@65b55b89edc2:/data# ls
<b><em>ORIGINAL.jpg</em></b>  ORIGINAL.mp3  ORIGINAL.png  ORIGINAL.wav  README.md  examples  <b><em>secret_message.txt</em></b>
root@65b55b89edc2:/data# cat secret_message.txt 
<b><em>This is a very secret message!</em></b>
root@65b55b89edc2:/data#<b><em> jphide ORIGINAL.jpg output.jpg secret_message.txt</em></b>

jphide, version 0.3 (c) 1998 Allan Latham <alatham@flexsys-group.com>

This is licenced software but no charge is made for its use.
NO WARRANTY whatsoever is offered with this product.
NO LIABILITY whatsoever is accepted for its use.
You are using this entirely at your OWN RISK.
See the GNU Public Licence for full details.

Passphrase: 
Re-enter  : 
root@65b55b89edc2:/data# ls
ORIGINAL.jpg  ORIGINAL.mp3  ORIGINAL.png  ORIGINAL.wav  README.md  examples  <b><em>output.jpg</em></b>  secret_message.txt
root@65b55b89edc2:/data#<b><em> jpseek output.jpg output.txt</em></b>

jpseek, version 0.3 (c) 1998 Allan Latham <alatham@flexsys-group.com>

This is licenced software but no charge is made for its use.
NO WARRANTY whatsoever is offered with this product.
NO LIABILITY whatsoever is accepted for its use.
You are using this entirely at your OWN RISK.
See the GNU Public Licence for full details.

Passphrase: 
root@65b55b89edc2:/data# ls
ORIGINAL.jpg  ORIGINAL.png  README.md  output.jpg  secret_message.txt
ORIGINAL.mp3  ORIGINAL.wav  examples   <b><em>output.txt</em></b>
root@65b55b89edc2:/data# cat output.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## mp3stego

**Lưu ý: Sử dụng absolute path cho các file.**

Giấu data **Input là WAV, có thể lỗi với vài file WAV** 

`ffmpeg -i audio.mp3 -flags bitexact audio.wav`
```
mp3stego-encode -E [secret_file] -P <password> /path/to/input_file.wav /path/to/output_file.mp3
```

Lấy data
```
mp3stego-decode -X -P <password> /path/to/input_file.mp3 /path/to/output_file.pcm /path/to/output_file.txt
```


**Demo**
<pre>
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3
root@65b55b89edc2:/data/examples/stego-files/mp3# <b><em>mp3stego-decode -X -P abcd /data/examples/stego-files/mp3/mp3stego.mp3 /data/examples/stego-files/mp3/output.pcm /data/examples/stego-files/mp3/output.txt</em></b>
MP3StegoEncoder 1.1.17
See README file for copyright info
Input file = '/data/examples/stego-files/mp3/mp3stego.mp3'  output file = '/data/examples/stego-files/mp3/output.pcm'
Will attempt to extract hidden information. Output: /data/examples/stego-files/mp3/output.txt
the bit stream file /data/examples/stego-files/mp3/mp3stego.mp3 is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=3, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=single-ch, sblim=32, jsbd=32, ch=1
[Frame 4295]Avg slots/frame = 417.862; b/smp = 2.90; br = 127.970 kbps
Decoding of "/data/examples/stego-files/mp3/mp3stego.mp3" is finished
The decoded PCM output file name is "/data/examples/stego-files/mp3/output.pcm"
WARNING: if you used relative paths, you find your results relative to "/opt/mp3stego/MP3Stego_1_1_18/MP3Stego/"
root@65b55b89edc2:/data/examples/stego-files/mp3# ls
hideme.mp3  mp3stego.mp3  <b><em>output.pcm  output.txt</em></b>
root@65b55b89edc2:/data/examples/stego-files/mp3# cat output.txt
<b><em>This is a very secret message!</em></b>
</pre>


## openstego

Giấu data
```
openstego embed -mf [secret_file] -cf [input_file] -p <password> -sf [output_file]
```

Lấy data (có thể có bỏ -xf)
```
openstego extract -sf [input_file] -p <password> -xf [output_file]
```

**Demo**
<pre>
root@d4b18ad1112d:/data/examples/stego-files/png# ls  
cloackedpixel.png  openstego.png  stegano-lsb.png  stegano-red.png
root@d4b18ad1112d:/data/examples/stego-files/png# <b><em>openstego extract -sf openstego.png -p abcd</em></b>
Extracted file: secret_message.txt
root@d4b18ad1112d:/data/examples/stego-files/png# cat secret_message.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## outguess

Giấu data
```
outguess -k <password> -d [secret_file] [input_file] [output_file]
```

Lấy data
```
outguess -r -k <password> [input_file] [output_file]
```

**Demo**
<pre>
root@e6da5eb4b90f:/data/examples/stego-files/jpg# ls
jsteg.jpg  outguess-0.13.jpg  outguess.jpg  steghide.jpg
root@e6da5eb4b90f:/data/examples/stego-files/jpg# <b><em>outguess -r -k abcd outguess.jpg output.txt</em></b>
Reading outguess.jpg....
Extracting usable bits:   139630 bits
Steg retrieve: seed: 176, len: 31
root@e6da5eb4b90f:/data/examples/stego-files/jpg# cat output.txt
<b><em>This is a very secret message!</em></b>
</pre>

## stegano

**Docs**

https://stegano.readthedocs.io/en/latest/software.html

**Demo**

<pre>
root@e6da5eb4b90f:/data/examples/stego-files/png# ls
cloackedpixel.png  openstego.png  secret_message.txt  stegano-lsb.png  stegano-red.png
root@e6da5eb4b90f:/data/examples/stego-files/png# <b><em>stegano-lsb reveal -i stegano-lsb.png </em></b>
<b><em>VGhpcyBpcyBhIHZlcnkgc2VjcmV0IG1lc3NhZ2UhCg==</em></b>
root@e6da5eb4b90f:/data/examples/stego-files/png#<b><em> stegano-lsb reveal -i stegano-lsb.png -e UTF-8 -o output.txt</em></b>  
root@e6da5eb4b90f:/data/examples/stego-files/png# ls
cloackedpixel.png  openstego.png  <b><em>output.txt</em></b>  secret_message.txt  stegano-lsb.png  stegano-red.png
root@e6da5eb4b90f:/data/examples/stego-files/png# cat output.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## steghide
Giấu data
```
steghide embed -ef [secret_file] -cf [input_file] -p <password> -sf [output_file]
```

Lấy data
```
steghide extract -sf [input_file] -p <password>
```

**Demo**
<pre>
root@e6da5eb4b90f:/data/examples/stego-files/wav# ls   
hideme.wav  steghide.wav
root@e6da5eb4b90f:/data/examples/stego-files/wav#<b><em> steghide info steghide.wav -p abcd</em></b>
"steghide.wav":
  format: wave audio, PCM encoding
  capacity: 302.1 KB
  embedded file "secret_message.txt":
    size: 31.0 Byte
    encrypted: rijndael-128, cbc
    compressed: yes
root@e6da5eb4b90f:/data/examples/stego-files/wav#<b><em> steghide extract -sf steghide.wav -p abcd</em></b>
wrote extracted data to "secret_message.txt".
root@e6da5eb4b90f:/data/examples/stego-files/wav# cat secret_message.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## cloackedpixel

Giấu data
```
cloackedpixel hide [input_file] [secret_file] <password>
```

Lấy data
```
cloackedpixel extract [input_file] [output_file] <password>
```

**Demo**
<pre>
root@e6da5eb4b90f:/data/examples/stego-files/png# ls
cloackedpixel.png  openstego.png  stegano-lsb.png  stegano-red.png
root@e6da5eb4b90f:/data/examples/stego-files/png# <b><em>cloackedpixel extract cloackedpixel.png output.txt abcd</em></b>
[+] Image size: 1280x959 pixels.
[+] Written extracted data to output.txt.
root@e6da5eb4b90f:/data/examples/stego-files/png# cat output.txt 
<b><em>This is a very secret message!</em></b>
</pre>

## LSBSteg

broken

## f5

Giấu data
```
f5 -t e -i [input_file] -o [output_file] -d 'secret_message'
```

Lấy data
```
f5 -t x -i [input_file]
```

**Demo**
<pre>
root@e6da5eb4b90f:/data/examples# ls          
ORIGINAL.jpg  ORIGINAL.mp3  ORIGINAL.png  ORIGINAL.wav  create_examples.sh  secret_message.txt  stego-files  stego.bmp
root@e6da5eb4b90f:/data/examples#<b><em> f5 -t e -i ORIGINAL.jpg -o output.jpg -d 'super secret message'</em></b>
2022-07-11 19:44:40,539 [jpeg_encoder] DCT/quantisation starts
2022-07-11 19:44:40,539 [jpeg_encoder] 1280 x 959
2022-07-11 19:44:42,078 [jpeg_encoder] got 1843200 DCT AC/DC coefficients
2022-07-11 19:44:42,190 [jpeg_encoder] one=76375
2022-07-11 19:44:42,191 [jpeg_encoder] large=90989
2022-07-11 19:44:42,191 [jpeg_encoder] expected capacity: 128412 bits
2022-07-11 19:44:42,191 [jpeg_encoder] expected capacity with
2022-07-11 19:44:42,191 [jpeg_encoder] default code: 16051 bytes (efficiency: 1.5 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 3, 2) code: 10701 bytes (efficiency: 1.8 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 7, 3) code: 6878 bytes (efficiency: 2.2 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 15, 4) code: 4278 bytes (efficiency: 2.7 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 31, 5) code: 2588 bytes (efficiency: 3.2 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 63, 6) code: 1527 bytes (efficiency: 3.8 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] (1, 127, 7) code: 873 bytes (efficiency: 4.3 bits per change)
2022-07-11 19:44:42,191 [jpeg_encoder] permutation starts
2022-07-11 19:44:46,528 [jpeg_encoder] Embedding of 192 bits (20+4 bytes)
2022-07-11 19:44:46,528 [jpeg_encoder] using (1, 63, 6) code
2022-07-11 19:44:46,553 [jpeg_encoder] 40 coefficients examined
2022-07-11 19:44:46,553 [jpeg_encoder] 72 coefficients changed (efficiency: 2.6 bits per change
2022-07-11 19:44:46,553 [jpeg_encoder] 37 coefficients thrown (zeroed)
2022-07-11 19:44:46,553 [jpeg_encoder] 192 bits (24 bytes) embedded
2022-07-11 19:44:46,553 [jpeg_encoder] starting hufman encoding
root@e6da5eb4b90f:/data/examples# ls 
ORIGINAL.jpg  ORIGINAL.png  create_examples.sh  secret_message.txt  stego.bmp
ORIGINAL.mp3  ORIGINAL.wav  output.jpg          stego-files
root@e6da5eb4b90f:/data/examples# <b><em>f5 -t x -i output.jpg </em></b>
2022-07-11 19:45:19,655 [jpeg_decoder] huffman decoding starts
2022-07-11 19:45:20,759 [jpeg_decoder] permutation starts
2022-07-11 19:45:25,174 [jpeg_decoder] 1843200 indices shuffled
2022-07-11 19:45:25,174 [jpeg_decoder] extraction starts
2022-07-11 19:45:25,174 [jpeg_decoder] length of embedded file: 20 bytes
2022-07-11 19:45:25,174 [jpeg_decoder] (1, 63, 6) code used
<b><em>super secret message</em></b>
</pre>

## stegpy

Giấu data
```
stegpy [secret_data] [input_file]
```

Lấy data
```
stegpy _[input_file]
```