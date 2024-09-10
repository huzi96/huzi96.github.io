<link href="./retro.css" rel="stylesheet"></link>

## How to export 10-bit HDR HEIC (HEIF) pictures in Adobe Lightroom Classic

*Sep. 9 2024* 

By the time this article is written, the latest Adobe Lightroom (Lr) Classic only support exporting HDR photos to AVIF (AV1 Intra) and JPEG XL. Sadly these formats are not natively supported by Apple devices and Apps like Instagram.  This article describe a (but imperfect) method to export 10-bit HDR HEIC images from Adobe Lightroom Classic. This method has the following limitations:

1. The major difficulty to produce Apple device-compatible HEIC files is that it has some special container syntax for fast preview and decoding. Also there are too many color space to choose from. To overcome this issue, the core idea of this method is to call Apple's own API to encode HEIC, which guarantee compatibility. So here we need to run some Swift script calling a macOS API. That means you need a Mac to complete the following steps.
2. Although the produced HEIC can be viewed in correct color using Apple's Photo App, for 3rd-party Apps like Weibo and Instagram, the color space may not be correctly interpreted, resulting in over-exposed results in Weibo and not-fully-triggered HDR on Instagram (but works fine).


### Step 1: Export your 10-bit HDR image as a TIFF file

First make sure you turned on HDR for the pictures you processed with Lr. Then you need to export the pictures to TIFF images with 16-bit depth.

1. Select the image you want to export in Lightroom Classic.
2. Go to `File` > `Export` in the top menu.
3. In the Export dialog box, choose a location to save the exported file.
4. Choose `TIFF` from the `File Format` dropdown menu.
5. For color space, `HDR P3` works fine with me. You might want to try different ones.
6. Click `Export` to export the image as a TIFF file.

### Step 2: Convert the TIFF file to 10-bit HDR HEIC

You need a script to do this conversion.

1. Go to [https://github.com/milch/LRExportHEIC/releases](https://github.com/milch/LRExportHEIC/releases) and download ExportHEIC.lrplugin.zip. (Or you can download the source code and compile by yourself if you have Xcode.)
2. Unzip.
3. DO NOT install this extension (because the author didn't add HDR support in the panel but actually the API has support.). Right click `ExportHEIC.lrplugin` and choose `show package content`. In the opened folder, copy LRExportHEIC to a folder you like. This is the excutable you will need to execute in your terminal.
4. Relocate your working directory to the folder where you put `LRExportHEIC`.  Run the following command in your terminal, 
   ```./LRExportHEIC path_to_output.heic --input-file path_to_input.tif --quality 0.8```.

   For example,

   ```./LRExportHEIC DSC08951.heic --input-file DSC08951.tif --quality 0.8```.
   
   Choose your quality factor to tradeoff file size and quality. (No need to use 1.0. 0.8 should be visually lossless.)
5. Now you get your HEIC picture. Just feel free to delete the TIFF file.



If you have any questions or feedback, feel free to email me.

<[Back](welcome.html)>