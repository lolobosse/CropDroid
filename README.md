CropDroid
=========================

Android crop image library. Modified from https://github.com/biokys/cropimage and remove some warnings.

Call this method to run CropImage activity
```java
private void runCropImage() {

    // create explicit intent
    Intent intent = new Intent(this, CropImage.class);
    
    // tell CropImage activity to look for image to crop 
    String filePath = ...;
    intent.putExtra(CropImage.IMAGE_PATH, filePath);
    
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

            String path = data.getStringExtra(CropImage.IMAGE_PATH);
            
            // if nothing received
            if (path == null) {

                return;
            }

            // cropped bitmap
            Bitmap bitmap = BitmapFactory.decodeFile(mFileTemp.getPath());
            
            break;
    }
    super.onActivityResult(requestCode, resultCode, data);
}
```