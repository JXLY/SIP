# Installation guide:

**Step 1: Install anaconda.** Install conda for python 3.7: https://docs.anaconda.com/anaconda/install/linux/. For Winows, please go to https://www.anaconda.com/distribution/. 

**Step 2: Create python 3.8.2 environment.** Create a conda environment 'py38' that runs on python version 3.8.2. 
```
conda create -n py38 python=3.8
```

**Step 3: Activate 'py38':**

```
conda activate py38
```

**Step 4: In linux, install the following packages:**

```
conda install pytorch
``` 

**However, in windows, use the following command:**

```
conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
```

** Install the following packages**
conda install pandas
conda install -c anaconda pyqt
conda install -c conda-forge/label/cf201901 gdal
conda install -c anaconda scikit-image
conda install -c anaconda scikit-learn
conda install pyyaml
conda install git
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


