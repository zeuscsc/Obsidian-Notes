#### R-CNN

The R-CNN detector [2](https://www.mathworks.com/help/vision/ug/getting-started-with-r-cnn-fast-r-cnn-and-faster-r-cnn.html#mw_a9cdd2b3-b910-4d3d-90db-b485b415fd9b) first generates region proposals using an algorithm such as Edge Boxes[1](https://www.mathworks.com/help/vision/ug/getting-started-with-r-cnn-fast-r-cnn-and-faster-r-cnn.html#mw_cfbce1ef-74b2-46dd-814f-a0f985c96301). The proposal regions are cropped out of the image and resized. Then, the [[Convolutional Neural Network|CNN]] classifies the cropped and resized regions. Finally, the region proposal bounding boxes are refined by a support vector machine (SVM) that is trained using [[Convolutional Neural Network|CNN]] features.

Use the [`trainRCNNObjectDetector`](https://www.mathworks.com/help/vision/ref/trainrcnnobjectdetector.html) function to train an R-CNN object detector. The function returns an [`rcnnObjectDetector`](https://www.mathworks.com/help/vision/ref/rcnnobjectdetector.html) object that detects objects in an image.

![[Pasted image 20220816114646.png]]
R-CNN use [[Image segmentation]] to select reagions that may be object and then apply [[Convolutional Neural Network]] onto it.
![[Pasted image 20220816140843.png]]
