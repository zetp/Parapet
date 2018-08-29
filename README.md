# Parapet

This apple script was written in 2008 as a result of discussion in one of apple user group forums. The idea was to have new functionality concerning window size which was lacking in the Finder. The idea was to have each Finder window (and each newly opened window) to have predefined size chosen by user. However the user should be able to change window size afterwards if he/she chooses to do so.

The script should be saved as app with option to stay open (such app is present in this repository). On launch it will open new window which user can resize to set up the desired size of windows (via "Get window size" button). Then when "Start" button is pressed the script will work in the background. It will set all open Finder window sizes to desired size as well as any new window. But it will do it only once for each window so user can still resize it if she/he desires.

Code is displayed below as Github does not display AppleScript:
<html>
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
  <meta http-equiv="Content-Style-Type" content="text/css">
  <title></title>
  <meta name="Generator" content="Cocoa HTML Writer">
  <meta name="CocoaVersion" content="1561.6">
  <style type="text/css">
    p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; color: #5f6060}
    p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; color: #5f6060; min-height: 15.0px}
    p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; min-height: 15.0px}
    p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana}
    p.p5 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; color: #0433ff}
    p.p6 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; color: #812fdc}
    p.p7 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px Verdana; color: #4e8f00}
    span.s1 {color: #4e8f00}
    span.s2 {color: #0433ff}
    span.s3 {color: #000000}
    span.s4 {color: #812fdc}
    span.s5 {color: #012fbe}
    span.s6 {color: #5730be}
    span.s7 {color: #5f6060}
    span.Apple-tab-span {white-space:pre}
  </style>
</head>
<body>
<p class="p1">(*</p>
<p class="p1">This apple script was written in 2008 as a result of discussion in one of apple user group forums. The idea was to have new functionality concerning window size which was lacking in the Finder. The idea was to have each Finder window (and each newly opened window) to have predefined size chosen by user. However the user should be able to change window size afterwards if he/she chooses to do so.</p>
<p class="p2"><br></p>
<p class="p1">The script should be saved as app with option to stay open. On launch it will open new window which user can resize to set up the desired size of windows (via "Get window size" button). Then when "Start" button is pressed the script will work in the background. It will set all open Finder window sizes to desired size as well as any new window. But it will do it only once for each window so user can still resize it if she/he desires.</p>
<p class="p1">*)</p>
<p class="p3"><br></p>
<p class="p4"><b>property</b> <span class="s1">lista_okien</span> : {}</p>
<p class="p4"><b>property</b> <span class="s1">lista_okien2</span> : {}</p>
<p class="p4"><b>property</b> <span class="s1">lista_temp</span> : {}</p>
<p class="p4"><b>property</b> <span class="s1">guzik</span> : ""</p>
<p class="p4"><b>property</b> <span class="s1">loop</span> : 0</p>
<p class="p4"><b>property</b> <span class="s1">wys</span> : 0</p>
<p class="p4"><b>property</b> <span class="s1">szer</span> : 0</p>
<p class="p3"><br></p>
<p class="p4"><b>on</b> <span class="s2"><b>run</b></span></p>
<p class="p3"><span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">loop</span> = 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p5"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span><b>make</b><span class="s3"> </span>new<span class="s3"> </span><i>Finder window</i></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">window_ID</span> <b>to</b> <span class="s4">id</span> <b>of</b> <span class="s2"><i>window</i></span> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s4">toolbar visible</span> <b>of</b> <b>the</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">window_ID</span> <b>to</b> <span class="s4"><i>true</i></span></p>
<p class="p6"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> </span>statusbar visible<span class="s3"> <b>of</b> <b>the</b> </span><span class="s2"><i>window</i></span><span class="s3"> </span><i>id</i><span class="s3"> </span><span class="s1">window_ID</span><span class="s3"> <b>to</b> </span><i>true</i></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> {<span class="s1">a</span>, <span class="s1">b</span>, <span class="s1">c</span>, <span class="s1">d</span>} <b>to</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">window_ID</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">szerokosc</span> <b>to</b> (<span class="s1">c</span> - <span class="s1">a</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">wysokosc</span> <b>to</b> (<span class="s1">d</span> - <span class="s1">b</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>delay</b></span> 0.5</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p3"><span class="Apple-tab-span">	</span></p>
<p class="p3"><span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">guzik</span> <b>to</b> "Get window size"</p>
<p class="p4"><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">guzik</span> <b>is</b> <b>not</b> "Get window size"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s5"><b>display dialog</b></span> "Set widow desired<span class="Apple-converted-space">  </span>size</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span>width: " &amp; <span class="s1">szerokosc</span> &amp; " height: " &amp; <span class="s1">wysokosc</span> <span class="s5">buttons</span> {"Quit", "Get window size", "Start"} <span class="s5">with icon</span> <span class="s6"><i>note</i></span> <span class="s5">with title</span> "Parapet"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s4">result</span> <b>to</b> <b>set</b> <span class="s1">guzik</span> <b>to</b> <span class="s6">button returned</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>if</b> <span class="s1">guzik</span> <b>is</b> "Get window size" <b>then</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> {<span class="s1">a</span>, <span class="s1">b</span>, <span class="s1">c</span>, <span class="s1">d</span>} <b>to</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">window_ID</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">szerokosc</span> <b>to</b> (<span class="s1">c</span> - <span class="s1">a</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">wysokosc</span> <b>to</b> (<span class="s1">d</span> - <span class="s1">b</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s5"><b>display dialog</b></span> "Hmm... looks like youhave closed the window or Finder is busy" <span class="s5">buttons</span> {"Quit"} <span class="s5">default button</span> 1 <span class="s5">with icon</span> <span class="s6"><i>note</i></span> <span class="s5">with title</span> "Parapet"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">guzik</span> <b>to</b> "Quit"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p3"><span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>if</b> <span class="s1">guzik</span> <b>is</b> "Quit" <b>then</b></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span><span class="s2"><b>quit</b></span><span class="s3"> <b>me</b> </span>-- koniec</p>
<p class="p3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>else</b> <b>if</b> <span class="s1">guzik</span> <b>is</b> "Start" <b>then</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> {<span class="s1">a</span>, <span class="s1">b</span>, <span class="s1">c</span>, <span class="s1">d</span>} <b>to</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">window_ID</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">szerokosc</span> <b>to</b> (<span class="s1">c</span> - <span class="s1">a</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">wysokosc</span> <b>to</b> (<span class="s1">d</span> - <span class="s1">b</span>)</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s5"><b>display dialog</b></span> "Hmm... looks like youhave closed the window or Finder is busy" <span class="s5">buttons</span> {"Quit"} <span class="s5">default button</span> 1 <span class="s5">with icon</span> <span class="s6"><i>note</i></span> <span class="s5">with title</span> "Parapet"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>quit</b></span> <b>me</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p7"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> </span>wys<span class="s3"> <b>to</b> </span>wysokosc</p>
<p class="p7"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> </span>szer<span class="s3"> <b>to</b> </span>szerokosc</p>
<p class="p3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span>--===pierwszy i ostatni raz===--</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">loop</span> = 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">lista_okien</span> <b>to</b> <span class="s4">id</span> <b>of</b> <b>every</b> <span class="s2"><i>window</i></span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>delay</b></span> 0.5</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">loop</span> = 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>with</b> <span class="s1">i</span> <b>in</b> <span class="s1">lista_okien</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> {<span class="s1">a</span>, <span class="s1">b</span>, <span class="s1">c</span>, <span class="s1">d</span>} <b>to</b> <b>get</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">i</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>if</b> (<span class="s1">c</span> - <span class="s1">a</span>) = <span class="s1">szer</span> <b>and</b> (<span class="s1">d</span> - <span class="s1">b</span>) = <span class="s1">wys</span> <b>then</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>else</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">c</span> <b>to</b> (<span class="s1">c</span> + (<span class="s1">szer</span> - (<span class="s1">c</span> - <span class="s1">a</span>)))</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">d</span> <b>to</b> (<span class="s1">d</span> + (<span class="s1">wys</span> - (<span class="s1">d</span> - <span class="s1">b</span>)))</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <b>the</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> (<span class="s1">i</span> <b>as</b> <span class="s2"><i>integer</i></span>) <b>to</b> {<span class="s1">a</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">b</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">c</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">d</span> <b>as</b> <span class="s2"><i>integer</i></span>}</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>delay</b></span> 0.5</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span></span>--===/pierwszy i ostatni raz===--</p>
<p class="p4"><b>end</b> <span class="s2"><b>run</b></span></p>
<p class="p3"><br></p>
<p class="p3"><br></p>
<p class="p5"><span class="s3"><b>on</b> </span><b>idle</b></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span></span>-- ===p?tla=== --</p>
<p class="p4"><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">loop</span> = 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">lista_okien2</span> <b>to</b> <span class="s4">id</span> <b>of</b> <b>every</b> <span class="s2"><i>window</i></span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>delay</b></span> 0.5</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p3"><span class="Apple-tab-span">	</span></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><b>if</b> </span><span class="s1">lista_okien</span><span class="s3"> = </span><span class="s1">lista_okien2</span><span class="s3"> <b>then</b> </span>-- je?li listy s? takie same nie rób nic</p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span>-- nic</p>
<p class="p4"><span class="Apple-tab-span">	</span><b>else</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>until</b> <span class="s1">loop</span> = 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>tell</b> <span class="s2"><i>application</i></span> "Finder"</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>with</b> <span class="s1">i</span> <b>in</b> <span class="s1">lista_okien2</span></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>if</b> <b>not</b> (</span><span class="s1">i</span><span class="s3"> <b>is</b> <b>in</b> </span><span class="s1">lista_okien</span><span class="s3">) <b>then</b> </span>-- porównanie nowa lista do starej</p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span>-- je?li nie ma<span class="Apple-converted-space"> </span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <b>the</b> <b>end</b> <b>of</b> <span class="s1">lista_okien</span> <b>to</b> (<span class="s1">i</span> <b>as</b> <span class="s2"><i>integer</i></span>) <span class="s7">-- to doda? je do lista_okien</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> {<span class="s1">a</span>, <span class="s1">b</span>, <span class="s1">c</span>, <span class="s1">d</span>} <b>to</b> <b>get</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> <span class="s1">i</span> <span class="s7">-- i je dopasowa? do wymiarów</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>if</b> (<span class="s1">c</span> - <span class="s1">a</span>) = <span class="s1">szer</span> <b>and</b> (<span class="s1">d</span> - <span class="s1">b</span>) = <span class="s1">wys</span> <b>then</b> <span class="s7">-- je?li wymiary s? dobre robi? nic</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s7">-- nic</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>else</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">c</span> <b>to</b> (<span class="s1">c</span> + (<span class="s1">szer</span> - (<span class="s1">c</span> - <span class="s1">a</span>)))</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">d</span> <b>to</b> (<span class="s1">d</span> + (<span class="s1">wys</span> - (<span class="s1">d</span> - <span class="s1">b</span>)))</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <b>the</b> <span class="s4">bounds</span> <b>of</b> <span class="s2"><i>window</i></span> <span class="s4"><i>id</i></span> (<span class="s1">i</span> <b>as</b> <span class="s2"><i>integer</i></span>) <b>to</b> {<span class="s1">a</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">b</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">c</span> <b>as</b> <span class="s2"><i>integer</i></span>, <span class="s1">d</span> <b>as</b> <span class="s2"><i>integer</i></span>}</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>else</b> </span>-- je?li jest</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s7">-- nic</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>tell</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 1</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>on</b> <b>error</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="s2"><b>delay</b></span> 0.5</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>try</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">loop</span> <b>to</b> 0</p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span></span>----</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>repeat</b> <b>with</b> <span class="s1">i</span> <b>in</b> <span class="s1">lista_okien</span></p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>if</b> (</span><span class="s1">i</span><span class="s3"> <b>is</b> <b>in</b> </span><span class="s1">lista_okien2</span><span class="s3">) <b>then</b> </span>-- porownanie stara lista do nowej</p>
<p class="p1"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <b>the</b> <b>end</b> <b>of</b> </span><span class="s1">lista_temp</span><span class="s3"> <b>to</b> (</span><span class="s1">i</span><span class="s3"> <b>as</b> </span><span class="s2"><i>integer</i></span><span class="s3">) </span>-- je?li jest zbudowa? list? temp<span class="Apple-tab-span">	</span></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>end</b> <b>repeat</b></p>
<p class="p7"><span class="s3"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> </span>lista_okien<span class="s3"> <b>to</b> </span>lista_temp</p>
<p class="p4"><span class="Apple-tab-span">	</span><span class="Apple-tab-span">	</span><b>set</b> <span class="s1">lista_temp</span> <b>to</b> {}</p>
<p class="p4"><span class="Apple-tab-span">	</span><b>end</b> <b>if</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>return</b> 1</p>
<p class="p4"><b>end</b> <span class="s2"><b>idle</b></span></p>
<p class="p1">-- ===/p?tla=== --</p>
<p class="p3"><br></p>
<p class="p5"><span class="s3"><b>on</b> </span><b>quit</b></p>
<p class="p4"><span class="Apple-tab-span">	</span><b>continue</b> <span class="s2"><b>quit</b></span></p>
<p class="p4"><b>end</b> <span class="s2"><b>quit</b></span></p>
</body>
</html>