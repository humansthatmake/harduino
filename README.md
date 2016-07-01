0.0 - THE HARDUINO
</strong></h3>
<p style="text-align: left;">Harduino is an Arduino Compatible Input/Output Board that uses the same micro controller as most Arduino boards, the <a href="http://www.atmel.com/images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet_Complete.pdf" target="_blank">ATmega328P</a>.</p>

<h4><strong>0.1 - DESIGN FILES</strong></h4>
<p style="text-align: left;">The design files are freely available at GitHub and you can both download or fork the project if you want to contribute.</p>
<p style="text-align: left;"><a href="http://open3dge.com/wp-content/uploads/2015/06/schematic.png"><img class="aligncenter size-large wp-image-6689" src="http://open3dge.com/wp-content/uploads/2015/06/schematic-1024x445.png" alt="schematic" width="1024" height="445" /></a></p>
<p style="text-align: center;">[kleo_button title="HARDUINO DESIGNS" href="https://github.com/humansthatmake/harduino" style="default" size="lg" icon="github-circled"]</p>

<h4><strong>0.2 - BILL OF MATERIALS</strong></h4>
<iframe src="https://docs.google.com/spreadsheets/d/1ibOElA56LUYQ1zGwwcC5avGWMOkidIsuDOuW23gPkVk/pubhtml?gid=0&amp;single=true&amp;widget=true&amp;headers=false" width="700" height="340"></iframe>

<h3><strong>1.0 - FLASHING THE BOOTLOADER
</strong></h3>
The first step for putting your board to work is to download and install the Arduino IDE. Then connect your board to the computer using an FTDI breakout or cable.
Identify the Atmega328 microcontroller on your board by going to <code>Tools&gt;Board&gt;Arduino Pro or Pro Mini</code> and choose the Serial Port your board is connected to <code>Tools&gt;Serial Port&gt;ttyUSB#</code>

<a href="http://open3dge.com/wp-content/uploads/2015/06/propromini.png"><img class="aligncenter size-full wp-image-6678" src="http://open3dge.com/wp-content/uploads/2015/06/propromini.png" alt="propromini" width="716" height="720" /></a>

Then press <code>Tools&gt;Burn Bootloader</code>

If you've been successful with this step you can move forward to the PROGRAMMING chapter.
If you are getting errors while burning please check the TROUBLESHOOTING section at the bottom.
<h3><strong>2.0 - PROGRAMMING THE BOARD
</strong></h3>
For programing your new Harduino board using the Arduino IDE you can start by writing or loading your own code first.
Here we'll use the "Blink" example just for demonstration purposes.
<pre>void setup() {
pinMode(13, OUTPUT);
}

void loop() {
digitalWrite(13, HIGH);
delay(1000);
digitalWrite(13, LOW);
delay(1000);
}</pre>
On it, you'll see a reference to the pin 13. That will be the output pin to make your led blink. But this pin refers to the official Arduino board pinout that does not match with the real pin number on the Atmega microcontroller.
So we've developped an easy to understand pin mapping where you can see the pin number you need to write on your code in blue and the real Atmega pinout in black inside the microcontroller drawing.

<a href="http://open3dge.com/wp-content/uploads/2015/06/fabkit_arduino-1.png"><img class="aligncenter wp-image-6357" src="http://open3dge.com/wp-content/uploads/2015/06/fabkit_arduino-1-1024x966.png" alt="" width="600" height="566" /></a>Now, whenever you type a pin number in the Arduino IDE you just need to check this graphic so you can confirm if it matches with the pin you're working on.
In this "blink" case, the pin 13 will be the microcontroller pin 17, so you need to add your led to the Atmega pin 17 on your Harduino.
By the way, this pin already has an embeded smd led on our board, so you don't need to add anything here.

Then you need to identify your microcontroller by going to <code>Tools&gt;Board&gt;Arduino Pro or Pro Mini</code>, choose your Serial Port <code>Tools&gt;Serial Port&gt;ttyUSB#</code> and hit <code>upload</code>.

