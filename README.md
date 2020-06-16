
# SIP (smart image processing) 

Intelligent pixel-level image classification using deep neural networks.

![](./pics/vhr.png)

# Features

* **Strong feature learning capability** of deep neural networks to capture weak signature information for accurate pixel-level classification and mapping.

* **Fast processing and mapping** of a large number of image scenes by leverating GPU computation;

* **Quickly drawing some examplar pixels** using lines, points and polygons on one scene gives you high-precision pixel-level label map of the whole scene;

* Quickly drawing some lines, points and polygons on mutiple scenes gives you **a robust classifer that generates accurate predictions on new images**; 

* Accurate pixel-level classification and mapping of **many hundreds or thousands large scenes** (e.g., 5k by 5k pixels) can be achived within a single day using **a single desktop with GPU**;

* **Safe and convenient** for research, industry or governmental usage where all the data and data processing is local, avoiding the troubles of uploading your data to the cloud.

* Runs on **multiple system settings**, e.g., loptop with/without GPU, desktop with/without GPU, server with/without GPU; 

* Runs on **multiple operational systems**, e.g., Linux, Windows, MacOS; 

* **Strong preprocessing functionalities** to support open source or commercial images, e.g., **Drone hyperspectral/multispectral image**, Sentinel-1/2/3, RADARSAT-1/2, **RADARSAT Constellation Mission (RCM)**, Landsat, MODIS, Drone images, and other **biomedical and industrial images**;

# Documentation
* [Installation](docs/installation.md)
* [First example - sea ice classification](docs/first_example.md)
* [Image preprocessing](docs/sentinel1_preprocessing.md)
* [Burned area detection from Landsat8 Images](docs/ba_landsat8.md)
* [Config file](docs/config_file.md)
* [FAQ](docs/qa.md)
<!---* [Getting started](docs/get-started.md)--->
<!---* [Introduction](intro.md)--->
<!---* [Parameters](parameters.md)--->
<!---* [How To](how-to.md)--->
<!---* [FAQ](faq.md)--->
<!---* [Related Websites](related-website.md)--->

# First example: Process Sentinel-1 SAR image for sea ice classification

![](./pics/classify.gif)

**Step 1: Run app and open data.** 
- Run SIP;
- Open the '.json' file in ***'SIP/data/sentinel1_preprocessed_imgs'***;
- Also open the associated '.tiff' image.

**Step 2: Draw region of interst (ROI).**  
- ***Double click a class*** in the 'Label List' panel on the right to choose a class; 
- Draw point, or line or polygon to add more ROI for this class;
- ***To finish drawing line and polygon, type 'c' from keyboard***;
- Save drawing using default name;

**Step 3: Edit config file.** 
- Copy ***"sentinel1_config_os.yaml.bak"*** in the 'config' folder and change name to ***sentinel1_config_os.yaml***;
- **Make sure you have changed all dirs to your own directories**;

**Step 4: Prepare label mask.** 
- Click on ***"prepare label mask"*** under ***classification*** menu;
- First select the config file you just edited, and then select the csv file you just saved;
- This step transfer ROIs from vectors to mask images;
- Take a look at the png images generated in the "Image List" panel on the left;

**Step 5: Prepare all dirs and data.** 
- Click on ***"prepare all dirs and data"*** under ***classification*** menu to prepare all training, test and prediction data. 
- You need to choose the .yaml 'config' file you just edited. 
- Once finished, take a look at all the folders generated and 'npz' files under ***data*** folders and 'png' mask files under ***mask*** folders in ***train***, ***val*** and ***test***.  

**Step 6: Train classifier.** 
- Click on ***'train classifier'*** under ***classification*** menu and then choose the .yaml config file you just edited. 
- Once training is finished, you can see the generated label map by clicking on this file in the 'Image List' panel on the left. 
- Check ***the training and validation accuracies*** in the "train_log" file under the "save_model" folder specified in the .yaml config file you edited. 
- Change the ***number of epoches*** in the .yaml config file and see what happens. 

**Step 7: Test classifier.** 
- You can optionally run ***"Test classifier"*** under ***classification***, but it will run on the same image using the trained model in Step 6. 
- You also need to select the same .yaml config file. 
- Check the ***test accuracies*** in the "test_log" file under the "save_model" folder specified in the .yaml config file.  

**Step 8: Predict label map on a new image.** 
- Click on ***"Predict image"*** to run the trained model on the other scene in the folder.
- Once it is done, you can also check the label map in the "Image List" panel. You also need to select the same .yaml config file.
- Check the "predict_log" file under the "save_model" folder specified in the .yaml config file. 



