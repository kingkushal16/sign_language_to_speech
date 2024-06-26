# sign_language_to_text

## Purpose
Our project focuses in recognizing signs in real time video feed and convert the detected signs to English sentences. As of now we detect 10 signs only due to limited dataset size(reason for it is discused below), but we can detect more signs as we grow the dataset.


## About the implementation
### Dataset
We have created our own dataset, which cointains 1200 images classified into 10 classes namely 'deaf', 'food', 'hello', 'help', 'iloveyou', 'internet', 'no', 'okay', 'thanks', and 'yes', these classes represent the signs that we detect. Since we used our own and our friends' images we will not be able to upload the dataset due to security reasons.

### Training Phase
We chose SSD MobileNet V2 model ([Download it](http://download.tensorflow.org/models/object_detection/tf2/20200711/ssd_mobilenet_v2_fpnlite_320x320_coco17_tpu-8.tar.gz)) from the Tensorflow 2 Detection Model Zoo. This model can be trained with minimal GPU requirements, in our case we used a laptop with **NVDIA GeForce RTX 3050 Ti Laptop GPU** to train the model. We have trained the model for 15000 steps and with a batch size of 8, you can refer the [pipeline.config](https://github.com/Bu1raj/sign_language_to_speech/blob/main/models/my_ssd_mobilenet_v2_fpnlite_320x320/pipeline.config) file for further details. 


## What you need to do
In order to run the model and perform the detection, you can simply download the follwing files and palce in a folder 
1. Latest checkpoint from [here](https://github.com/Bu1raj/sign_language_to_speech/tree/main/models/my_ssd_mobilenet_v2_fpnlite_320x320)
2. pipeline.config from [here](https://github.com/Bu1raj/sign_language_to_speech/blob/main/models/my_ssd_mobilenet_v2_fpnlite_320x320/pipeline.config)
3. label_map.pbtxt from [here](https://github.com/Bu1raj/sign_language_to_speech/blob/main/annotations/label_map.pbtxt)
4. The detection code from [here](https://github.com/Bu1raj/sign_language_to_speech/blob/main/detection_code.ipynb)
open the [detection_code.iypnb](https://github.com/Bu1raj/sign_language_to_speech/blob/main/detection_code.ipynb) in jupyter notebook/google colab then follow these steps..............

> [!NOTE] 
> The following steps might not be required for everyone, but following along will not harm
1. Install tensorflow using `pip install tensorflow=2.5.0`
2. Install object-detection package using `pip install objection-detection`
3. You need to change few paths in the [detection_code.iypnb](https://github.com/Bu1raj/sign_language_to_speech/blob/main/detection_code.ipynb)
    - ```python
      configs = config_util.get_configs_from_pipeline_file('''path of the pipeline.config file''')
      ```
    - ```python
      ckpt.restore('''path of the downloaded checkpoint''').expect_partial()
      ```
    - ```python
      category_index = label_map_util.create_category_index_from_labelmap('''path of the label_map.pbtxt''')
      ```  
4. Run all the cells in the [detection_code.iypnb](https://github.com/Bu1raj/sign_language_to_speech/blob/main/detection_code.ipynb), you should be able to see a detection window open, this will take several minutes

if you face any erros/problems please refer stackoverflow :upside_down_face: , as we cannot cover all the possible error you might come accross :v:

This project also leverages NLP (Natural Language Processing) to transform a list of words from the 10 words into coherent and meaningful sentences. To achieve this efficiently, we utilized an API from existing large language models (LLMs), specifically Gemini. By carefully crafting prompts, we guide the LLM to generate meaningful sentences from a given list of words.Initially, we concentrated on a smaller subset of 3 words from the list to form sentences. This approach balances complexity and processing time. Although experimenting with different list sizes and more advanced tweaking of the LLM could potentially enhance efficiency, such improvements may incur higher costs and was'nt worth investing our time in.

Before running the project, make sure to put your Gemini API key in cell number 4 of detection_code.ipynb. 
The list of detected words are shown on the terminal as output everytime a new word is detected. Press the Q key on your keyboard to send this list as prompt to Gemini, after which the ouput from the LLM will be displayed in the terminal. 

## Output and Results

The final demo of the project involved presenting the model in real life secanarios with sub optimal lighting, in which it performed upto our calculated expectations. We managed to obtain meaningful sentences from the detected signs and also encorporated Text- to -Speech capabilites.