Your sketch will be promptly uploaded and the code executed by your board.
<h3><strong>3.0 - TROUBLESHOOTING</strong></h3>
<h4><strong>3.1 - EXPECTED SIGNATURE ERROR
</strong></h4>
<a href="http://open3dge.com/wp-content/uploads/2015/06/expected_signature1.jpg"><img class="aligncenter wp-image-5538 size-full" src="http://open3dge.com/wp-content/uploads/2015/06/expected_signature1.jpg" alt="expected_signature" width="498" height="170" /></a>

This is a relatively common error, and happens due to the fact that there are a few different versions of the ATMega328, such as <i>328P AU</i> and <i>328 AU</i>. They are almost identical and 100% interchangeable but carry different signatures.

The Arduino IDE is only prepared for their products, which means that if you use a slightly different component, the configurations might not match.
<div data-canvas-width="383.45834000000013">So when your component doesn't work as it should, the best idea is always to read its datasheet and see if there's something missing.</div>
<div data-canvas-width="383.45834000000013">And that's what we're going to do. If you make a quick search (Ctrl+F) on the <a href="http://www.atmel.com/images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet_Complete.pdf" target="_blank">ATmega328 datasheet</a> with the keyword <em>"signature"</em> and after some occurrences you'll see the following excerpt:</div>
<div data-canvas-width="383.45834000000013"></div>
<div data-canvas-width="383.45834000000013">
<blockquote>
<div data-canvas-width="792.3777599999999"><em>"All Atmel microcontrollers have a three-byte signature code which identifies the device. This code can be read in both serial and parallel mode, also when the device is locked. The three bytes reside in a separate address</em></div>
<div><em>space. For the ATmega48A/PA/88A/PA/168A/PA/328/P the signature bytes are given in Table 28-10."</em></div></blockquote>
</div>
And here is the 28-10 Table:
<div data-canvas-width="383.45834000000013"><a href="http://open3dge.com/wp-content/uploads/2015/06/signature_bytes.png"><img class="aligncenter wp-image-6019 size-full" src="http://open3dge.com/wp-content/uploads/2015/06/signature_bytes.png" alt="" width="736" height="305" /></a></div>
<div data-canvas-width="383.45834000000013"></div>
<div data-canvas-width="383.45834000000013"></div>
<div data-canvas-width="383.45834000000013">As you can see the ATmega328 and the ATmega328P have different <em>"signatures" and the boards under tools on your Arduino IDE are only configured for the 328"P". But <a href="https://learn.adafruit.com/usbtinyisp/avrdude">AVRdude</a>, the compiler underneath the IDE, is obviously ready to accept the 328 "non P" micro controller.
</em></div>
<div data-canvas-width="383.45834000000013">So you just need to tell the IDE that there is another micro controller on the AVRdude library called <em>"ATmega328" </em>that you want to use.</div>
<div data-canvas-width="383.45834000000013"></div>
<div data-canvas-width="383.45834000000013">And how do you do it? It's easy...</div>
<div data-canvas-width="383.45834000000013">Go to:</div>
<code>cd /usr/share/arduino/hardware/arduino
sudo sublime boards.txt</code>

Duplicate the standard entry format from Arduino Uno to the top of the file. Then change the following entries:

<code>uno.name= FabKit w/ATmega328 non P
uno.build.mcu=atmega328</code>

<a href="http://open3dge.com/wp-content/uploads/2015/06/config_boards.png"><img class="aligncenter wp-image-6022 size-full" src="http://open3dge.com/wp-content/uploads/2015/06/config_boards.png" alt="" width="1005" height="739" /></a>
Save the file and open your Arduino IDE again.
You'll see the new board added under tools&gt;board.

...........missing image.......

Now you can flash the bootloader properly by going to <code>Tools&gt;Burn Bootloader</code> again and you should be successfull.
