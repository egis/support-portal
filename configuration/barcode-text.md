# Barcode Recognition Setup

1) Setup an extractFromBarcode rule on the appropriate node  
2) Install the Softek SDK. You can download the latest version from:  
[Windows SDK
v8.1.2](http://softeksoftware.co.uk/download/barcode_sdk/windows/softek_barcode_sdk_8_1_2.zip)  
 [Linux SDK v8.3.1](http://bardecode.com/barcode_linux.tar.gz)
 
For a list of all versions go to [Bardecode](http://www.bardecode.com/en1/quick-download/), although a different license may need to be loaded via the License property. A license can be specified in the "Advanced" section of the extractFromBarcode rule by adding the line `LicenseKey=<license here>`<br>
`xml=/opt/PT_ID_NO.xml`
 
 Linux: Copy the barcode_linux.tar.gz file to the destination host
Run the following commands:<br>
`gzip -d barcode_linux.tar.gz`<br>
`tar -xf barcode_linux.tar`<br>
In the resultant bardecoder_8_3_1 directory, `sudo ./configure.sh`

Libraries need to be copied to `/usr/lib/` on Linux installations and `C:\\Windows\\System32` for Windows (this is dependant on where the java.library.path is pointing to). Below is a list of the libraries which need to be copied:

*  java/Softek/Barcode.class
*  java/Softek/Barcode.java
*  lib/bardecode.a
*  lib/libbardecode.so
*  lib/libbardecode_jni.so

An XML file in the following format can be created to configure specific properties:
```
<xml version='1.0' encoding='iso-8859-1'>
        <SoftekBarcode>
                <Properties>
                        <AllowDuplicateValues>1</AllowDuplicateValues>
                        <BarcodesAtTopOfPage>0</BarcodesAtTopOfPage>
                        <BitmapResolution>200</BitmapResolution>
                        <CodabarMaxVariance>20</CodabarMaxVariance>
                        <Code128Lenient>0</Code128Lenient>
                        <Code25Checksum>0</Code25Checksum>
                        <Code25MinOccurrenceLength>5</Code25MinOccurrenceLength>
                        <Code39Checksum>0</Code39Checksum>
                        <Code39MaxRatioPcnt>0</Code39MaxRatioPcnt>
                        <Code39NeedStartStop>1</Code39NeedStartStop>
                        <ColorChunks>1</ColorChunks>
                        <ColorProcessingLevel>2</ColorProcessingLevel>
                        <ColorThreshold>0</ColorThreshold>
                        <ConvertUPCEToEAN13>1</ConvertUPCEToEAN13>
                        <DataMatrixAutoUTF8>1</DataMatrixAutoUTF8>
                        <DataMatrixFinderGapTolerance>6</DataMatrixFinderGapTolerance>
                        <Despeckle>0</Despeckle>
                        <Encoding>3</Encoding>
                        <ErrorCorrection>0</ErrorCorrection>
                        <ExtendedCode39>1</ExtendedCode39>
                        <FastScanLineJump>25</FastScanLineJump>
                        <FixedLengthCode25>0</FixedLengthCode25>
                        <GammaCorrection>100</GammaCorrection>
                        <LineJump>1</LineJump>
                        <MaxBarcodesPerPage>0</MaxBarcodesPerPage>
                        <MaxLength>999</MaxLength>
                        <MaxThreads>0</MaxThreads>
                        <MedianFilter>0</MedianFilter>
                        <MedianFilterLevel>1</MedianFilterLevel>
                        <MedianFilterBias>5</MedianFilterBias>
                        <MinSeparation>180</MinSeparation>
                        <MinLength>4</MinLength>
                        <MinOccurrence>2</MinOccurrence>
                        <MinResyncs>3</MinResyncs>
                        <MinSpaceBarWidth>0</MinSpaceBarWidth>
                        <MinThresholdDiff>30</MinThresholdDiff>
                        <MultipleRead>1</MultipleRead>
                        <NoiseReduction>0</NoiseReduction>
                        <PageNo>1</PageNo>
                        <PatchCodeMinOccurrence>30</PatchCodeMinOccurrence>
                        <Pattern></Pattern>
                        <Pdf417AutoUTF8>1</Pdf417AutoUTF8>
                        <Pdf417Debug>0</Pdf417Debug>
                        <Pdf417ChannelMode>0</Pdf417ChannelMode>
                        <PDF417MacroEscapeBackslash>1</PDF417MacroEscapeBackslash>
                        <PdfBpp>8</PdfBpp>
                        <PdfDpi>300</PdfDpi>
                        <PdfImageExtractOptions>0</PdfImageExtractOptions>
                        <PdfImageOnly>1</PdfImageOnly>
                        <PdfImageRasterOptions>0</PdfImageRasterOptions>
                        <PdfMaxMem>32</PdfMaxMem>
                        <Photometric>0</Photometric>
                        <PrefOccurrence>5</PrefOccurrence>
                        <QRCodeAutoUTF8>1</QRCodeAutoUTF8>
                        <QRCodeBWAutoMedianFilter>1</QRCodeBWAutoMedianFilter>
                        <QRCodeFinderTolerance>0</QRCodeFinderTolerance>
                        <QuietZoneSize>0</QuietZoneSize>
                        <QuotedPrintableCharSet>0</QuotedPrintableCharSet>
                        <QRCodeReadInverted>1</QRCodeReadInverted>
                        <ReadCodabar>1</ReadCodabar>
                        <ReadCode128>1</ReadCode128>
                        <ReadCode25ni>1</ReadCode25ni>
                        <ReadCode25>1</ReadCode25>
                        <ReadCode39>1</ReadCode39>
                        <ReadCode93>1</ReadCode93>
                        <ReadDatabar>1</ReadDatabar>
                        <ReadDataMatrix>0</ReadDataMatrix>
                        <ReadEAN8>1</ReadEAN8>
                        <ReadEAN13>1</ReadEAN13>
                        <ReadMicroPDF417>1</ReadMicroPDF417>
                        <ReadNumeric>1</ReadNumeric>
                        <ReadPatchCodes>1</ReadPatchCodes>
                        <ReadPDF417>1</ReadPDF417>
                        <ReadQRCode>1</ReadQRCode>
                        <ReadShortCode128>1</ReadShortCode128>
                        <ReadUPCA>1</ReadUPCA>
                        <ReadUPCE>1</ReadUPCE>
                        <ReportUnreadBarcodes>0</ReportUnreadBarcodes>
                        <RotateBy45IfNoBarcode>0</RotateBy45IfNoBarcode>
                        <SkewedLinear>1</SkewedLinear>
                        <ResyncChars>2</ResyncChars>
                        <ResyncRows>10</ResyncRows>
                        <ScanDirection>15</ScanDirection>
                        <ShortCode128MinLength>2</ShortCode128MinLength>
                        <SkewLineJump>9</SkewLineJump>
                        <SkewTolerance>0</SkewTolerance>
                        <ShowCheckDigit>0</ShowCheckDigit>
                        <ShowCodabarStartStop>1</ShowCodabarStartStop>
                        <SkewSpeed>3</SkewSpeed>
                        <TwoDTimeOutPcnt>80</TwoDTimeOutPcnt>
                        <TimeOut>30000</TimeOut>
                        <UseFastScan>1</UseFastScan>
                        <UseOldCode128Algorithm>0</UseOldCode128Algorithm>
                        <UseRunCache>1</UseRunCache>
                        <UseScaledFaxCoords>1</UseScaledFaxCoords>
                        <UseOverSampling>0</UseOverSampling>
                        <WeightLongerBarcodes>1</WeightLongerBarcodes>
                </Properties>
        </SoftekBarcode>
</xml>

```

### Supported Barcodes

*  Codabar also known as Code 2 of 7, Codeabar, Ames Code, NW-7 and Monarch (ReadCodabar)
*  Code 128 Symbol Sets A, B and C (ReadCode128)
*  Code 128 Short Format (ReadShortCode128)
*  Code 2 of 5 Datalogic (ReadCode25ni)
*  Code 2 of 5 Iata1 (ReadCode25ni)
*  Code 2 of 5 Iata2 (ReadCode25ni)
*  Code 2 of 5 Industrial (ReadCode25ni)
*  Code 2 of 5 Interleaved (ReadCode25)
*  Code 2 of 5 Matrix (ReadCode25ni)
*  Code 3 of 9 (ReadCode39)
*  Code 3 of 9 Extended (ReadCode39 and ExtendedCode39)
*  Code 93 (ReadCode93)
*  EAN-8, European Article Number/International Article Number (ReadEAN8)
*  EAN-13 and UPC-A, European Article Number/International Article Number (ReadEAN13)
*  GS1-128, UCC-128, EAN-128 (ReadCode128)
*  GS1-Databar (please see 2-D section below)
*  Patch Code Symbols (ReadPatchCodes)
*  UPC-A, Universal Product Code (ReadEAN13 and ReadUPCA)
*  UPC-E, Universal Product Code (ReadUPCE)
*  QR-Code (ReadQRCode)
*  Data Matrix ECC200 sizes 8x8 to 144x144 (ReadDataMatrix)
*  GS1-Databar
*  Micro-PDF-417 (ReadMicroPDF417)
*  PDF-417, Portable Data File (ReadPDF417)

Properties
----------

| Properties        | Description
| ------------- |-------------
| AllowDuplicateValues   | Barcodes containing the same text on the same page 
| BarcodesAtTopOfPage   | Search from the top of a page downwards
| Code128Lenient |  Relax some of the requirements for Code 128 barcodes
| Code25Checksum |  Code 25 barcodes include checksum character
| Code25MinLengthOccurrence |  Control for false positive readings for Code 25 barcodes
| Code39Checksum |  Code 39 barcodes include checksum character
| Code39MaxRatioPcnt |  Set the max ratio between the wide and narrow bars
| Code39NeedStartStop |  Require start and stop \* characters for a Code 39 barcode
| ColorProcessingLevel |  Control the amount of processing time spent reading barcode values from color images
| ColorThreshold |  Contrast setting for color images
| ConvertUPCEToEAN13 |  Output UPC-E barcodes in EAN-13 format
| DatabarOptions |  Set the advanced options for reading GS1 Databar barcodes
| DataMatrixAutoUTF8 |  Automatic detection of UTF8 data in Datamatrix barcodes
| Despeckle |  Clean up images containing specks of black and white
| Encoding |  Character encoding for barcode values
| ErrorCorrection |  Correct errors in barcodes
| ExtendedCode39 |  Read Code 39 barcodes in the extended symbol set
| GammaCorrection |  Gamma correction value for color images
| LicenseKey | Specify a new license key for Barcode engine
| LineJump|  Frequency of line sampling in an image
| MaxLength  |  Maximum string length of a barcode
| MaxRectOverlap  |  Maximum number of threads
| MaxThreads  |  Maximum overlap for bounding rectangles
| MedianFilter  |  Apply a median filter to the image
| MedianFilterBias  |  Lighten/darken an image during a median filter
| MinLength  |  Minimum string length of a barcode
| MinOccurrence  |  Minimum number of hits needed to read a barcode
| MinSeparation  |  Minimum distance between similar barcodes
| MinSpaceBarWidth  |  Minimum width of a space in a barcode
| MultipleRead  |  Read more than one barcode
| NoiseReduction  |  Clean up images containing un-wanted black marks
| PageNo  |  Page number to scan in an image
| Pattern  |  Regular expression to search for
| PDF417AutoUTF8  |  Automatic identification of UTF8 data in PDF-417 barcodes
| Pdf417ChannelMode  |  Control the way macros are handled in PDF417 barcodes
| Pdf417MacroEscapeBackslash  |  Handling of back slash characters in PDF417 macros
| Photometric  |  Photometric interpretation for a black and white bitmap
| PrefOccurrence  |  Preferred number of hits for a barcode
| QRCodeAutoUTF8  |  Automatic identification of UTF8 data in QrCode barcodes
| QRCodeBWAutoMedianFilter  |  automatic use of median filter for QrCode detection
| QuietZoneSize  |  Size of quiet zone around a barcode
| ReadCodabar  |  Read Codabar barcodes
| ReadCode128  |  Read Code 128 barcodes
| ReadCode25  |  Read Code 25 (interlaced) barcodes
| ReadCode25ni  |  Read Code 25 (non-interlaced) barcodes
| ReadCode39  |  Read Code 39 barcodes
| ReadDatabar  |  Read GS1 Databar barcodes
| ReadDataMatrix  |  Read Data Matrix barcodes
| ReadEAN13  |  Read EAN-13 barcodes
| ReadEAN8  |  Read EAN-8 barcodes
| ReadMicroPDF417  |  Read micro-PDF-417 barcodes
| ReadNumeric  |  Only read numeric barcodes
| ReadPatchCodes  |  Read Patch Codes
| ReadPDF417 | Read PDF-417 barcodes
| ReadShortCode128  |  Read short Code 128 barcodes
| ReadUPCA  | Read UPC-A barcodes
| ReadUPCE  | Read UPC-E barcodes
| ReportUnreadBarcodes | Report barcodes that could not be decoded
| ScanDirection  |  Orientation to scan for a barcode
| ShortCode128MinLength  |  Minimum length for a barcode of type "SHORTCODE128"
| ShowCheckDigit  |  Display check digits
| SkewedDatamatrix  |  Check for skewed linear barcodes
| SkewedLinear  |  Check for skewed datamatrix barcodes
| SkewLineJump  |  Frequency of line sampling for skewed barcodes
| SkewTolerance  |  Search for barcodes at an angle to horizontal or vertical
| TifSplitMode  |  Controls how a TIF file should be split
| TifSplitPath  |  Split a TIF file into smaller parts based on the location of barcodes in the image
| TimeOut  |  Set a time out for barcode detection
| UseFastScan  |  Do a quick scan prior to a deeper search.
| UseOverSampling  |  Another method for cleaning up 'noisy' images
| WeightLongerBarcodes  |  Boost the hit count for longer barcodes.

