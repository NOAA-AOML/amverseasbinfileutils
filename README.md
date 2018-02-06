# amverseasbinfileutils
A package that contains classes to work wih XBT bin files generated by Amverseas<br>


-----------------------------------
**COMPILING AND USING THE LIBRARY**
------------------------------------

To compile, make sure that a java sdk version of at least 1.7 is installed<br>
and that the jar archive tool is installed.<br>

You can check by typing "javac -version"<br>
you should see something like "javac 1.7.0_65"<br>

Type "jar" and your screen should scroll with many jar options.<br>


-----------------
-Compile library-
-----------------

If using Windows run makeit.bat. If using linux/unix run makeit.sh .<br>
In linux/unix you will have to make makeit.sh executable.<br>
To make it executable type<br>

"chmod +x makeit.sh"<br>

When done compiling, AmverseasBinFileUtils.jar will be placed in the lib directory.<br>

--------------------------
-Example programs-
--------------------------

Some example programs are included to get an idea of how to use the library.<br>

<b>DecoderTest<br>
DecoderTestASCII<br>
DecoderTestGetDepths<br>
DecodeEncodeXBTProfile</b><br>


<b>DecoderTest</b><br>
Takes an XBT profile as an argument and prints the metadata and data to standard out.<br>
<b>DecoderTestASCII</b><br>
Takes an XBT profile as an argument and prints the metadata and data to standard out in the AOML ASCII format.<br>
<b>DecoderTestGetDepths</b><br>
Takes an XBT profile as an argument and prints the depth and temperature points to standard out.<br>
<b>DecoderTestGetDepthsTwoMeterResolution</b><br>
Takes an XBT profile as an argument and prints linearly interpolated depth and temperature points  at
two meter resolution to standard out.<br>
<b>DecodeEncodeXBTProfile</b><br>
Takes an XBT profile and a an output filename as arguments.It then extracts data from the input <br>
XBT profile and encodes it into a new profile. This example basically makes a copy of an XBT profile.<br>

--------------------------
-Compile example programs-
--------------------------

linux
-----

javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTest.java<br>
javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestASCII.java<br>
javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestGetDepths.java<br>
javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution.java<br>
javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile.java<br>

windows
-------

javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTest.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestASCII.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepths.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile.java<br>

----------------------
-Run example programs-
----------------------

linux
-----

java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTest profile.bin<br>
java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestASCII profile.bin<br>
java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestGetDepths profile.bin<br>
java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution profile.bin<br>
java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile profile.bin copiedProfile.bin<br>

windows
-------

java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTest profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestASCII profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepths profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile profile.bin copiedProfile.bin<br>



Two meter resolution check
--------------------------

You can ouput the depths and temperatures from DecoderTestGetDepths into a text file and interpolate in matlab or octave<br>
to double check the results.

in linux create profile.txt you can do the same in windows just use the appropriate command<br>

java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar DecoderTestGetDepths profile.bin > profile.txt<br>

You can copy paste the following into octave to compare the linear interpolation. This should also work in matlab.<br>
open octave and navigate to the directory containing profile.txt and paste the following<br>

%openfile created by DecoderTestGetDepths<br>
fid=fopen('profile.txt');<br>
%read in the depths and temperatures as floats.<br>
c=textscan(fid,'%f %f');<br>
%close file<br>
fclose(fid);<br>
%assign depths to x<br>
x=c{1};<br>
%assign temperature to y<br>
y=c{2};<br>
%dtermine max depth and floor the value<br>
maxDepth=floor(max(c{1}));<br>
%create matrix of depths starting at two and ending at maxDepth <br>
%increasing value every two meters<br> 
xq= [2:2:maxDepth];<br>
% get a piece-wise polynomial structure<br>
pp=interp1(x,y,'linear','pp');<br>
%evaluate piece-wise polynomial structure<br>
v=ppval(pp,xq);<br>
%examine values. index 1 is 2m, index 2 is 4m ect...<br>
v(2/2)<br>
v(maxDepth/2)<br>

%v contains all of the interpolated values, look through it.
