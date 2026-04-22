# Tooth Eater Module

Some early 2000's Honda CBR models use a 3-spoke cam trigger wheel. Some examples are the Honda Blackbird CBR1100XX, CBR600 and Honda Aquatrax jet ski. Other models may also use this pattern as well.

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

 While this 3-spoke pattern is designed to work with the OEM Keihin ECU, it will not work with many stand alone ECU's. Most 'off the shelf' stand alone ECU systems such as Speeduino, RusEFI and others will cater for a single tooth pulse from the camshaft without fuss since this is a very standard configuration. In the past this issue is usually worked around by physically removing two teeth from the original cam trigger wheel (by grinding or hack-saw), leaving one behind. This works for a stand alone unit, but then renders the Keihin unit inoperative since it expects the 3 teeth.

You can watch the tooth eater in action working together with the microRusEfi stand alone ECU by clicking on the image below.
[![Watch the video](./images/thumb.jpg)](https://vimeo.com/reviews/9667708b-47c5-4177-8223-fa850c1e370e/videos/1182912498)
<br>

This 'Tooth Eater' project allows you to run the bike without having to get into the top end and remove the teeth off the exhaust camshaft trigger wheel. Instead, this small PCB and its associated firmware digitally removes 'eats' the two teeth, leaving one behind to be processed by your stand alone unit. With this unit, your stand alone ECU will only see a single cam pulse (home position) instead of three pulses every cam revolution. This should allow the Blackbird and other CBR models with the same cam wheel to be run with many of the available ECU systems on the market.

This Tooth Eater module performs the following tasks:<BR>

<table border="1">

<tr> 
<td width="5%">
<strong>(1)</strong>
</td>
<td width="95%">
Converts the CBR's 3-spoke cam pattern into a single digital pulse making it compatible with other standalone ecu systems such as speeduino, rusefi, etc.
</td>
</tr>

<tr>
<td width="5%">
<strong>(2)</strong>
</td>
<td width="95%">
Houses an on-board VR conditioner. This unit is a direct plug in module as used on Speeduino boards and it plugs straight into the tooth eater board (as seen in the image above). The Blackbird and other CBR's models require the VR module since they use inductive pickups on both the crank and the cam. The VR module converts the direct signal from the inductive pickups into a 0-5v TTL signal making it compatible with the stand alone ECU.
</td>
</tr>

<tr>
<td width="5%">
<strong>(3)</strong>
</td>
<td width="95%">
On engine startup the tooth eater must 'SYNC' to the reference tooth (shown in red in the above image). it is critical that this tooth is always selected by the firmware on engine start since the ECU will be also synced to it. The Tooth Eater will inhibit any output until engine SYNC has occurred. Once SYNC has occured, the tooth eater will 'release' both the CRANK and CAM signals to the stand alone ECU for further processing. This is to make for a clean transition ensuring that the ECU recieves crisp signals.
</td>
</tr>

</table>

<br>
# Principles of Operation

The tooth eater appears to deals with 'teeth' or pulses, however in reality it is only the rising or falling edges of that pulse that is relevant to the downstream ECU. The ECU deals only with edges and when it receives them, the ECU internally fires an interrupt service routine (ISR) that will update the crank and/or cam position in real time. All ECU's work with edges.

The early 2000's CBRs have a 12 tooth crank trigger wheel. The teeth are exactly spaced as the hours on a watch. The cam trigger wheel is as shown below. The tooth highlighted in red is the SYNC tooth as mentioned. I also refer to this tooth as the 'First Paired', since it is adjacent to its neighbour tooth that I refer to the 'Second Paired'. The remaining opposite tooth I refer to as the 'Isolated' tooth. Once SYNCED, the firmware inhibits the 'Second Paired' and 'Isolated' tooth and only allows the 'First Paired' to pass through. It does this continually as the engine is running, however in most cases the ECU is only interested in the initial startup then manages its own cam sync internally. Once SYNCED, the crank signal is allowed to 'pass-through' to the ECU via the VR conditioner. When the engine is running the crank signal is not processed by the tooth eater, however it is briefly used at engine startup to gain the SYNC. In a worst case scenario, SYNC should be attained in no more than 2 camshaft revolutions or 4 crank revolutions. Both cam and crank signals are used to gain initial sync.



<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 50%;"
    src="./images/SyncedCamTooth.png#center">
</img>

