# Release notes

## 1.7.0
- utilize Camera2 API on devices that support it to achieve much better frame grabbing performance
- new algorithm for determining which video frame is of good enough quality to be processed - it uses much less memory than last one and works in separate thread so it does not impact image recognition thread
	- this results in much better and faster scanning performance
- support for [defining camera metering areas](https://blinkid.github.io/blinkid-android/com/microblink/view/BaseCameraView.html#setMeteringAreas(com.microblink.geometry.Rectangle[])) that will camera use to perform focus, exposure and white balance measurement.
- support for obtaining raw MRZ text even if our internal parser fails to parse it
	- in order to do that, you must [enable returning of unparsed MRTD results](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognizerSettings.html#setAllowUnparsedResults(boolean))
	- when obtaining [MRTD recognition result](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognitionResult.html), you should check if [MRZ was parsed](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognitionResult.html#isMRZParsed())
		- if MRZ was parsed, you can obtain parsed data as ususal
		- if MRZ was not parsed, you can obtain [raw OCR result](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognitionResult.html#getOcrResult()) and parse it yourself
- added support for Visa MRZ format in internal MRZ parser
- support for obtaining image of [MRZ zone](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognizerSettings.html#setShowMRZ(boolean)) and [full document image](https://blinkid.github.io/blinkid-android/com/microblink/recognizers/ocr/mrtd/MRTDRecognizerSettings.html#setShowFullDocument(boolean)) via [ImageListener](https://blinkid.github.io/blinkid-android/com/microblink/image/ImageListener.html)
- bitmaps can now be processed while [RecognizerView](https://blinkid.github.io/blinkid-android/com/microblink/view/recognition/RecognizerView.html) is active using method [recognizeBitmap](https://blinkid.github.io/blinkid-android/com/microblink/view/recognition/RecognizerView.html#recognizeBitmap(android.graphics.Bitmap, com.microblink.hardware.orientation.Orientation, com.microblink.view.recognition.ScanResultListener))
- removed method `resumeScanningWithoutStateReset` - method [resumeScanning](https://blinkid.github.io/blinkid-android/com/microblink/view/recognition/RecognizerView.html#resumeScanning(boolean)) of [RecognizerView](https://blinkid.github.io/blinkid-android/com/microblink/view/recognition/RecognizerView.html) now receives `boolean` indicating whether internal state should be reset
- by default, null quiet zone is now set to `true` in US Driver's License recognizer

## 1.6.0
- removed support for ARMv5 and ARMv6 processors (armeabi) because of their very poor scanning performance
- optimized MRZ text extraction algorithm - 0-O confusion now does not cause extremely long processing that resulted in freezing the device
- updated documentation with use cases for which BlinkID is applicable
- fixed crash in DirectAPI when recognizer was terminated in the middle of recognition process

## 1.5.0
- support for defining camera aspect mode via intent
- removed autoscale setting from USDL recognizer - autoscale is now always used
- added MRZ detector to MRTD recognizer - Machine Readable Zone location can now be detected almost everywhere on the image

## 1.4.0
- added support for defining region for scanning MRZ
- added support for scanning UK Driver's Licence, check [README](Readme.md) for details
- improved parsing of MRZ (Machine Readable Zones)
- support for defining camera zoom level
- fixed NPE when null SuccessCallback was given

## 1.3.1
- Improved parsing of some problematic US Driver's Licence barcodes

## 1.3.0
- Added support for non-standard issuing authorities

## 1.2.0
- added support for US Driver's Licence barcode scanning
- introduced new licence key format which is now mandatory (generate your free licence key on [https://microblink.com/login](https://microblink.com/login) or contact us at [http://help.microblink.com](http://help.microblink.com)

## 1.1.0
- added support for obtaining complete unparsed MRZ lines
- fixed crash on Motorola Lex755 and Sony Xperia Z

## 1.0.1
- Support for two-letter country codes

## 1.0.0
- Support for MRZ formats in passports and ID cards
- Support for integration via Maven
- Documentation update

## 0.6.0
- Scanning support for MRZ formats