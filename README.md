Skip to content
 
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 @YunsuC Sign out
1
0 0 YunsuC/yunsuc.github.com
 Code  Issues 0  Pull requests 0  Projects 0  Wiki  Insights  Settings
yunsuc.github.com/Poisson Blending with Mixed Gradients.htm
9e3d814  10 minutes ago
@YunsuC YunsuC Add files via upload
     
501 lines (412 sloc)  25.6 KB
<html>

<head>
<meta http-equiv=Content-Type content="text/html; charset=ks_c_5601-1987">
<meta name=Generator content="Microsoft Word 15 (filtered)">
<style>
<!--
 /* Font Definitions */
 @font-face
	{font-family:"Cambria Math";
	panose-1:2 4 5 3 5 4 6 3 2 4;}
@font-face
	{font-family:"맑은 고딕";
	panose-1:2 11 5 3 2 0 0 2 0 4;}
@font-face
	{font-family:"\@맑은 고딕";
	panose-1:2 11 5 3 2 0 0 2 0 4;}
 /* Style Definitions */
 p.MsoNormal, li.MsoNormal, div.MsoNormal
	{margin-top:0cm;
	margin-right:0cm;
	margin-bottom:8.0pt;
	margin-left:0cm;
	text-align:justify;
	text-justify:inter-ideograph;
	line-height:107%;
	text-autospace:none;
	word-break:break-hangul;
	font-size:10.0pt;
	font-family:"맑은 고딕";}
span.MsoPlaceholderText
	{color:gray;}
p.MsoListParagraph, li.MsoListParagraph, div.MsoListParagraph
	{margin-top:0cm;
	margin-right:0cm;
	margin-bottom:8.0pt;
	margin-left:40.0pt;
	text-align:justify;
	text-justify:inter-ideograph;
	line-height:107%;
	text-autospace:none;
	word-break:break-hangul;
	font-size:10.0pt;
	font-family:"맑은 고딕";}
.MsoChpDefault
	{font-family:"맑은 고딕";}
.MsoPapDefault
	{margin-bottom:8.0pt;
	text-align:justify;
	text-justify:inter-ideograph;
	line-height:107%;}
 /* Page Definitions */
 @page WordSection1
	{size:595.3pt 841.9pt;
	margin:3.0cm 72.0pt 72.0pt 72.0pt;}
div.WordSection1
	{page:WordSection1;}
 /* List Definitions */
 ol
	{margin-bottom:0cm;}
ul
	{margin-bottom:0cm;}
