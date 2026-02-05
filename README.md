<h2>TensorFlow-FlexUNet-Image-Segmentation-Prostate-MRI (2026/02/05)</h2>
Sarah T.  Arai<br>
Software Laboratory antillia.com<br><br>
This is the first experiment of Image Segmentation for <b>Prostate</b> based on our <a href="./src/TensorFlowFlexUNet.py">TensorFlowFlexUNet</a> 
(TensorFlow Flexible UNet Image Segmentation Model for Multiclass), 
and 
<a href="https://drive.google.com/file/d/1ha-8bNnWzvqOs7kiduYdjrYT-hb1_52t/view?usp=sharing">
<b>Augmented-Prostate-ImageMask-Dataset.zip</b></a> with colorized masks, which was derived by us from <br><br>
<a href="https://www.kaggle.com/datasets/haithem1999/prostate-annotated-dataset-for-image-segmentation">
<b>Prostate annotated dataset for image segmentation</b> </a> on the kaggle.com.
<br><br>
<b>Data Augmentation Strategy</b><br>
To address the limited size of images and masks of the original <b>Prostate </b> dataset,
we used our offline augmentation tool <a href="./generator/ImageMaskDatasetGenerator.py">ImageMaskDatasetGenerator.py</a> (please see also: 
<a href="https://github.com/sarah-antillia/Image-Deformation-Tool">Image-Deformation-Tool</a>)
 to generate our Augmented Prostate dataset.
<br><br> 
<hr>
<b>Actual Image Segmentation for Prostate Images of 512x512 pixels </b><br>
As shown below, the inferred masks predicted by our segmentation model trained by the dataset appear similar to the ground truth masks.
<br>
<b>rgb_map = {peripheral zone:red,  transitional zone:green}</b>
<br><br>
<table>
<tr>
<th>Input: image</th>
<th>Mask (ground_truth)</th>
<th>Prediction: inferred_mask</th>
</tr>
<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/102000_5.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/102000_5.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/102000_5.png" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/107000_10.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/107000_10.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/107000_10.png" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/barrdistorted_1001_0.3_0.3_104000_7.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/barrdistorted_1001_0.3_0.3_104000_7.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/barrdistorted_1001_0.3_0.3_104000_7.png" width="320" height="auto"></td>
</tr>
</table>
<hr>
<br>
<h3>1  Dataset Citation</h3>
The dataset used here was derived from <br><br>
<a href="https://www.kaggle.com/datasets/haithem1999/prostate-annotated-dataset-for-image-segmentation">
<b>Prostate annotated dataset for image segmentation</b>. </a>
<br><br>
<b>About Dataset</b><br>
<b>Content</b><br>
The prostate dataset consisted of 48 multi-parametric MRI studies provided by Radboud University (The Netherlands) reported in a previous segmentation study. <br>
Manual segmentation of the whole prostate from transverse T2-weighted scans 
with resolution 0.6 x 0.6 x 4 mm and the apparent diffusion coefficient (ADC) map (2 x 2 x 4 mm) was used.
<br><br>
<b>Citations</b><br>
<a href="https://arxiv.org/abs/1902.09063">A large annotated medical image dataset for the
development and evaluation of segmentation algorithms</a>
<br><br>
<b>License</b><br>
Unknown
<br>
<br>
<h3>
2 Prostate ImageMask Dataset
</h3>
 If you would like to train this Prostate Segmentation model by yourself,
please down load our dataset <a href="https://drive.google.com/file/d/1ha-8bNnWzvqOs7kiduYdjrYT-hb1_52t/view?usp=sharing">
<b>Augmented-Prostate-ImageMask-Dataset.zip</b>
</a> on the google drive,
expand the downloaded, and put it under <b>./dataset/</b> to be.
<pre>
./dataset
└─Prostate
    ├─test
    │   ├─images
    │   └─masks
    ├─train
    │   ├─images
    │   └─masks
    └─valid
        ├─images
        └─masks
</pre>
<br>
<b>Prostate Statistics</b><br>
<img src ="./projects/TensorFlowFlexUNet/Prostate/Prostate_Statistics.png" width="512" height="auto"><br>
<br>
As shown above, the number of images of train and valid datasets is large enough to use for a training set of our segmentation model.
<br><br>

