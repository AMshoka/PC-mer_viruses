# A new profiling approach for DNA sequences based on the nucleotides' physicochemical features for accurate analysis of SARS-COV-2 genomes
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AMshoka/PC-mer_Corona/blob/main/Code/Training.ipynb)
## PC-mer Workflow
![PC-mer(workflow)](https://user-images.githubusercontent.com/91915096/172617347-b66dff7f-f6fa-4b39-abdf-2ad99c528854.png)
## INTRODUCTION
<p style='text-align: center;'> Our proposed encoding method, PC-mer, is an ultra-fast, alignment-free, accurate, and compact feature extraction method which is compatible with the wide range of machine learning classifiers and can be imple-mented on the simple processing systems. Our simulation results are obtained through a comprehensive analysis of over 5874 unique viral sequences which are divided into 8 datasets, and confirm the superiority of the method, in terms of classification accuracy, runtime, and memory usage. Similar to the k-mer based methods, the applicability of the PC-mer approach, does not end here and it can be also employed in many computational comparison methods. This capability was examined by using the PC-mer and the Manhattan distance to analyze a dataset including 5 samples from 7 different classes. We compared the results to those obtained by an alignment approach. The distance matrices derived by these two methods have acorrelation coefficient value of 98%, as reported in this paper. This study suggests that a proper alignment-free approach for comparative genomics study can be used when the timely taxonomic classification is of the essence, such as at critical periods during novel viral outbreaks. For this purpose, we developed a package based on PC-mer encoding method including two parts: 1) an ML-based classifier, and 2) a computational comparison tool. The ML-based classi-fier is a fast and accurate method classifying the coronaviruses samples from 7 classes by means of the simple classifiers which can also get input sequences from NCBI database by IDs. On the other hand, the computa-tional comparison tool of this package computes a score for each pair of input sequences as an estimation of their dissimilarity. In all, the comprehensive analysis of the PC-mer approach indicates that it is also applica-ble for more detailed analysis of coronaviruses, examining intraspecies samples, as well as SARS-COV-2 samples from other countries. Fur-thermore, since k-mer based methods are used in a variety of applications, like metagenomics classification, we will investigate adoption of PC-mer encoding method in these applications in future studies as well.</p>

## PC-mer's Performance 
### Classification Accuracy: 
| Datasets 	| Accuracy <br>(%) 	| F1 <br>(%) 	| Precision <br>(%) 	| Recall <br>(%) 	|
|:---:	|:---:	|:---:	|:---:	|:---:	|
| Test-1 	| 97.25 	| 97.23 	| 97.38 	| 97.25 	|
| Test-2 	| 95.93 	| 95.9 	| 96.16 	| 95.93 	|
| Test-3a 	| 98.52 	| 98.49 	| 98.85 	| 98.52 	|
| Test-3b 	| 100 	| 100 	| 100 	| 100 	|
| Test-4 	| 100 	| 100 	| 100 	| 100 	|
| Test-5 	| 99.33 	| 99.36 	| 99.55 	| 99.33 	|
| Test-6 	| 100 	| 100 	| 100 	| 100 	|
| Human Coronavirus 	| 100 	| 100 	| 100 	| 100 	| 
###  Test Accuracy (Covid-19 Dataset) 
| Datasets 	| Testing datasets	| Prediction Accuracy (%)	| Predicted label 	| 
|:---:	|:---:	|:---:	|:---:	|
| Test-1 	| 29 Covid-19 Virus sequences	| 100 	| Riboviria 	| 
| Test-2 	| 29 Covid-19 Virus sequences	| 100 	| Coronaviridae 	| 
| Test-3(a/b) 	| 29 Covid-19 Virus sequences	| 100 	| Betacoronavirus	|

### Time Performace:
As another advantage of our proposed encoding method, PC-mer can significantly improve the total processing time, which includes the runtimes of preprocessing, training, and testing procedures. Thanks to its powerful encoding algorithm and thus, facilitating usage of simple machine learning-based models to classify Coronaviridae family, all classification experiments, including preprocessing, training, and testing steps, have been performed on a desktop computer and a CPU processor. 

![Time2(5)](https://user-images.githubusercontent.com/91915096/172781868-14a579f4-4542-43e4-980c-9094a3241d89.png)

### Memory Consumption:
It is worth mentioning that PC-mer encoding allows usage of larger k-mers by reducing the size of encoded data. Specifically, PC-mer encoding is designed to reduce the computational overhead of k-mers, as well as the volume of the generated data from O(4^k) to O(3×2^k). For example, assuming k=7 in the FCGR method, a vector of size 16,384 is generated for each genome sequence, while PC-mer encoding generates a vector of size 12,288 for each genomic sequence, assuming k=12, which is much smaller than that of the FCGR’s generated data for k=7. It should be mentioned that assuming k-mers of size 12 in the FCGR method leads to a vector of size 16,777,216 per genome sequence. As a key superiority, PC-mer encoding with k = 7 (that produces vectors of size 384 for each genome sequence) achieves equal or higher accuracy, compared to the MLDSP tool with k-mers of size 12. We can conclude that the data compression achieved by the PC-mer encoding not only increases the classification accuracy and the feasibility of using larger k-mers, but also it leads to significant reduction in preprocessing, training, and testing times.
Memory Consumption (PC-mer VS. FCGR)           |  Classification Accuracy for the variation of k-mer size in the range of [1,12]
:-------------------------:|:-------------------------:
![data-generated-nv(4)](https://user-images.githubusercontent.com/91915096/172797306-82d37634-55dd-46c2-9ebd-e0fe0f77cc04.png) |   ![acc](https://user-images.githubusercontent.com/91915096/172798793-96896d39-16f8-4840-81f4-d142e9875d65.png)


## PREREQUISITES
The method was implemented in Python 3.8 with the use of scikit-learn library running on a normal desktop computer (CPU: i7-6500 2.5 GHz, RAM: 8 GB RAM, HD: 256GB Lexar, GPU: GeForce GTX 920M. 
# PC-mer Package

Generate your own pc-mer.

## Instructions

1. Install:
```python
pip install pcmer
```
2. Generate pcmer vectors:

```python
from pcmer import features
#sample code
Seq = features.Change_DNA('AGGAAAAGCCAACCAACCTCGATCTCTTGTA')
features = features.PC_mer(Seq)
```
3. Main Features:

* *Change_DNA(dna)*: Extracting sequences from fasta files and uppercasing their characters. 
* *PC_mer(dna, k)*: k-mers generation function based on physicochemical properties. This function takes a sequence and size k as input and its output is the desired feature vector.
* *GFL(mypath)*: Takes a path and automatically reads all the fasta files in the desired path and returns the generated feature vectors and their labels.
* *get_metrics(y_test, y_prediction)*: Calculation of accuracy measures (F1, accuracy, recall, precision) based on real and predicted labels.
* *comp_confmat*: Create a confusion matriX.
* *pcmer_api*: Automatically download sequences from NCBI for training and testing PC-mer pipeline.

## CONTACT INFO

<b>**Somayyeh Koohi**</b> <br>
Department of Computer Engineering <br>
Sharif University of Technology <br>
e-mail: koohi@sharfi.edu <br>
WWW: http://sharif.ir/~koohi/
