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
DecodeEncodeXBTProfile<br>
EditBinFile</b><br>


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
<b>EditBinFile</b><br>
Allows one to edit an XBT profile's meta data on the command line.<br>

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
javac -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar:lib/commons-cli-1.4.jar EditBinFile.java<br>

windows
-------

javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTest.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestASCII.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepths.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile.java<br>
javac -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar;lib/commons-cli-1.4.jar EditBinFile.java<br>

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
java -cp .:lib/AmverseasBinFileUtils.jar:lib/commons-math3-3.6.1.jar:lib/commons-cli-1.4.jar EditBinFile -help<br>

windows
-------

java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTest profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestASCII profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepths profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecoderTestGetDepthsTwoMeterResolution profile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar DecodeEncodeXBTProfile profile.bin copiedProfile.bin<br>
java -cp .;lib/AmverseasBinFileUtils.jar;lib/commons-math3-3.6.1.jar;lib/commons-cli-1.4.jar EditBinFile -help<br>





Plotting the profile in Octave or Matlab
----------------------------------------
Once compiled, you can read, edit and create an xbt profile with Octave or Matlab by importing<br>
the library. Open Octave or Matlab and navigate to the directory containing all the files.<br>
This should be the directory that has the lib folder.<br>
Here is an exmaple of how to plot temperature vs depth for profile.bin.<br>

javaaddpath([pwd(),'/lib/AmverseasBinFileUtils.jar'])<br>
javaaddpath([pwd(),'/lib/commons-math3-3.6.1.jar'])<br>
BinDecoder=javaObject('binfileutils.BinDecoder','profile.bin');<br>
XBTProfile=javaMethod('getXBTProfile',BinDecoder);<br>
temps=javaMethod('getTemperaturePoints',XBTProfile);<br>
DepthCalculator=javaObject('binfileutils.DepthCalculator',XBTProfile);<br>
depths=javaMethod('getMeasurementDepths',DepthCalculator);<br>
plot(temps,-depths)<br>


Two meter resolution check
--------------------------

You can do some interpolation and produce two meter resolution profiles withOctave or Matlab.<br>
Here is an example of a linear interpolation.<br>

Open Octave or Matlaband navigate to the directory containing profile.bin and do the following<br>

%determine max depth and floor the value<br>
maxDepth=floor(max(depths));<br>
%create matrix of depths starting at 2 and ending at maxDepth with a step of 2<br>
%increasing value every two meters<br> 
twoMeterDepths= [2:2:maxDepth];<br>
% get a piece-wise polynomial structure<br>
pp=interp1(depths,temps,'linear','pp');<br>
%evaluate piece-wise polynomial structure<br>
twoMeterTemps=ppval(pp,twoMeterDepths);<br>
%plot one on top of the other<br>
figure;<br>
hold on;<br>
plot(depths,temps,'x');<br>
plot(twoMeterDepths,twoMeterTemps);<br>