<b>Train_images_sample</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/train_images_sample.png" width="1024" height="auto">
<br>
<b>Train_masks_sample</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/train_masks_sample.png" width="1024" height="auto">
<br>
<h3>
3 Train TensorflowFlexUNet Model
</h3>
 We trained Prostate TensorflowFlexUNet Model by using the following
<a href="./projects/TensorFlowFlexUNet/Prostate/train_eval_infer.config"> <b>train_eval_infer.config</b></a> file. <br>
Please move to ./projects/TensorFlowFlexUNet/Prostate and run the following bat file.<br>
<pre>
>1.train.bat
</pre>
, which simply runs the following command.<br>
<pre>
>python ../../../src/TensorFlowFlexUNetTrainer.py ./train_eval_infer.config
</pre>
<hr>

<b>Model parameters</b><br>
Defined a small <b>base_filters=16</b> and a large <b>base_kernels=(11,11)</b> for the first Conv Layer of Encoder Block of 
<a href="./src/TensorFlowFlexUNet.py">TensorFlowFlexUNet.py</a> 
and a large num_layers (including a bridge between Encoder and Decoder Blocks).
<pre>
[model]
image_width    = 512
image_height   = 512
image_channels = 3
input_normalize = True
normalization  = False
num_classes    = 3
base_filters   = 16
base_kernels  = (11,11)
num_layers    = 8
dropout_rate   = 0.05
dilation       = (1,1)
</pre>

<b>Learning rate</b><br>
Defined a small learning rate.  
<pre>
[model]
learning_rate  = 0.00007
</pre>

<b>Loss and metrics functions</b><br>
Specified "categorical_crossentropy" and "dice_coef_multiclass".<br>
<pre>
[model]
loss           = "categorical_crossentropy"
metrics        = ["dice_coef_multiclass"]
</pre>
<b >Learning rate reducer callback</b><br>
Enabled learing_rate_reducer callback, and a small reducer_patience.
<pre> 
[train]
learning_rate_reducer = True
reducer_factor     = 0.5
reducer_patience   = 4
</pre>
<b>Early stopping callback</b><br>
Enabled early stopping callback with patience parameter.
<pre>
[train]
patience      = 10
</pre>
<b></b><br>
<b>RGB color map</b><br>
rgb color map dict for Prostate 1+2 classes.<br>
<pre>
[mask]
mask_file_format = ".png"
;Prostate 1+2
;  gb_map = {peripheral zone:red,  transitional zone:green}    
rgb_map = {(0,0,0):0, (255,0,0):1, (0,255,0):2, }       
</pre>
<b>Epoch change inference callbacks</b><br>
Enabled epoch_change_infer callback.<br>
<pre>
[train]
epoch_change_infer       = True
epoch_change_infer_dir   =  "./epoch_change_infer"
epoch_changeinfer        = False
epoch_changeinfer_dir    = "./epoch_changeinfer"
num_infer_images         = 6
</pre>
By using this epoch_change_infer callback, on every epoch_change, the inference procedure can be called
 for 6 images in <b>mini_test</b> folder. This will help you confirm how the predicted mask changes 
 at each epoch during your training process.<br> <br> 
<b>Epoch_change_inference output at starting (1,2,3)</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/epoch_change_infer_at_start.png" width="1024" height="auto"><br>
<br>
<b>Epoch_change_inference output at middle-point (23,24,25)</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/epoch_change_infer_at_middlepoint.png" width="1024" height="auto"><br>
<br>
<b>Epoch_change_inference output at ending (48,49,50)</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/epoch_change_infer_at_end.png" width="1024" height="auto"><br>

<br>
In this experiment, the training process was terminated at epoch 50.<br><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/train_console_output_at_epoch50.png" width="880" height="auto"><br>
<br>
<a href="./projects/TensorFlowFlexUNet/Prostate/eval/train_metrics.csv">train_metrics.csv</a><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/eval/train_metrics.png" width="520" height="auto"><br>

<br>
<a href="./projects/TensorFlowFlexUNet/Prostate/eval/train_losses.csv">train_losses.csv</a><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/eval/train_losses.png" width="520" height="auto"><br>
<br>
<h3>
4 Evaluation
</h3>
Please move to a <b>./projects/TensorFlowFlexUNet/Prostate</b> folder,<br>
and run the following bat file to evaluate TensorflowFlexUNet model for Prostate.<br>
<pre>
>./2.evaluate.bat
</pre>
This bat file simply runs the following command.
<pre>
>python ../../../src/TensorFlowFlexUNetEvaluator.py  ./train_eval_infer.config
</pre>
Evaluation console output:<br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/evaluate_console_output_at_epoch50.png" width="880" height="auto">
<br><br>Image-Segmentation-Prostate

