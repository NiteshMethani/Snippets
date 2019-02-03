# Snippets
Code snippets for some CV/NLP/DL tasks.

* remove_whitespace_from_image.py <br/>
  -code to trim the extra whitespace in the bboxes
  Description of the code:
    We read in the image, but we also convert to grayscale as your image is in colour for some reason. The tricky part is the third line of code where I threshold below the intensity of 128 so that the dark text becomes white. This however produces a binary image, so I convert to uint8, then scale by 255. This essentially inverts the text.

    Next, given this image we find all of the non-zero coordinates with cv2.findNonZero and we finally put this into cv2.boundingRect which will give you the top-left corner of the bounding box as well as the width and height. We can finally use this to crop the image. Note we do this on the original image and not the inverted one. We use simply NumPy array indexing to do the cropping for us.

    Finally, we show the image to show that it works and we save it to disk.
    A good thing to do is to remove some of the right border and bottom border. We can do that by cropping the image down to that first. Next, this image contains some very small noisy pixels. I would recommend doing a morphological opening with a very small kernel, then redo the logic we talked about above.
    In short,
     invert the image so the black text becomes white, find all the non-zero points in the image then determine what the minimum spanning bounding box would be. You can use this bounding box to finally crop your image. Finding the contours is very expensive and it isn't needed here - especially since your text is axis-aligned. You can use a combination of cv2.findNonZero and cv2.boundingRect to do what you need.

    Therefore, something like this should work.

    Ref: https://stackoverflow.com/questions/49907382/how-to-remove-whitespace-from-an-image-in-opencv