-->
</style>
</head>
<body lang=KO>
<div class=WordSection1>
<p class=MsoNormal align=center style='text-align:center'><b><span lang=EN-US
style='font-size:14.0pt;line-height:107%;font-family:"Times New Roman",serif'>Poisson
Blending with Mixed Gradients</span></b></p>
<p class=MsoNormal align=right style='text-align:right'><span lang=EN-US
style='font-family:"Times New Roman",serif'>2016314430 Yunsu Choi</span></p>
<p class=MsoNormal align=right style='text-align:right'><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoListParagraph style='margin-left:38.0pt;text-indent:-18.0pt'><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>1.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>Toy
Problem</span></b></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>To
perform Poisson Blending, we proceeded with the Toy Problem to restore the
original image from zero image with minimal gradient from the original image.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>To
obtain an image satisfying all three equations, we wrote the source code as
shown below.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>Denote
the intensity of the source image at (x,y) as s(x,y), and the values of the
image to solve for as v(x,y). </span></p>
<p class=MsoListParagraph style='margin-left:38.0pt'><span
lang=EN-US style='font-size:10.0pt;line-height:107%;font-family:"맑은 고딕"'><img
width=391 height=25
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image001.png"></span></p>
<p class=MsoListParagraph style='margin-left:38.0pt'><span
lang=EN-US style='font-size:10.0pt;line-height:107%;font-family:"맑은 고딕"'><img
width=391 height=25
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image002.png"></span></p>
<p class=MsoListParagraph style='margin-left:38.0pt'><span
lang=EN-US style='font-size:10.0pt;line-height:107%;font-family:"맑은 고딕"'><img
width=195 height=25
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image003.png"></span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>I = double(imread(</span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:#A020F0'>'toy_problem.png'</span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:black'>));</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>[imh, imw, nn] = size(I);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>Im2var = zeros(imh,imw);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>Im2var(1:imh*imw) = 1:imh*imw;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>A =
sparse([],[],[],1+(imw-1)*imh+(imh-1)*imw,imw*imh);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>b(1) = I(1,1);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>A(1,:) = zeros(1,imh*imw);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>A(1,1) = 1;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:blue'>for</span><span lang=EN-US
style='font-size:9.0pt;font-family:"Courier New";color:black'>
k=1:(imw-1)*imh+(imh-1)*imw</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp; k</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp; </span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:blue'>if</span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:black'> k
&lt; (imw-1)*imh + 1</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
y = floor(1+(k-1)/imw);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
x = 1+mod(k-1,imw-1);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
A(k+1,Im2var(y,x+1)) = 1;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
A(k+1,Im2var(y,x)) = -1;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
b(k+1) = I(y,x+1) - I(y,x);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp; </span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:blue'>else</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
k_temp = k-imh*(imw-1);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
y = 1+mod(k_temp-1,imh-1);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
x = floor(1+(k_temp-1)/imh);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
A(k+1,Im2var(y+1,x)) = 1;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
A(k+1,Im2var(y,x)) = -1;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
b(k+1) = I(y+1,x) - I(y,x);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>&nbsp;&nbsp;&nbsp; </span><span
lang=EN-US style='font-size:9.0pt;font-family:"Courier New";color:blue'>end</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:blue'>end</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:blue'>&nbsp;</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>v = A\b';</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>v = reshape(v,[119,110]);</span></p>
<p class=MsoNormal align=left style='margin-top:0cm;margin-right:0cm;
margin-bottom:0cm;margin-left:20.0pt;margin-bottom:.0001pt;text-align:left;
line-height:normal;word-break:keep-all'><span lang=EN-US style='font-size:9.0pt;
font-family:"Courier New";color:black'>imshow(v,[])</span></p>
<p class=MsoNormal><span lang=EN-US style='font-size:11.0pt;line-height:107%;
font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>Since
Matrix A is sparse, we use MATLAB’s <i>sparse </i>function to initialize it so
that the \ operator can run fast. The results of the Toy Problem is as follows.
From the left are the original image, the output image and the error image of
the two images.</span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=123 height=132
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image004.png"><img
width=121 height=130
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image005.png"><img
width=123 height=130 id="그림 6"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image006.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>From
the results, we verified that the Matrix for finding the x-gradient and
y-gradient of the image works well.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:11.0pt;line-height:107%;font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoListParagraph style='margin-left:38.0pt;text-indent:-18.0pt'><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>2.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></b><span
lang=EN-US style='font-size:10.0pt;line-height:107%;font-family:"맑은 고딕";
position:relative;top:4.0pt'><img width=7 height=20
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image007.png"></span><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>Poisson
Blending with Mixed Gradients</span></b></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>Unlike
the Toy problem above, Poisson blending had to solve the least squares problem.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US><img width=571
height=59 id="그림 1"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image008.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>The
second term of the equation is an expression for the masked boundary. However,
in my source code, I excluded this term because the boundary portion became
awkward with the image from the first term. </span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>The
background image and input image to be used for Poisson blending are shown
below.</span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=475 height=342 id="그림 2"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image009.png"></span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=218 height=266 id="그림 3"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image010.png"></span><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img width=171 height=252
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image011.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>In
addition, to obtain a more natural image, we used a technique of mixing the
input image with the gradient of the background image. In Equation above, Av =
b, the elements of vector b are put into conditional as follows.</span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US><img width=508 height=66 id="그림 8"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image012.png"></span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US><img width=287 height=63 id="그림 9"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image013.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>The
results of Poisson blending are as follows.</span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=467 height=300 id="그림 10"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image014.png"></span></p>
<p class=MsoNormal align=center style='margin-left:20.0pt;text-align:center'><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>Input
image (left), Poisson Blended image (right)</span></p>
<p class=MsoNormal align=center style='text-align:center'><b><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=602 height=433 id="그림 11"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image015.png"></span></b></p>
<p class=MsoNormal><b><span lang=EN-US style='font-size:12.0pt;line-height:
107%;font-family:"Times New Roman",serif'><img width=602 height=433 id="그림 12"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image016.png"></span></b></p>
<p class=MsoNormal><b><span lang=EN-US style='font-size:12.0pt;line-height:
107%;font-family:"Times New Roman",serif'>&nbsp;</span></b></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>For
some results, Poisson blending did not work well because the background
brightness varies greatly.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=554 height=397
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image017.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=555 height=398 id="그림 5"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image018.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>In
order to solve this case, we blended naturally by histogram matching with
surrounding background values.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=592 height=425 id="그림 4"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image019.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>However,
there were still some points to be supplemented.</span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>&nbsp;</span></p>
<p class=MsoListParagraph style='margin-left:38.0pt;text-indent:-18.0pt'><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>3.<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'>Your
Own Examples</span></b></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=601 height=337 id="그림 20"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image020.png"><img
width=601 height=337 id="그림 21"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image021.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=601 height=429 id="그림 23"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image022.png"></span></p>
<p class=MsoNormal style='margin-left:20.0pt'><span lang=EN-US
style='font-size:12.0pt;line-height:107%;font-family:"Times New Roman",serif'><img
width=601 height=429 id="그림 22"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image023.png"></span></p>
<p class=MsoNormal align=right style='text-align:right'><span lang=EN-US
style='font-family:"Times New Roman",serif'><img width=546 height=469 id="그림 24"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image024.png"><img
width=546 height=469 id="그림 25"
src="Poisson%20Blending%20with%20Mixed%20Gradients.files/image025.png"></span></p>
</div>
</body>
</html>
© 2018 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
Press h to open a hovercard with more details.
