# Web Scan

For installing webscan see [End user installation](../installation/end-user-installation.md)  

Each user who useses webscan will need to be configured as a Webscan user type in **User Management -> Users**  

Web Scan is configured using JSON profiles stored in `System/scanning/profiles`  



## Web Scan Profile Settings

### separation

type - *string*

Possible values:

- **None** - combine all images to single PDF file;

- **Page** - put each image to new PDF file, so each PDF file will contain single page;

- **Blank** - create new PDF when blank image appeared. For instance, there is images sequence:

  ```
  image1, image2, blank image, image3, image4, image5, blank image, image6
  ```

  As a result of **Blank** separation, scan addon will return 3 PDF files: 2 pages (image1, image2), 3 pages (image3, image4, image5) and 1 page (image6).

- **Barcode** - create new PDF when image with unique barcode appeared. For instance, there is images sequence:

  ```
  image1, image with barcode1, image2, image3, image with barcode3
  ```

  As a result of **Blank** separation, scan addon will return 3 PDF files: 1 page (image1), 3 pages (image with barcode1, image2, image3) and 1 page (image with barcode3).

### resolution

type - *object*

Fields:

- **x** - integer, *x* value of resolution. Common possible values: 100 - 600

- **y** - integer, *y* value of resolution. Common possible values: 100 - 600

- *units* - string, measure units for *x* and *y*. Possible values:  

    * Inches  
    * Centimeters  
    * Points  
    * Pixels  
   
**Important note:** list of supported values for *resolution* may vary depending on scanner model
   
### compressionMode
   
type - *string*
   
Common values:
   
- **None** - don't use any compression mode;
- **Jpeg** - intended for the compression of color photographs
- **Lzw** - a compression licensed by UNISYS
- **Jbig** - intended for bi-tonal and grayscale document images
- **Png** - Portable Network Graphic
- **Group4** - CCITT Group 4 fax encoding, intended for document images

**Important note:** list of supported values for *compressionMode* may vary depending on scanner model

### pdfDecoder

type - *object*

Fields:

- **resolution** - integer, resolution at which to render a PDF page. Minimum - 1, maximum - 3600.

### barcodeSettings

type - *object*

See [Barcode Configuration](barcode-text.md) for list of supported properties

## Examples

Split images into PDF files by barcode and use 300x300px scan resolution

```
{
  "separation": "Barcode",
  "resolution": {
    "x": 300,
    "y": 300,
    "units": "Pixels"
  }
}
```

Create single PDF file from scanned images and render it with 80 resolution

```
{
  "separation": "None",
  "pdfDecoder": {
    "resolution": 80
  }
}
```
