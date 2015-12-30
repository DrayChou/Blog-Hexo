---
date: 2011-02-18
layout:  post
title:  "php bmp格式图片转换成jpg格式程序"
tagline:
categories:
- web
tags:
- bmp
---
<div class="cnblogs_code">

    <?php
    /*
     * To change this template, choose Tools | Templates
     * and open the template in the editor.
    */
    //php教程将bmp格式图片转换成jpg格式程序
    function imagebmp($img,$file="",$rle=0) {

        $colorcount=imagecolorstotal($img);
        $transparent=imagecolortransparent($img);
        $istransparent=$transparent!=-1;

        if($istransparent) $colorcount--;
        if($colorcount==0) {
            $colorcount=0;
            $bitcount=24;
        };
        if(($colorcount>0)and($colorcount<=2)) {
            $colorcount=2;
            $bitcount=1;
        };
        if(($colorcount>2)and($colorcount<=16)) {
            $colorcount=16;
            $bitcount=4;
        };
        if(($colorcount>16)and($colorcount<=256)) {
            $colorcount=0;
            $bitcount=8;
        };

        $width=imagesx($img);
        $height=imagesy($img);
        $zbytek=(4-($width/(8/$bitcount))%4)%4;
        if($bitcount<24) $palsize=pow(2,$bitcount)*4;
        $size=(floor($width/(8/$bitcount))+$zbytek)*$height+54;
        $size+=$palsize;
        $offset=54+$palsize;
        // bitmap file header
        $ret = 'bm';                        // header (2b)
        $ret .= int_to_dword($size);        // size of file (4b)
        $ret .= int_to_dword(0);        // reserved (4b)
        $ret .= int_to_dword($offset);        // byte location in the file which is first byte of image (4b)
        // bitmap info header
        $ret .= int_to_dword(40);        // size of bitmapinfoheader (4b)
        $ret .= int_to_dword($width);        // width of bitmap (4b)
        $ret .= int_to_dword($height);        // height of bitmap (4b)
        $ret .= int_to_word(1);        // biplanes = 1 (2b)
        $ret .= int_to_word($bitcount);        // bibitcount = {1 (mono) or 4 (16 clr ) or 8 (256 clr) or 24 (16 mil)} (2b)
        $ret .= int_to_dword($rle);        // rle compression (4b)
        $ret .= int_to_dword(0);        // width x height (4b)
        $ret .= int_to_dword(0);        // bixpelspermeter (4b)
        $ret .= int_to_dword(0);        // biypelspermeter (4b)
        $ret .= int_to_dword(0);        // number of palettes used (4b)
        $ret .= int_to_dword(0);        // number of important colour (4b)
        // image data
        $cc=$colorcount;
        $sl1=strlen($ret);
        if($cc==0) $cc=256;
        if($bitcount<24) {
            $colortotal=imagecolorstotal($img);
            if($istransparent) $colortotal--;
            for($p=0;$p<$colortotal;$p++) {
                $color=imagecolorsforindex($img,$p);
                $ret.=inttobyte($color["blue"]);
                $ret.=inttobyte($color["green"]);
                $ret.=inttobyte($color["red"]);
                $ret.=inttobyte(0); //reserved
            };
            $ct=$colortotal;
            for($p=$colortotal;$p<$cc;$p++) {
                $ret.=inttobyte(0);
                $ret.=inttobyte(0);
                $ret.=inttobyte(0);
                $ret.=inttobyte(0); //reserved
            };
        };

        if($bitcount<=8) {
            for($y=$height-1;$y>=0;$y--) {
                $bwrite="";
                for($x=0;$x<$width;$x++) {
                    $color=imagecolorat($img,$x,$y);
                    $bwrite.=decbinx($color,$bitcount);
                    if(strlen($bwrite)==8) {
                        $retd.=inttobyte(bindec($bwrite));
                        $bwrite="";
                    };
                };
                if((strlen($bwrite)<8)and(strlen($bwrite)!=0)) {
                    $sl=strlen($bwrite);
                    for($t=0;$t<8-$sl;$t++)
                        $sl.="0";
                    $retd.=inttobyte(bindec($bwrite));
                };
                for($z=0;$z<$zbytek;$z++)
                    $retd.=inttobyte(0);
            };
        };
        if(($rle==1)and($bitcount==8)) {
            for($t=0;$t<strlen($retd);$t+=4) {
                if($t!=0)
                    if(($t)%$width==0)
                        $ret.=chr(0).chr(0);
                if(($t+5)%$width==0) {
                    $ret.=chr(0).chr(5).substr($retd,$t,5).chr(0);
                    $t+=1;
                }
                if(($t+6)%$width==0) {
                    $ret.=chr(0).chr(6).substr($retd,$t,6);
                    $t+=2;
                }
                else {
                    $ret.=chr(0).chr(4).substr($retd,$t,4);
                };
            };
            $ret.=chr(0).chr(1);
        }
        else {
            $ret.=$retd;
        };

        if($bitcount==24) {
            for($z=0;$z<$zbytek;$z++)
                $dopl.=chr(0);
            for($y=$height-1;$y>=0;$y--) {
                for($x=0;$x<$width;$x++) {
                    $color=imagecolorsforindex($img,imagecolorat($img,$x,$y));
                    $ret.=chr($color["blue"]).chr($color["green"]).chr($color["red"]);
                }
                $ret.=$dopl;
            };
        };
        if($file!="") {
            $r=($f=fopen($file,"w"));
            $r=$r and fwrite($f,$ret);
            $r=$r and fclose($f);
            return $r;
        }
        else {
            echo $ret;
        };
    };

    /*
    *------------------------------------------------------------
    *                    imagecreatefrombmp
    *------------------------------------------------------------
    *            - reads image from a bmp file
    *
    *         parameters:  $file - target file to load
    *
    *            returns: image id
    */
    function imagecreatefrombmp($file) {
        global  $currentbit, $echomode;
        $f=fopen($file,"r");
        $header=fread($f,2);
        if($header=="bm") {
            $size=freaddword($f);
            $reserved1=freadword($f);
            $reserved2=freadword($f);
            $firstbyteofimage=freaddword($f);
            $sizebitmapinfoheader=freaddword($f);
            $width=freaddword($f);
            $height=freaddword($f);
            $biplanes=freadword($f);
            $bibitcount=freadword($f);
            $rlecompression=freaddword($f);
            $widthxheight=freaddword($f);
            $bixpelspermeter=freaddword($f);
            $biypelspermeter=freaddword($f);
            $numberofpalettesused=freaddword($f);
            $numberofimportantcolors=freaddword($f);
            if($bibitcount<24) {
                $img=imagecreate($width,$height);
                $colors=pow(2,$bibitcount);
                for($p=0;$p<$colors;$p++) {
                    $b=freadbyte($f);
                    $g=freadbyte($f);
                    $r=freadbyte($f);
                    $reserved=freadbyte($f);
                    $palette[]=imagecolorallocate($img,$r,$g,$b);
                };

                if($rlecompression==0) {
                    $zbytek=(4-ceil(($width/(8/$bibitcount)))%4)%4;
                    for($y=$height-1;$y>=0;$y--) {
                        $currentbit=0;
                        for($x=0;$x<$width;$x++) {
                            $c=freadbits($f,$bibitcount);
                            imagesetpixel($img,$x,$y,$palette[$c]);
                        };
                        if($currentbit!=0) {
                            freadbyte($f);
                        };
                        for($g=0;$g<$zbytek;$g++)
                            freadbyte($f);
                    };
                };
            };

            if($rlecompression==1) //$bi_rle8
            {
                $y=$height;
                $pocetb=0;
                while(true) {
                    $y--;
                    $prefix=freadbyte($f);
                    $suffix=freadbyte($f);
                    $pocetb+=2;
                    $echoit=false;
                    if($echoit)echo "prefix: $prefix suffix: $suffix<br>";
                    if(($prefix==0)and($suffix==1)) break;
                    if(feof($f)) break;
                    while(!(($prefix==0)and($suffix==0))) {
                        if($prefix==0) {
                            $pocet=$suffix;
                            $data.=fread($f,$pocet);
                            $pocetb+=$pocet;
                            if($pocetb%2==1) {
                                freadbyte($f);
                                $pocetb++;
                            };
                        };
                        if($prefix>0) {
                            $pocet=$prefix;
                            for($r=0;$r<$pocet;$r++)
                                $data.=chr($suffix);
                        };
                        $prefix=freadbyte($f);
                        $suffix=freadbyte($f);
                        $pocetb+=2;
                        if($echoit) echo "prefix: $prefix suffix: $suffix<br>";
                    };
                    for($x=0;$x<strlen($data);$x++) {
                        imagesetpixel($img,$x,$y,$palette[ord($data[$x])]);
                    };
                    $data="";
                };
            };

            if($rlecompression==2) //$bi_rle4
            {
                $y=$height;
                $pocetb=0;
                /*while(!feof($f))
     echo freadbyte($f)."_".freadbyte($f)."<br>";*/
                while(true) {
    //break;
                    $y--;
                    $prefix=freadbyte($f);
                    $suffix=freadbyte($f);
                    $pocetb+=2;
                    $echoit=false;
                    if($echoit)echo "prefix: $prefix suffix: $suffix<br>";
                    if(($prefix==0)and($suffix==1)) break;
                    if(feof($f)) break;
                    while(!(($prefix==0)and($suffix==0))) {
                        if($prefix==0) {
                            $pocet=$suffix;
                            $currentbit=0;
                            for($h=0;$h<$pocet;$h++)
                                $data.=chr(freadbits($f,4));
                            if($currentbit!=0) freadbits($f,4);
                            $pocetb+=ceil(($pocet/2));
                            if($pocetb%2==1) {
                                freadbyte($f);
                                $pocetb++;
                            };
                        };
                        if($prefix>0) {
                            $pocet=$prefix;
                            $i=0;
                            for($r=0;$r<$pocet;$r++) {
                                if($i%2==0) {
                                    $data.=chr($suffix%16);
                                }
                                else {
                                    $data.=chr(floor($suffix/16));
                                };
                                $i++;
                            };
                        };
                        $prefix=freadbyte($f);
                        $suffix=freadbyte($f);
                        $pocetb+=2;
                        if($echoit) echo "prefix: $prefix suffix: $suffix<br>";
                    };
                    for($x=0;$x<strlen($data);$x++) {
                        imagesetpixel($img,$x,$y,$palette[ord($data[$x])]);
                    };
                    $data="";
                };
            };

            if($bibitcount==24) {
                $img=imagecreatetruecolor($width,$height);
                $zbytek=$width%4;
                for($y=$height-1;$y>=0;$y--) {
                    for($x=0;$x<$width;$x++) {
                        $b=freadbyte($f);
                        $g=freadbyte($f);
                        $r=freadbyte($f);
                        $color=imagecolorexact($img,$r,$g,$b);
                        if($color==-1) $color=imagecolorallocate($img,$r,$g,$b);
                        imagesetpixel($img,$x,$y,$color);
                    }
                    for($z=0;$z<$zbytek;$z++)
                        freadbyte($f);
                };
            };
            return $img;
        };

        fclose($f);

    };

    /*
    * helping functions:
    *-------------------------
    *
    * freadbyte($file) - reads 1 byte from $file
    * freadword($file) - reads 2 bytes (1 word) from $file
    * freaddword($file) - reads 4 bytes (1 dword) from $file
    * freadlngint($file) - same as freaddword($file)
    * decbin8($d) - returns binary string of d zero filled to 8
    * retbits($byte,$start,$len) - returns bits $start->$start+$len from $byte
    * freadbits($file,$count) - reads next $count bits from $file
    * rgbtohex($r,$g,$b) - convert $r, $g, $b to hex
    * int_to_dword($n) - returns 4 byte representation of $n
    * int_to_word($n) - returns 2 byte representation of $n
    */
    function freadbyte($f) {
        return ord(fread($f,1));
    };
    function freadword($f) {
        $b1=freadbyte($f);
        $b2=freadbyte($f);
        return $b2*256+$b1;
    };

    function freadlngint($f) {
        return freaddword($f);
    };
    function freaddword($f) {
        $b1=freadword($f);
        $b2=freadword($f);
        return $b2*65536+$b1;
    };

    function retbits($byte,$start,$len) {
        $bin=decbin8($byte);
        $r=bindec(substr($bin,$start,$len));
        return $r;
    };

    $currentbit=0;
    function freadbits($f,$count) {
        global $currentbit,$smode;
        $byte=freadbyte($f);
        $lastcbit=$currentbit;
        $currentbit+=$count;
        if($currentbit==8) {
            $currentbit=0;
        }
        else {
            fseek($f,ftell($f)-1);
        };
        return retbits($byte,$lastcbit,$count);
    };

    function rgbtohex($red,$green,$blue) {
        $hred=dechex($red);
        if(strlen($hred)==1) $hred="0$hred";
        $hgreen=dechex($green);
        if(strlen($hgreen)==1) $hgreen="0$hgreen";
        $hblue=dechex($blue);
        if(strlen($hblue)==1) $hblue="0$hblue";
        return($hred.$hgreen.$hblue);
    };
    function int_to_dword($n) {
        return chr($n & 255).chr(($n >> 8) & 255).chr(($n >> 16) & 255).chr(($n >> 24) & 255);
    }
    function int_to_word($n) {
        return chr($n & 255).chr(($n >> 8) & 255);
    }

    function decbin8($d) {
        return decbinx($d,8);
    };
    function decbinx($d,$n) {
        $bin=decbin($d);
        $sbin=strlen($bin);
        for($j=0;$j<$n-$sbin;$j++)
            $bin="0$bin";
        return $bin;
    };
    function inttobyte($n) {
        return chr($n);
    };

    //实例方法
    //include_once('bmp.php');
    $image=imagecreatefrombmp('a.bmp');
    imagejpeg($image,'a.jpeg');
    imagedestroy($image);
