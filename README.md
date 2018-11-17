# Data Preparation

Create a folder called 'data'
Create a folder called 'final_dataset'

Download the MS-COCO [Training (13GB)](http://images.cocodataset.org/zips/train2014.zip) and [Validation (6GB)](http://images.cocodataset.org/zips/val2014.zip) images. Also download [Andrej Karpathy's training, validation, and test splits](http://cs.stanford.edu/people/karpathy/deepimagesent/caption_datasets.zip). This zip file contains the captions. Unzip all files and place in 'data' folder. 


Next, type this command:
`python create_input_files.py`

This command reads the data downloaded and saves the following files –

- An **HDF5 file containing images for each split in an `I, 3, 256, 256` tensor**, where `I` is the number of images in the split. Pixel values are still in the range [0, 255], and are stored as unsigned 8-bit `Int`s.
- A **JSON file for each split with a list of `N_c` * `I` encoded captions**, where `N_c` is the number of captions sampled per image. These captions are in the same order as the images in the HDF5 file. Therefore, the `i`th caption will correspond to the `i // N_c`th image.
- A **JSON file for each split with a list of `N_c` * `I` caption lengths**. The `i`th value is the length of the `i`th caption, which corresponds to the `i // N_c`th image.
- A **JSON file which contains the `word_map`**, the word-to-index dictionary.


# Training

To **train the model from scratch**, simply run this file:
`python train.py`

# Validation

The validation set BLEU-4 score calculated at the end of every training epoch is one where the decoder uses teacher forcing. To calculate the validation set score without teacher forcing, which is the correct way of doing it, please run: 
 `python eval.py`