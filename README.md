# Adafruit GFX Library

This is the core graphics library for all our displays, providing a common set of graphics primitives (points, lines, circles, etc.). It needs to be paired with a hardware-specific library for each display device we carry (to handle the lower-level functions).

Adafruit invests time and resources providing this open source code, please support Adafruit and open-source hardware by purchasing products from Adafruit!

Written by Limor Fried/Ladyada for Adafruit Industries.
BSD license, check license.txt for more information.
All text above must be included in any redistribution.

Recent Arduino IDE releases include the Library Manager for easy installation. Otherwise, to download, click the DOWNLOAD ZIP button, uncompress and rename the uncompressed folder Adafruit_GFX. Confirm that the Adafruit_GFX folder contains Adafruit_GFX.cpp and Adafruit_GFX.h. Place the Adafruit_GFX library folder your <arduinosketchfolder>/Libraries/ folder. You may need to create the Libraries subfolder if its your first library. Restart the IDE.

# Useful Resources

- Image2Code: This is a handy Java GUI utility to convert a BMP file into the array code necessary to display the image with the drawBitmap function. Check out the code at ehubin's GitHub repository: https://github.com/ehubin/Adafruit-GFX-Library/tree/master/Img2Code

- drawXBitmap function: You can use the GIMP photo editor to save a .xbm file and use the array saved in the file to draw a bitmap with the drawXBitmap function. See the pull request here for more details: https://github.com/adafruit/Adafruit-GFX-Library/pull/31

- 'Fonts' folder contains bitmap fonts for use with recent (1.1 and later) Adafruit_GFX. To use a font in your Arduino sketch, #include the corresponding .h file and pass address of GFXfont struct to setFont(). Pass NULL to revert to 'classic' fixed-space bitmap font.

- 'fontconvert' folder contains a command-line tool for converting TTF fonts to Adafruit_GFX .h format.

---
# What is this Fork?

This is a fork which adds the function `write16(uint16_t)` which allows users to initiate extremely fast mass SPI transfers for RGB displays. I made this fork to be able to quickly transfer a RAM buffer from an ESP8266 to a SSD1351. Here's an example for copying ram quickly to a display using `write16`.

```
  tft.startWrite();

  tft.setAddrWindow(0, 0, 128, 128);
  
  for (uint16_t i = 0; i < NUM_PIXELS; i++){
    tft.write16(buf[i]);
  }
  
  tft.endWrite();
```
The transfer takes approximately 40 ms (80MHz CPU, 16MHz SPI), as opposed to other methods which could take <100ms.
### Roadmap

The PRIME DIRECTIVE is to maintain backward compatibility with existing Arduino sketches -- many are hosted elsewhere and don't track changes here, some are in print and can never be changed! This "little" library has grown organically over time and sometimes we paint ourselves into a design corner and just have to live with it or add ungainly workarounds.

Highly unlikely to merge any changes for additional or incompatible font formats (see Prime Directive above). There are already two formats and the code is quite bloaty there as it is (this also creates liabilities for tools and documentation). If you *must* have a more sophisticated font format, consider creating a fork with the features required for your project. For similar reasons, also unlikely to add any more bitmap formats, it's getting messy.

Please don't reformat code for the sake of reformatting code. The resulting large "visual diff" makes it impossible to untangle actual bug fixes from merely rearranged lines.
