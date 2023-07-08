# KenwoodBootScreen
Thesea are my notes for adding a custom boot/start screen to the Kenwood DMX706S. This should work for newer Kenwoods like the DMX706S, however, ymmv.

#### 1) Creating the image (These steps will work for any head unit)

- **Find an image you like**  
  In general, the image should be the same resolution or greater than the pixel count of the headunit as scaling up or enlarging an image up leads to poor image quality and pixelization. For example, the Kenwood DMX706S has a screen resolution of 800 x 480 and the image I used was 1280 x 720.

- Correct the aspect ratio so the image isn't stretched.
  Computer screens are typically square pixels, however, headunits may not be. This can be seen in the aspect ratio of the screen vs the aspect ratio of the screen resolution. For example, the Kenwood DMX706S has a screen resolution of 800 x 480 (width x height). Divide 800 by 480 to get an aspect ration of 1.66. However, the screen size as stated in the manual is 156.6mm x 81.6mm. I'm using mm here instead of inches for simplicity; the ratio will be the same with mm or inches. Divide 156.6 by 81.6 and we get an aspect ratio of 1.92. This means the image will need to be wider than 800 pixels. I'm focusing on width here because, in my case, the height was correct and the width was stretched, so I can keep the height at 480 and only need to adjust the width. Multiply 480 by 1.92 to get a new width of 922 pixels wide. We'll use this when we scale the image.

- Scale the image
  I used GIMP, a free image program. You may need to account for differences in your image program. My original image was 1280 x 720 (width x height). To scale it to the proper height, ensure height and width scaling are locked and change the height to 480 pixels. Doing this scaled my image to 853 x 480. Next, we need to make the image 922 pixels wide. Don't scale it or the image will be stretched. Instead, increase the width of the "canvas" to 922. GIMP gives me the option to centering and filling in the new empty side space with a color. My image background was black so I filled the new empty edges with black. You may need to clone the edges of your image to extend the background. Now that the image is 922 x 480 (width x height), the last step is to scale the width back to 800 pixels wide. Remember the headunit only has 800 pixels across so we need to squish the image. This time unlock width and height scaling so we can scale the width without changing the height. Scale the width to 800. The result should be an 800 x 480 image that looks a bit squished. Don't worry because the wider pixels on the headunit will stretch it back to normal.  
  
#### 2) Uploading the files (Kenwood specific)

- Prepping the files and USB drive
  The DMX706S requires a 16bit bitmap (.bmp) file and the image needs the setting for R5 G6 B5 enabled. In GIMP, export the file as a bitmap named image1.bmp and enable 16bit R5 G6 B5 under "Advanced Options". You'll also need a text file that tells the DMX706S to use the image file. I used the text file from comments section of this youtube video: https://youtu.be/FS9KdDIyl2o

OpeningCustomize.txt
```
Opening Customize
[FILE]image1.bmp
[VERSION]9876
~END
```

- Use a fat32 formatted USB drive. I don't think it matters if other files are on the drive, but I only had the two files when I did this: `image1.bmp` and `OpeningCustomize.txt`

- Put the DMX706S in `StandBy`. Then tap top left corner twice, bottom left corner twice, top left corner once, bottom left corner once. A secret "Customize Menu" should open. Select `Opening Customize`. The screen should turn blue meaning it worked (or red meaining it didn't, never got red screen). Power off the headunit, then power back on and you should have a custom startup screen that isn't stretched. If you want to revert to the Kenwood defaul start screen, open the OpeningCustomize.txt file, change the Version line to `0000` and do the StandBy/screen taps.

