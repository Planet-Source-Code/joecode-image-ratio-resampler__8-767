<div align="center">

## Image ratio resampler


</div>

### Description

Resamples an uploaded image to 75% jpeg, without changing the ratio! If x and y size is equal, the image will be [100px]*[100px]. If x is bigger than y, the image will be [150px or less] * [100px]. If y is bigger than x, the image will be [100px] * [150px or less].
 
### More Info
 
One uploaded jpeg file.

Nothing, it send the image back to the uploaded temp file for later use.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[JoeCode](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/joecode.md)
**Level**          |Intermediate
**User Rating**    |4.5 (18 globes from 4 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Graphics/ Sound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics-sound__8-15.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/joecode-image-ratio-resampler__8-767/archive/master.zip)





### Source Code

```
	$UploadedFile = $_FILES['fileupload']['tmp_name'];
	$Quality = 75;
	$CurrentX = imagesx($UploadedImage);
	$CurrentY = imagesy($UploadedImage);
	if($CurrentX >= $CurrentY) {
		$MaxX = 150;
		$MaxY = 100;
		$NewX = $MaxX;
		$NewY = $CurrentY/($CurrentX/$MaxX);
		if($NewY > $MaxY) {
			$NewY = $MaxY;
			$NewX = $CurrentX/($CurrentY/$MaxY);
		}
	} else {
		$MaxX = 100;
		$MaxY = 150;
		$NewY = $MaxY;
		$NewX = $CurrentX/($CurrentY/$MaxY);
		if($NewX > $MaxX) {
			$NewX = $MaxX;
			$NewY = $CurrentY/($CurrentX/$MaxX);
		}
	}
	$im = imagecreatetruecolor($NewX, $NewY);
	imagecopyresampled($im, $UploadedImage, 0, 0, 0, 0, $NewX, $NewY, $CurrentX, $CurrentY);
	imagejpeg($im, $_FILES['fileupload']['tmp_name'], $Quality);
```

