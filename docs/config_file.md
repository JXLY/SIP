
# 1. Preprocessing

SIP supports the preprocessing of raw data to extract enhanced images and features as input to the classification algorithms. Parameters are illustrated using landsat8 as an example.  

```
landsat8_params:
    landsat8_zip_dir: /home/l44xu/SIP2/data/landsat8_raw_zip
    raw_landsat8_format: tar.gz
    to_unzip: False
    multilook_num: 1
    low_percentage_to_remove: 0.02
    high_percentage_to_remove: 0.02
    output_raw_img_dir: /home/l44xu/SIP/data/landsat8_preprocessed_imgs/
```

**1.1 Unzip the raw data.** If ***to_unzip*** is True, the raw data files with extension ***raw_landsat8_format*** in folder ***landsat8_zip_dir*** will be extracted into separate folders. 

**1.2 Multilooking to reduce size.** To reduce image size, a image patch of size ***multilook_num*** by ***multilook_num*** will be averaged into a single pixel in the preprocessed images. 

**1.3 Remove extrame pixels.** To increase image contrast for better visualization, low intensity pixels of percentage ***low_percentage_to_remove*** will be set to the value 0, and high intensity pixels of percentage ***high_percentage_to_remove*** will be set to the value 255. After this, the dynamic range of image will be extended. 

**1.4 Save preprocessed images.** The preprocessed images will be saved into folder ***output_raw_img_dir***.
 


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
* [Config file] (docs/config_file.md)
* [Burned area detection from Landsat8 Images] (docs/ba_landsat8.md)
<!---* [Getting started](docs/get-started.md)--->
<!---* [Introduction](intro.md)--->
<!---* [Parameters](parameters.md)--->
<!---* [How To](how-to.md)--->
<!---* [FAQ](faq.md)--->
<!---* [Related Websites](related-website.md)--->


## Installation guide:

**Step 1: Install anaconda.** Install conda for python 3.7: https://docs.anaconda.com/anaconda/install/linux/. For Winows, please go to https://www.anaconda.com/distribution/. 

**Step 2: Create python 3.8.2 environment.** Create a conda environment 'py38' that runs on python version 3.8.2. 
```
conda create -n py38 python=3.8
```

**Step 3: Activate 'py38':**

```
conda activate py38
```

**Step 4: Install the following packages:**
```
conda install pytorch 
conda install pandas
conda install -c anaconda pyqt
conda install -c anaconda scikit-image
conda install -c anaconda scikit-learn
conda install pyyaml
conda install git
```
For Windows, the above applies except pytorch. Please use 
```
conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
```

**Step 5: Cd to your home folder, and run**
```
cd you_home_folder
git clone https://github.com/spectrumAI/SIP.git
```

cd to the folder 'SIP' to run the app:
```
cd SIP
python SIP.py
```

**Step 6: Get a license to run.** Please email spectrumaitech@gmail.com with your name and organization to get a free license. Put the license.lic under the pytransform folder and replace the old one. 

# Process Sentinel-1 SAR image for sea ice classification

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

**Step 3: Prepare label mask.** 
- Click on ***"prepare label mask"***, and then specify the csv file you just saved;
- This step transfer ROIs from vectors to images;
- Take a look at the png images generated in the "Image List" panel on the left;

**Step 4: Edit config file.** 
- Open the ***"sentinel1_config_os.yaml"*** config file in the 'config' folder;
- **Make sure you have changed all dirs to your own directories**.

**Step 5: Prepare all dirs and data.** 
- Click on ***"prepare all dirs and data"*** to prepare all training, test and prediction data. 
- You need to choose the .yaml 'config' file you just edited. 
- Take a look at all the folders generated and the 'npz' files. 

**Step 6: Train classifier.** 
- Click on ***'train classifier'*** and then choose the .yaml config file you just edited. 
- Once training is finished, you can see the generated label map by clicking on this file in the 'Image List' panel on the left. 
- Check ***the training and validation accuracies*** in the "train_log" file under the "save_model" folder specified in the .yaml config file you edited. 
- Change the ***number of epoches*** in the .yaml config file and see what happens. 

**Step 7: Test classifier.** 
- You can optionally run ***"Test classifier"***, but it will run on the same image in this example. 
- You also need to select the same .yaml config file. 
- Check the ***test accuracies*** in the "test_log" file under the "save_model" folder specified in the .yaml config file.  

**Step 8: Predict label map on a new image.** 
- Click on ***"Predict image"*** to run the trained model on the other scene in the folder.
- Once it is done, you can also check the label map in the "Image List" panel. You also need to select the same .yaml config file.
- Check the "predict_log" file under the "save_model" folder specified in the .yaml config file. 


# Preprocess raw Sentinel-1 data by just one click:

**Step 1: Download data.** Downlaod Sentinel1 SAR scenes from https://search.asf.alaska.edu/#/.

**Step 2: Copy all downloaded .zip files to /data/sentinel1_raw_zip/ folder.** 

**Step 3: Preprocess.** 
- Run SIP, and click on ***"preprocessing -> sentinel1"***;
- First select the /data/sentinel1_raw_zip/ folder, and then ***select the sentinel1_config_os.yaml file***;
- Take a look at the preprocessed scenes in /data/sentinel1_preprocessed_imgs/ folder;
- Change the 'multilook_num' parameter in the .yaml config file and re-run the program to see what happens. 

**Step 4: Classification.** Go to step 1 in the sentinel-1 example and start from there to finish.

# Preprocess raw Landsat8 L1TP data. 

**Step 1: Download data.** Downlaod Landsat8 L1TP scenes from USGS Earthexplorer https://earthexplorer.usgs.gov. 

**Step 2: Copy all downloaded .tar.gz files to /data/landsat8_raw_zip/ folder.** 

**Step 3: Preprocess.** 
- Run SIP, and click on ***"preprocessing -> Landsat8 L1TP"***;
- First select the /data/landsat8_raw_zip/ folder, and then ***select the landsat8_config_os.yaml file***;
- Take a look at the preprocessed scenes in /data/landsat8_preprocessed_imgs/ folder;
- Change the 'multilook_num' parameter in the .yaml config file and re-run the program to see what happens. 

**Step 4: Classification.** Go to step 1 in the sentinel-1 example and start from there to finish.



# Process RCM SLC CP Winnipeg scene for land cover classification

**Step 1: Download data.** Downlaod Winnipeg RCM SLC CP scene from ftp://ftp.asc-csa.gc.ca/users/OpenData_DonneesOuvertes/pub/RCM/. Copy the data to /data/rcm_raw_data/ folder.

**Step 2: Edit config file** Open config/rcm_slc_cp_config.yaml, and change all dirs to your own dirs.

**Step 3: Open file.** Run SIP, and click on "preprocessing" manu, and click on "RCM SLC CP". ** You need to first select the .safe file in RCM SLC CP data folder, and then select the .yaml file you just edited.

**Step 4: Classification.** Go to step 3 in the sentinel-1 example and start from there to finish.

![](./pics/rcm.png)

![](./pics/rcm_result.png)

