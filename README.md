# LUTModelTraining

Cuda/GPU accelerated Jupyter Notebook to train a neural network to analyze 16x16x16 look-up textures for color grading parameters.

This is my final project for Aalto University AI for Media, Art, and Design (CS-E7770) course in 2024.

## Background and motivation

Lookup Tables (LUTs) are used in game engines at the post processing stage to implement a "look" to the final scene color after tonemapping. Main principle is to remap RGB values (#000000 - #ffffff) with linear interpolation using the values from the LUT texture.

In general, LUTs come in many shapes, but 16x16x16 3D texture (provided as 256x16 2D texture) is commonly used and often the go-to format for various third party LUT packs.

LUTs can provide an easy way to try looks to a scene. They are also a very practical format to establish the look in an external graphics editing software. However, as the LUTs work in limited range and quite often come in quite small resoution (just 16 values representing the whole range of a color component), they are not recommended to be used for modern high dynamic range pipelines.

## Training the model

The notebook provides basic color grading and LUT creation functions to generate n samples of training data. Sobol sequence is used to create evenly distributed random parameters in n dimensional space (n being the number of trained color grading parameters).

<img width="640" alt="image" src="https://github.com/A57R4L/LUTModelTraining/assets/3133779/93c69490-e0a2-4e07-bf47-4919ae749451">

## Benchmarking

New test samples generated with random parameters and the model outputs are compared to the groundtruth parameters. In color grading, all operations (saturation, contrast, gamma, gain and offset) are being applied one after another for the same input pixel value. Saturation also blends the values of r,g,b components. In short, the more parameters are included in the training, more harded the job becomes

<img width="640" alt="image" src="https://github.com/A57R4L/LUTModelTraining/assets/3133779/89a4adf6-3a5a-46c8-b49f-e830e976ab46">


<img width="238" alt="image" src="https://github.com/A57R4L/LUTModelTraining/assets/3133779/4f1a7d5e-a7ed-4caf-87d7-5850daad8b38">

## Other tests

The notebook provides testing and debugging functions, including visuals tests to compare groundtruth graded images with the model output graded image. Also test for third party LUT visual comparison is included.

<img width="889" alt="image" src="https://github.com/A57R4L/LUTModelTraining/assets/3133779/e1d78075-f8f9-4e09-a414-f27ac1af297a">


## Results in short and future work

The model in its current version does a decent job for analyzing up to 9 parameters (All 3 components in Saturation, Contrast and Gamma). While it can sometimes get a third party LUT right, the visual test indicates further work is needed in tuning the model for general purpose.

Finding the right grading parameters and input ranges with the ability to minimize parameter crosstalk is key. As the nature of LUT is to provide a meaningful path between 0 and 1 in three dimensional space, using 3D convolutional layers in the might be a better approach.

Further insights are provided in the final pdf report.

## Links and resources

NVidia GPU Gems 2 Chapter 24: Using Lookup Tables to Accelerate Color Transformations https://developer.nvidia.com/gpugems/gpugems2/part-iii-high-quality-rendering/chapter-24-using-lookup-tables-accelerate-color

Unreal Engine documentation: Using Lookup Tables (LUTs) for Color Grading https://docs.unrealengine.com/5.3/en-US/using-look-up-tables-for-color-grading-in-unreal-engine

Test images https://github.com/sobotka/Testing_Imagery




