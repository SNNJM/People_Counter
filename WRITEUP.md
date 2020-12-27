

## Explaining Custom Layers

The process behind converting custom layers involves the addition of extensions to both the Model Optimizer and the Inference Engine.

The Model Optimizer searches for each layer of the input model in the list of known layers before building the model's internal representation, optimizing the model, and producing the Intermediate Representation.

There are a few differences depending on the original model framework to actually add custom layers, . In both TensorFlow and Caffe, the first option is to register the custom layers as extensions to the Model Optimizer.

Meanwhile, in Caffe Model, the second option is to register the layers as Custom, then use Caffe to calculate the output shape of the layer. You’ll need Caffe on your system to do this option.

For TensorFlow, its second option is to actually replace the unsupported subgraph with a different subgraph. The final TensorFlow option is to actually offload the computation of the subgraph back to TensorFlow during inference.

**Detail:**
1. Using Model Optimizer to Generate IR Files Containing the Custom Layer
    - Edit the Extractor Extension Template File
    - Edit the Operation Extension Template File
    - Generate the Model IR Files

2. Inference Engine Custom Layer Implementation for the Intel® CPU
    - Edit the CPU extension template files.
    - Compile the CPU extension library.
    - Execute the Model with the custom layer.
3. Generate the Extension Template Files Using the Model Extension Generator

Some of the potential reasons for handling custom layers are...
- Due to OpenVINO support various frameworks(TensorFlow, Caffe, MXNet, ONNX, etc.), so toolkit has a list of all supported layers from these framework. In case of model uses layer that not exists in list, it will be automatically classified as a custom layer by the Model Optimizer. 
- Custom layers are layers that are not included into a list of known layers. If your topology contains any layers that are not in the list of known layers, the Model Optimizer classifies them as custom. [Here from Custom Layers documentation](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_customize_model_optimizer_Customize_Model_Optimizer.html).
- The [list of supported layers](https://docs.openvinotoolkit.org/2019_R3/_docs_MO_DG_prepare_model_Supported_Frameworks_Layers.html) from earlier very directly relates to whether a given layer is a custom layer. Any layer not in that list is automatically classified as a custom layer by the Model Optimizer.


## Comparing Model Performance

My method(s) to compare models before and after conversion to Intermediate Representations
were by observing the type of files and the size of it. Non-frozen model should be in their initial state eg: .onnx, .caffe.
These non-frozen models are reuqired to be frozen which produce .pb file.
The .pb file is the used with model optimizer which can be found in OpenVINO toolkit's directory path.
Success conversion would produce ,bin and .xml files which are know as IR(Intermediate Representative) files.


The inference time of the model pre- and post-conversion was
|Model(Framework)|Inference time OpenVINO (ms)|
| ------ | ------ |
|ssd_mobilenet_v2_coco|80|
|ssd_inception_v2_coco|167|
|ssdlite_mobilenet_v2_coco|44|
|person-detection-retail-0013 (FP16)|45|

## Assess Model Use Cases

Some of the potential use cases of the people counter app are...

Each of these use cases would be useful because...

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. The potential effects of each of these are as follows...

## Model Research

[This heading is only required if a suitable model was not found after trying out at least three
different models. However, you may also use this heading to detail how you converted 
a successful model.]

In investigating potential people counter models, I tried each of the following three models:

- Model 1: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...
  
- Model 2: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...

- Model 3: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...