<a href="./projects/TensorFlowFlexUNet/Prostate/evaluation.csv">evaluation.csv</a><br>
The loss (categorical_crossentropy) to this Prostate/test was very low, and dice_coef_multiclass very high as shown below.
<br>
<pre>
categorical_crossentropy,0.0059
dice_coef_multiclass,0.9971
</pre>
<br>
<h3>5 Inference</h3>
Please move to a <b>./projects/TensorFlowFlexUNet/Prostate</b> folder<br>
,and run the following bat file to infer segmentation regions for images by the Trained-TensorflowFlexUNet model for Prostate.<br>
<pre>
>./3.infer.bat
</pre>
This simply runs the following command.
<pre>
>python ../../../src/TensorFlowFlexUNetInferencer.py ./train_eval_infer.config
</pre>
<hr>
<b>mini_test_images</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/mini_test_images.png" width="1024" height="auto"><br>
<b>mini_test_mask(ground_truth)</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/mini_test_masks.png" width="1024" height="auto"><br>
<hr>
<b>Inferred test masks</b><br>
<img src="./projects/TensorFlowFlexUNet/Prostate/asset/mini_test_output.png" width="1024" height="auto"><br>
<br>
<hr>
<b>Enlarged images and masks for  Prostate  Images of 512x512 pixels</b><br>
As shown below, the inferred masks predicted by our segmentation model trained by the dataset appear similar to the ground truth masks.
<br>
<b>rgb_map = {peripheral zone:red,  transitional zone:green}</b>
<br>
<br>
<table>
<tr>
<th>Input: image</th>
<th>Mask (ground_truth)</th>
<th>Prediction: inferred_mask</th>
</tr>
<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/102000_4.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/102000_4.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/102000_4.png" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/121000_3.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/121000_3.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/121000_3.png" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/125000_1.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/125000_1.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/125000_1.png" width="320" height="auto"></td>
</tr>
<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/127000_5.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/127000_5.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/127000_5.png" width="320" height="auto"></td>
</tr>
<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/barrdistorted_1001_0.3_0.3_109000_6.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/barrdistorted_1001_0.3_0.3_109000_6.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/barrdistorted_1001_0.3_0.3_109000_6.png" width="320" height="auto"></td>
</tr>
<tr>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/images/barrdistorted_1001_0.3_0.3_109000_15.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test/masks/barrdistorted_1001_0.3_0.3_109000_15.png" width="320" height="auto"></td>
<td><img src="./projects/TensorFlowFlexUNet/Prostate/mini_test_output/barrdistorted_1001_0.3_0.3_109000_15.png" width="320" height="auto"></td>
</tr>
</table>
<hr>
<br>
<h3>
References
</h3>
<b>1. FastMRI Prostate: A public, biparametric MRI dataset to advance machine learning for prostate cancer imaging</b><br>
Radhika Tibrewala, Tarun Dutt, Angela Tong, Luke Ginocchio, Riccardo Lattanzi, Mahesh B. Keerthivasan,<br>
Steven H. Baete, Sumit Chopra, Yvonne W. Lui, Daniel K. Sodickson, Hersh Chandarana & Patricia M. Johnson <br>
<a  href="https://www.nature.com/articles/s41597-024-03252-w">https://www.nature.com/articles/s41597-024-03252-w</a>
<br>
<br>
<b>2. Segmentation of prostate and prostate zones using deep learning</b><br>
Olmo Zavala-Romero, Adrian L Breto, Isaac R Xu, Yu-Cherng C Chang, Nicole Gautney, Alan Dal Pra ,<br>
Matthew C Abramowitz, Alan Pollack, Radka Stoyanova<br>
<a href="https://pmc.ncbi.nlm.nih.gov/articles/PMC8418872/">https://pmc.ncbi.nlm.nih.gov/articles/PMC8418872/</a>
<br>
<br>
<b>3. TensorFlow-FlexUNet-Image-Segmentation-Model</b><br>
Toshiyuki Arai <br>
<a href="https://github.com/sarah-antillia/TensorFlow-FlexUNet-Image-Segmentation-Model">
TensorFlow-FlexUNet-Image-Segmentation-Model
</a>
<br>
<br>
