# Tooth Eater Module

Some early 2000's Honda CBR models use a 3-spoke cam trigger wheel. Some examples are the Honda Blackbird CBR1100XX, CBR600 and Honda Aquatrax. Other models may also use this pattern as well.

</br>
<table border="1">
<tr>
<td align="center" valign="center">
<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 50%;"
    src="./images/BB_ExhCam.png#center">
</img>

<p style="text-align: center;">The tooth shown in red is the reference tooth that is allowed through to the stand alone ECU. The other teeth are digitally deleted (eaten) by the tooth eater. This reference tooth also happens to align with TDC cylinder #1 & #4.</p>
</table>
</td>
</tr>
</br>

 While this 3-spoke pattern is designed to work with the OEM Keihin ECU, it will not work with many stand alone ECU's. Most 'off the shelf' stand alone ECU systems such as speeduino/RusEFI and others will cater for a single tooth pulse from the camshaft without fuss since this is a very standard configuration. In the past this issue is usually worked around by physically removing two teeth from the original cam trigger wheel (by grinding or hack-saw), leaving one behind. This works for a stand alone unit, but then renders the Keihin unit inoperative since it expects the 3 teeth.

You can watch the tooth eater in action working together with the microRusEfi stand alone ECU by clicking on the image below.
[![] (./images/thumb.jpg)](https://player.vimeo.com/video/1182912498)
<br>

This 'Tooth Eater' project allows you to run the bike, without having to get into the top end and remove the teeth off the cam trigger wheel. Instead, this small PCB and its associated firmware digitally removes 'eats' the two teeth, leaving one behind to be processed by your stand alone unit. Therefore, your stand alone ECU will only see a single cam pulse (home position) instead of three every cam revolution.

This Tooth Eater module performs the following tasks:<BR>
<table border="1">

<tr> 
<td width="5%">
<strong>(1)</strong>
</td>
<td width="95%">
Converts the CBR's 3-spoke cam pattern into a single digital pulse, making it compatable with other standalone ecu systems such as speeduino, rusefi, etc.
</td>
</tr>

<tr>
<td width="5%">
<strong>(2)</strong>
</td>
<td width="95%">
Houses an on-board VR conditioner. This unit is a direct plug in unit as is used on speeduino boards and it plugs straight into the tooth eater board.
</td>
</tr>

<tr>
<td width="5%">
<strong>(3)</strong>
</td>
<td width="95%">
On engine startup, it must 'SYNC' to the reference tooth (shown in red in the above image). The Tooth Eater will inhibit any output until engine SYNC has occured. Once SYNC has occured, the Tooth Eater will release both the CRANK and CAM signals to the stand alone ECU for further processing.
</td>
</tr>


</table>


