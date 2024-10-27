## 3DFace Reconstruction and Facial Expression Transfer using Deep3DFace

- This project enables 3D face reconstruction and facial expression transfer using Deep3DFaceRecon_pytorch.
- This project will work only in GPU enviroment.

## Setup Instructions

## Step 1: Clone the Repository
- git clone <https://github.com/marvensherif/3d_face_reconstruction_Facial_expression_transfer-UNING-DEEP3FACES>

## Step 2: Download Required Models
- Download 01_MorphableModel.mat : <https://faces.dmi.unibas.ch/bfm/main.php?nav=1-2&id=downloads>
- Downolad Exp_Pca.bin : <https://drive.google.com/file/d/1bw5Xf8C12pWmcMhNEu6PtsYVZkVucEN6/view> 
- Download epoch_20.pth : <https://drive.google.com/drive/folders/1liaIxn9smpudjjqMaWWRpP0mXRW_qRPP>
- upload them to googledrive

## Step 3: Setup Directory Structure
## Arrange the downloaded files within the project structure as follows:
```
 Deep3DFaceRecon_pytorch
│
└─── BFM
    │
    └─── 01_MorphableModel.mat
    └─── Exp_pca.bin
    └─── ... 
│
└─── checkpoints
    │
    └─── <model_name>
        │
        └─── epoch_20.pth
```


## Step 4: Prepare Test Images and Landmarks
- Create <folder_to_test_images> 
- Add your test images in this folder.
- Create detections Folder within <folder_to_test_images>
- Inside detections, add a .txt file for each image with the same name of image.
   - Use the reference code in the helper notebook to extract the 5 face landmarks for each image and save these coordinates in the corresponding .txt file.

- Ensure the Same Structre:
```
Deep3DFaceRecon_pytorch
│
└─── <folder_to_test_images>
    │
    └─── *.jpg/*.png
    |
    └─── detections
        |
	└─── *.txt
```

## Step 5: Modify Preprocess.py for Compatibility
- Open Preprocess.py in the utils folder.
- Comment out warnings.filterwarnings("ignore", category=np.VisibleDeprecationWarning) line 19
- Update the array addition as follows trans_params = np.array([w0, h0, s, t[0][0], t[1][0]) line 202

## Step 6: Run the Code
- Follow the steps and installation guidelines provided in the deep3faces notebook to execute the model.
- Results will be saved in : checkpoints/models/results/<folder_to_test_images>
- For each input image, the output will include: .png file , .mat file , .obj file

## Facial Expression Transfer
- Download the .mat file for the source image.
- Use the helper notebook to extract the expression parameters of the source face.
- Open model/bfm.py and navigate to line 261,Comment the existing line and replace it with:exp_coefs = torch.tensor([output from helper function], device=id_coeffs.device).unsqueeze(0)
- repeat the steps again but with the target image only in the <folder_to_test_images>.
 

