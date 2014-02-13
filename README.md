Progressive Image Loader
======================

A Progressive Image loader javascript class. Originally created by Hinderling Volkart AG. With a few tweaks made for my specific needs of a more obsessive asset nullification system.

###Usage:

```
    //path, numImages, opts
    var imgLoader = new ProgressiveImageSequence("path/to/directory/frame-{index}.jpg", 3221, {
        indexSize : 6,// makes your filename to load path/to/directory/frame-000001 always 6 digits
        initialStep : 64, // starts at every 64th img then every 32nd img, then every 16th img etc. ALWAYS a power of 2
        onProgress : onImgLoaderProgress, //function to fire when an image loads
        onComplete : onImgLoaderComplete, // function to fire when loading completes
        stopAt : 1,//when to stop loading, 1 will be the last image
        loadDelay : CSSTransformSupport ? 5 : 50 //milliseconds to wait before loading next image in the load loop
    });

    //when ready to start loading
    var loadStartPosition = loadCounterForIE = 0;
    imgLoader.loadPosition(loadStartPosition, function(){
        //because sometimes IE will fire this multiple times I added this to make sure it fires once
        loadCounterForIE++;
        if(loadCounterForIE == 1)
            imgLoader.load();//start the loading progress
    }):

```

###Useful Methods

You can obviously call any method that is under the `this` name space (`this.whatever()`) but i find these few have been useful for me

```
    imgLoader.getNumLoaded(); //returns the number of images loaded
    imgLoader.getLoadProgress(): // returns load progress (0-100%)
    imgLoader.loadPosition(position); //loads an image at a certain position through the sequence
    imgLoader.getAt(index);// returns an image at a specific index
    imgLoader.reset();//resets loading back to initial state
    imgLoader.stop();// stop loading and leave the loaded stuff as is
    imgLoader.stopLoading();// added by me, stops loading, removes event listener references and unloads all images, setting those to null.
```

