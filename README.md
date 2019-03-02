# fgc_dataset 

In our competition (https://fgc.univ-lr.fr/), we propose a comic character dataset which is extracted from the comic books DCM772 public dataset. This dataset is composed of 772 annotated images from 27 golden age comic books. It is freely collected from the free public domain collection of digitized comic books Digital Comics Museum (https://digitalcomicmuseum.com). The ground-truth annotations of this dataset contain bounding boxes for panels and comic characters (body + faces), and segmentation masks for balloons, and links between balloons and characters.

## Image dataset
In order to create the characters dataset, we crop all instances of main characters from the dataset DCM772 basing on their ground-truth bounding boxes. We have eliminated character’s instances which overlap much with other instances and extra characters (too small or unidentifiable to the eye). The final dataset contains 2871 images of 100 different characters. We have manually identified which image belongs to which comic character class (of 100 different class).

The dataset is divided into 2 sets: dev-set for participants to work with their methods, test-set is for the evaluation phase. All images are provided with the name as the image_id, together with the generated graph for each image. Please note that the images have different sizes. There are in total 100 different labels present in the dataset. All the labels are provided as text files having the following format.

| Image_id | class |
| ------ | ------ |
| DCM010 | 1 |
| DCM202 | 12 | 
| ... | ... | 

#### Training (dev) and Evaluation (test) sets

Each character has atleast 10 images in the training set.
Total of images : 2046 (100 classes)

Each character has atleast 1 images in the test set.
Total of images : 825 (100 classes)

| Dataset | Dataset | Training | Test |
| ------ | ------ | ------ | ------ |
| Number of images | 2871 | 2046 | 825 |
| Numbe of classes | 100 | 100 | 100 |   
| Minimum images per class | 14 |  10 |  1 | 

The datasets are divided randomly.

#### Sample_submission_randomlabel.txt: 

example submission file with random predictions to illustrate the submission file format. The training dataset includes 2000 images of characters and their class. We also provide a sample submission CSV file as an example. The evaluation section has a more detailed description of the submission format.

We do not provide validation dataset, participants can create the validation set from the dev-set data.



#### Examples of several images for 4 comic characters. 

description

## Graph dataset
The graph dataset is constructed by representing each image in the “Image dataset” by an attributed Region Adjacency Graph (RAG). 

The images are preprocessed (and manually checked) and then represented by an attributed RAG. The nodes of a graph represent the MSER regions in the image and its edges represents the spatial relations (based on the proximity) between these MSER regions. The attributes on a node represent the properties of its underlying MSER region and the attributes on an edge represent the properties of the relations between its corresponding underlying MSER regions. The presence of a list of attributes on the nodes and edges of the graphs in the datasets for the competition is very important. However, it is not our goal in this work, to propose the best set of attributes for the nodes and edges of graph representation of comics. The nodes have regionID, compactness, area-in-pixels, RGB color, Lab color, bounding-box (height, width, x, y) and Hu-moments as attributes. Whereas, the edges have percentage of overlap between MSER regions of corresponding nodes as attribute.

The following figure presents an overview of the step for representing a comic character by a RAG (after preprocessing).


#### Overview of graph representation step
The attributed RAGs are saved in standard GXL format (an XML- based format for graphs) which is often used by the research community and which is easy to read/write by majority of the commonly used programming languages. Below is the GXL snippet corresponding to an attributed RAG in the dataset: 


Snippet of XML of an attributed Region Adjacency Grap