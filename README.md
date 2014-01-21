CropDroid
=========================

Android crop image library. Modified from https://github.com/biokys/cropimage and remove some warnings.

Call this method to run CropImage activity
```java
private void runCropImage() {

    // create explicit intent
    Intent intent = new Intent(this, CropImage.class);
    
    // tell CropImage activity to look for image to crop 
    String URI = ...;
    intent.putExtra(CropImage.IMAGE_URI, URI.toString());
    
    // allow CropImage activity to rescale image
    intent.putExtra(CropImage.SCALE, true);
    
    // if the aspect ratio is fixed to ratio 3/2
    intent.putExtra(CropImage.ASPECT_X, 3);
    intent.putExtra(CropImage.ASPECT_Y, 2);
    
    // start activity CropImage with certain request code and listen
    // for result
    startActivityForResult(intent, REQUEST_CODE_CROP_IMAGE);
}
```

Waiting for result
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {

    if (resultCode != RESULT_OK) {

        return;
    }  

    switch (requestCode) {

        case REQUEST_CODE_CROP_IMAGE:

            String uri = data.getStringExtra(CropImage.IMAGE_URI);
            
            // if nothing received
            if (uri == null) {

                return;
            }

            // cropped bitmap
            Bitmap b = MediaStore.Images.Media.getBitmap(this.getContentResolver(), Uri.parse(uri);
            
            break;
    }
    super.onActivityResult(requestCode, resultCode, data);
}
```
