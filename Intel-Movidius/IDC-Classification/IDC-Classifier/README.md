# Invasive Ductal Carcinoma (IDC) Classification Using Computer Vision & IoT

![Intel® Movidius](../images/IDC-Classification.png)

## Abstract

This project shows how existing deep learning technologies can be utilized to train artificial intelligence (AI) to be able to detect invasive ductal carcinoma (IDC)1 (breast cancer) in unlabeled histology images. More specifically, I show how to train a convolutional neural network using TensorFlow* and transfer learning using a dataset of negative and positive histology images. In addition to showing how artificial intelligence can be used to detect IDC, I also show how the Internet of Things (IoT) can be used in conjunction with AI to create automated systems that can be used in the medical industry.

- [View the technical article on Intel® AI Academy Documentation section of IDZ](https://software.intel.com/en-us/articles/machine-learning-and-mammography "View the technical article on Intel® AI Academy Documentation section of IDZ")

**Invasive Ductal Carcinoma (IDC) Classification Using Computer Vision & IoT** combines **Computer Vision** and the **Internet of Things** to provide developers, researchers, doctors and/or students with a way to train a neural network with labelled breast cancer histology images to detect Invasive Ductal Carcinoma (IDC) in unseen/unlabelled images.

The project uses the power of the **Intel® Movidius** and uses a custom trained **Inception V3 model** to carry out **image classification**, both locally and via a server / client. IoT communication is powered by the [iotJumpWay](https://www.iotJumpWay.tech "iotJumpWay") and publishes the results after processing local images or images sent through the API.

![Intel® Movidius](../../Images/movidius.jpg) 

## What Will We Do?

1.  Install the [Intel® NCSDK](https://github.com/movidius/ncsdk "Intel® NCSDK") on a Linux development device.
2.  Install the [Intel® NCSDK API](https://github.com/movidius/ncsdk "Intel® NCSDK API") on a Raspberry Pi 3 / UP Squared.
3.  Install the [iotJumpWay Python MQTT Client](https://github.com/AdamMiltonBarker/JumpWayMQTT "iotJumpWay Python MQTT Client") on the Raspberry Pi / UP Squared and configure the iotJumpWay.
4.  Clone & Set Up The Repo.
5.  Prepare your training dataset.
6.  Finetuning your training parameters.
7.  Train Inception V3 IDC Classification model on Intel® AI DevCloud.
8.  Convert the model to a format suitable for the Movidius.
9.  Test the IDC classifier locally on the Linux development device.
10. Live IDC classification via the server / client.

## Applications

**Invasive Ductal Carcinoma (IDC) Classification Using Computer Vision & IoT** is made up of 5 core applications:

- **DevCloudTrainer:** A training program that allows you to train a convolutional neural network using Intel® AI DevCloud.
- **Evaluator:** An evaluation program for evaluating your model.
- **Classifier:** A classification program for testing your model.
- **Server/API:** A server that powers a REST Api, providing access to the classifier.
- **Client:** A client that can interact with the server/API.

## Related Tutorials

- [IDC Classifier GUI: Upload testing data and run the IDC Classifier from a Universals Windows Application](https://github.com/iotJumpway/IoT-JumpWay-Intel-Examples/tree/master/Intel-Movidius/IDC-Classification/IDC-Classifier-GUI "IDC Classifier GUI: Upload testing data and run the IDC Classifier from a Universals Windows Application")

- [Dev Kit IoT Alarm: An IoT connected alarm system built on a Raspberry Pi using the iotJumpWay](https://github.com/iotJumpway/IoT-JumpWay-Intel-Examples/tree/master/Intel-Movidius/IDC-Classification/Dev-Kit-IoT-Alarm "Dev Kit IoT Alarm: An IoT connected alarm system built on a Raspberry Pi using the iotJumpWay")

## Python Versions

- Tested in Python 3.5

## Software Requirements

- [Intel® NCSDK](https://github.com/movidius/ncsdk "Intel® NCSDK")
- [Tensorflow](https://www.tensorflow.org/install "Tensorflow")
- [iotJumpWay Python MQTT Client](https://github.com/iotJumpway/JumpWayMQTT "iotJumpWay Python MQTT Client")
- [GrovePi](https://github.com/DexterInd/GrovePi "GrovePi")
- [Microsoft Visual Studio 2017](https://www.visualstudio.com/downloads/ "Microsoft Visual Studio 2017")

## Hardware Requirements

- 1 x [Access to Intel® AI DevCloud](https://software.intel.com/en-us/ai-academy/tools/devcloud "Access to Intel® AI DevCloud")
- 1 x [Intel® Movidius](https://www.movidius.com/ "Intel® Movidius")
- 1 x Linux Device for training & converting the trained model to a Movidius friendly model.
- 1 x Raspberry Pi 3 / UP Squared for the classifier / server.

### Optional Hardware

- 1 x Raspberry Pi 3 for IoT connected alarm.
- 1 x Grove starter kit for IoT, Raspberry Pi edition.
- 1 x Blue LED (Grove)
- 1 x Red LED (Grove)
- 1 x Buzzer (Grove)

## Install NCSDK On Your Development Device

The first thing you will need to do is to install the **NCSDK** on your development device, this will be used to convert the trained model into a format that is compatible with the Movidius.

```
 $ mkdir -p ~/workspace
 $ cd ~/workspace
 $ git clone https://github.com/movidius/ncsdk.git
 $ cd ~/workspace/ncsdk
 $ make install
```

Next plug your Movidius into your device and issue the following commands:

```
 $ cd ~/workspace/ncsdk
 $ make examples
```

## Install NCSDK On Your Raspberry Pi 3 / UP Squared

![Intel® Movidius](../images/UP2.jpg)

Next you will need to install the **NCSDK** on your Raspberry Pi 3 / UP Squared device, this will be used by the classifier to carry out inference on local images or images received via the API we will create. Make sure you have the Movidius plugged in.

```
 $ mkdir -p ~/workspace
 $ cd ~/workspace
 $ git clone https://github.com/movidius/ncsdk.git
 $ cd ~/workspace/ncsdk/api/src
 $ make
 $ sudo make install
```
```
 $ cd ~/workspace
 $ git clone https://github.com/movidius/ncappzoo
 $ cd ncappzoo/apps/hello_ncs_py
 $ python3 hello_ncs.py
```

## Getting Started With The iotJumpWay

There are a few tutorials that you should follow before beginning, especially if it is the first time you have used the **iotJumpWay Dev Program**. If you do not already have one, you will require an **iotJumpWay Dev Program developer account**, and some basics to be set up before you can start creating your IoT devices. Visit the following [iotJumpWay Dev Program Docs (5-10 minute read/setup)](https://www.iotjumpway.tech/developers/getting-started "iotJumpWay Dev Program Docs (5-10 minute read/setup)") and check out the guides that take you throughsetting up your Location Space, Zones, Devices and Applications (About 5 minutes read).

## Install iotJumpWay Python MQTT Client On Your Raspberry Pi 3 / UP Squared

Next install the iotJumpWay Python MQTT Client on your Raspberry Pi 3 / UP Squared. For this you can execute the following command:

```
 $ pip3 install JumpWayMQTT
```

## iotJumpWay Device Connection Credentials & Settings

- Setup an iotJumpWay Location Device for IDC Classifier, ensuring you set up a camera node, as you will need the ID of the dummy camera for the project to work. Once your create your device add the location ID and Zone ID to the **IoTJumpWay** details in the confs file located at **model/confs.json**, also add the device ID and device name exactly, add the MQTT credentials to the **IoTJumpWayMQTT** .

You will need to edit your device and add the rules that will allow it to communicate autonomously with the other devices and applications on the network, but for now, these are the only steps that need doing at this point.

Follow the [iotJumpWay Dev Program Location Device Doc](https://www.iotjumpway.tech/developers/getting-started-devices "iotJumpWay Dev Program Location Device Doc") to set up your devices.

```
{
    "IoTJumpWay": {
        "Location": 0,
        "Zone": 0,
        "Device": 0,
        "DeviceName" : "",
        "App": 0,
        "AppName": ""
    },
    "Actuators": {},
    "Cameras": [
        {
            "ID": 0,
            "URL": 0,
            "Name": ""
        }
    ],
    "Sensors": {},
	"IoTJumpWayMQTT": {
        "MQTTUsername": "",
        "MQTTPassword": ""
    },
    "ClassifierSettings":{
        "dataset_dir":"model/train/",
        "log_dir":"model/_logs",
        "log_eval":"model/_logs_eval",
        "classes":"model/classes.txt",
        "labels":"labels.txt",
        "labels_file":"model/train/labels.txt",
        "validation_size":0.3,
        "num_shards":2,
        "random_seed":50,
        "tfrecord_filename":"200label",
        "file_pattern":"200label_%s_*.tfrecord",
        "image_size":299,
        "num_classes":2,
        "num_epochs":60,
        "dev_cloud_epochs":60,
        "test_num_epochs":1,
        "batch_size":10,
        "test_batch_size":36,
        "initial_learning_rate":0.0001,
        "learning_rate_decay_factor":0.96,
        "num_epochs_before_decay":10,
        "NetworkPath":"",
        "InceptionImagePath":"model/test/",
        "InceptionThreshold": 0.54,
        "InceptionGraph":"igraph"
    }
}
```

## Cloning The Repo

You will need to clone this repository to a location on your development terminal. Navigate to the directory you would like to download it to and issue the following commands.

    $ git clone https://github.com/iotJumpway/IoT-JumpWay-Intel-Examples.git

Once you have the repo, you will need to find the files in this folder located in [IoT-JumpWay-Intel-Examples/master/Intel-Movidius/IDC-Classification](https://github.com/iotJumpway/IoT-JumpWay-Intel-Examples/tree/master/Intel-Movidius/IDC-Classification "IoT-JumpWay-Intel-Examples/master/Intel-Movidius/IDC-Classification").

## Preparing Your IDC Training Data

For this tutorial, I used a dataset from Kaggle ( [Predict IDC in Breast Cancer Histology Images](https://www.kaggle.com/paultimothymooney/predict-idc-in-breast-cancer-histology-images/data "Predict IDC in Breast Cancer Histology Images") ), but you are free to use any dataset you like. I have uploaded the collection I used for positive and negative images which you will find in the **model/train** directory. Once you decide on your dataset you need to arrange your data into the **model/train** directory. Each subdirectory should be named with integers, I used 0 and 1 to represent positive and negative. In my testing I used 4400 positive and 4400 negative examples giving an overall training accuracy of 0.8596 (See Training Results below) and an average confidence of 0.96 on correct identifications. The data provided is 50px x 50px, as Inception V3 was trained on images of size 299px x 299px, the images are resized to 299px x 299px, ideally the images would be that size already so you may want to try different datasets and see how your results vary.

## Finetuning Your Training Parameters

You can finetune the settings of the network at any time by editing the classifier settings in the **model/confs.json** file.

```
"ClassifierSettings":{
    "dataset_dir":"model/train/",
    "log_dir":"model/_logs",
    "log_eval":"model/_logs_eval",
    "classes":"model/classes.txt",
    "labels":"labels.txt",
    "labels_file":"model/train/labels.txt",
    "validation_size":0.3,
    "num_shards":2,
    "random_seed":50,
    "tfrecord_filename":"200label",
    "file_pattern":"200label_%s_*.tfrecord",
    "image_size":299,
    "num_classes":2,
    "num_epochs":60,
    "dev_cloud_epochs":60,
    "test_num_epochs":1,
    "batch_size":10,
    "test_batch_size":36,
    "initial_learning_rate":0.0001,
    "learning_rate_decay_factor":0.96,
    "num_epochs_before_decay":10,
    "NetworkPath":"",
    "InceptionImagePath":"model/test/",
    "InceptionThreshold": 0.54,
    "InceptionGraph":"igraph"
}
```

## Training Your IDC Model On Intel® AI DevCloud

Now you are ready to upload the files and folders outlined below to AI DevCloud.

```
model
tools
DevCloudTrainer.ipynb
DevCloudTrainer.py
Eval.py
```

Once uploaded, follow the instructions in **DevCloudTrainer.ipynb**, this notebook will help you sort your data, train your model and evaluate it.

## Training Results

![Training Accuracy](../images/training-accuracy.jpg)

![Training Accuracy](../images/training-total-loss.jpg)

## Evaluating Your Model

Once you have completed your training on the AI DevCloud, complete the notebook by running the evaluation job.

```
INFO:tensorflow:Global Step 1: Streaming Accuracy: 0.0000 (2.03 sec/step)
INFO:tensorflow:Global Step 7: Streaming Accuracy: 0.8843 (0.64 sec/step)

-------------------------------------------------------------------------

INFO:tensorflow:Global Step 68: Streaming Accuracy: 0.8922 (0.81 sec/step)
INFO:tensorflow:Global Step 74: Streaming Accuracy: 0.8942 (0.67 sec/step)
INFO:tensorflow:Final Streaming Accuracy: 0.8941
```

![Training Accuracy](../images/validation-accuracy.jpg)

![Training Accuracy](../images/validation-total-loss.jpg)

## Download Your Model

When the training completes you need to download **model/DevCloudIDC.pb** and **model/classes.txt** to the **model** directory on your development machine, ensure the Movidius is setup and connected and then run the following commands on your development machine:

```
$ cd ~/IoT-JumpWay-Intel-Examples/master/Intel-Movidius/IDC-Classification
$ ./DevCloudTrainer.sh
```

The contents of DevCloudTrainer.sh are as follows:

```
#IDC Classification Trainer
mvNCCompile model/DevCloudIDC.pb -in=input -on=InceptionV3/Predictions/Softmax -o igraph
python3.5 Classifier.py InceptionTest
```

1. Compile the model for Movidius
2. Test

## Testing Your IDC Model

Once the shell script has finished the testing program will start. In my example I had two classes 0 and 1 (IDC negative & IDC positive), a classification of 0 shows that the AI thinks the image is not IDC positive, and a classification of 1 is positive.

```
-- Loaded Test Image model/test/negative.png

-- DETECTION STARTING
-- STARTED: :  2018-04-24 14:14:26.780554

-- DETECTION ENDING
-- ENDED:  2018-04-24 14:14:28.691870
-- TIME: 1.9114031791687012

*******************************************************************************
inception-v3 on NCS
*******************************************************************************
0 0 0.9873
1 1 0.01238
*******************************************************************************

-- Loaded Test Image model/test/positive.png

-- DETECTION STARTING
-- STARTED: :  2018-04-24 14:14:28.699254

-- DETECTION ENDING
-- ENDED:  2018-04-24 14:14:30.577683
-- TIME: 1.878432035446167ß

TASS Identified IDC with a confidence of 0.945

-- Published to Device Sensors Channel

*******************************************************************************
inception-v3 on NCS
*******************************************************************************
1 1 0.945
0 0 0.05542
*******************************************************************************

-- INCEPTION V3 TEST MODE ENDING
-- ENDED:  2018-04-24 14:14:30.579247
-- TESTED:  2
-- IDENTIFIED:  1
-- TIME(secs): 3.984593152999878
```

## Serving Your Live IDC Model

Now that we are all trained and tested, it is time to set up the server that will serve the API. For this I have provided **Server.py** and **Client.py**

The following instructions will help you set up your server and test a positive and negative prediction:

1. If you used the [Predict IDC in Breast Cancer Histology Images](https://www.kaggle.com/paultimothymooney/predict-idc-in-breast-cancer-histology-images/data "Predict IDC in Breast Cancer Histology Images") dataset, you can use the **positive.png** & **negative.png** as they are from that dataset, if not you should chose a positive and negative example from your testing set and replace these images.

2. The server is currently set to start up on localhost, if you would like to change this you need to edit line 281 of **Server.py** and line 38 of **Client.py** to match your desired host. Once you have things working, if you are going to be leaving this running and access it from the outside world you shoud secure it with LetsEncrypt or similar.

3. Upload the following files and folders to the UP Squared or Raspberry Pi 3 that you are going to use for the server.

```
model/test/
model/classes.txt
model/confs.json
tools
igraph
Server.py
```

4. Open up a terminal and navigate to the to the folder containing Server.py then issue the following command. This will start the server and wait to receive images for classification.

```
$ python3.5 Server.py
```

5. If you have followed all of the above steps, you can now start the client on your development machine with the following commands:

```
$ python3.5 Client.py
```

This will send a positive and negative histology slide to the Raspberry Pi 3 / UP Squared which will return the predictions.

```
!! Welcome to IDC Classification Client, please wait while the program initiates !!

-- Running on Python 3.5.2 (default, Nov 23 2017, 16:37:01)
[GCC 5.4.0 20160609]

-- Imported Required Modules
-- IDC Classification Client Initiated

{'Response': 'OK', 'ResponseMessage': 'IDC Detected!', 'Results': 1}
{'Response': 'OK', 'ResponseMessage': 'IDC Not Detected!', 'Results': 0}
```

```
* Running on http://0.0.0.0:7455/ (Press CTRL+C to quit)

-- IDC CLASSIFIER LIVE INFERENCE STARTING
-- STARTED: :  2018-04-24 14:25:36.465183

-- Loading Sample
-- Loaded Sample
-- DETECTION STARTING
-- STARTED: :  2018-04-24 14:25:36.476371

-- DETECTION ENDING
-- ENDED:  2018-04-24 14:25:38.386121
-- TIME: 1.9097554683685303

TASS Identified IDC with a confidence of 0.945

-- Published: 2
-- Published to Device Warnings Channel

-- Published: 3
-- Published to Device Sensors Channel

*******************************************************************************
inception-v3 on NCS
*******************************************************************************
1 1 0.945
0 0 0.05542
*******************************************************************************

-- IDC CLASSIFIER LIVE INFERENCE ENDING
-- ENDED:  2018-04-24 14:25:38.389217
-- TESTED:  1
-- IDENTIFIED:  1
-- TIME(secs): 1.9240257740020752

192.168.1.40 - - [24/Apr/2018 14:25:38] "POST /api/infer HTTP/1.1" 200 -

-- IDC CLASSIFIER LIVE INFERENCE STARTING
-- STARTED: :  2018-04-24 14:25:43.422319

-- Loading Sample
-- Loaded Sample
-- DETECTION STARTING
-- STARTED: :  2018-04-24 14:25:43.432647

-- DETECTION ENDING
-- ENDED:  2018-04-24 14:25:45.310354
-- TIME: 1.877711534500122

-- Published: 4
-- Published to Device Warnings Channel

-- Published: 5
-- Published to Device Sensors Channel

*******************************************************************************
inception-v3 on NCS
*******************************************************************************
0 0 0.9873
1 1 0.01238
*******************************************************************************

-- IDC CLASSIFIER LIVE INFERENCE ENDING
-- ENDED:  2018-04-24 14:25:45.313174
-- TESTED:  1
-- IDENTIFIED:  0
-- TIME(secs): 1.89084792137146

192.168.1.40 - - [24/Apr/2018 14:25:45] "POST /api/infer HTTP/1.1" 200 -
```

## Viewing Your Data

Each command sent to the device is stored in the [iotJumpWay](https://www.iotJumpWay.tech/ "iotJumpWay"). You will be able to access the data in the [iotJumpWay Developers Area](https://www.iotJumpWay.tech/console/ "iotJumpWay Developers Area"). 

Once you have logged into Console, visit the [iotJumpWay Locations homepage](https://www.iotjumpway.tech/console/locations/ "iotJumpWay Locations homepage"). You will see a list of all of your locations and access to **edit**, **zones**, **devices** & **data**.

![Viewing Your Data](../../../images/iotJumpWay-Locations-Data-Tab.jpg)

 Now click on the **data** button in the relevant location to be taken to the data logs area. 

![Viewing Your Data](../../../images/iotJumpWay-Locations-Data.jpg)

## DISCLAIMER

This is a project I created as an extension to one of my facial recognition projects, I advise that this is to be used by developers interested in learning about the use cases of computer vision, medical researchers and students, or professionals in the medical industry to evaluate if it may help them and to expand upon. This is not meant to be an alternative for use instead of seeking professional help. I am a developer not a doctor or expert on cancer.

## ACKNOWLEDGEMENTS

- Uses code from Intel® **movidius/ncsdk** ([movidius/ncsdk Github](https://github.com/movidius/ncsdk "movidius/ncsdk Github"))
- Uses code from chesterkuo **imageclassify-movidius** ([imageclassify-movidius Github](https://github.com/chesterkuo/imageclassify-movidius "imageclassify-movidius Github"))
- Uses data from **paultimothymooney** on **Kaggle** ([predict-idc-in-breast-cancer-histology-images data on Kaggle](https://www.kaggle.com/paultimothymooney/predict-idc-in-breast-cancer-histology-images/data "predict-idc-in-breast-cancer-histology-images data on Kaggle"))

## Bugs/Issues

Please feel free to create issues for bugs and general issues you come across whilst using this or any other Intel® related iotJumpWay issues. You may also use the issues area to ask for general help whilst using the iotJumpWay in your IoT projects.

## Contributors

[![Adam Milton-Barker, Intel® Software Innovator](../../../images/Intel-Software-Innovator.jpg)](https://github.com/AdamMiltonBarker)

