# Gray Cast Iron Graphite Classification Using Microsoft Azure Custom Vision

Artificial Intelligence (AI) is a disruptive technology that is revolutionizing different areas of science and industry, and AI tools have been increasingly researched and implemented. This study explores the potential of AI for the recognition of microstructures in cast iron alloys, a crucial process for quality control and property optimization. A customized computer vision model was developed on the Microsoft Azure platform to automatically identify microstructures present in micrographs of cast iron alloys. The model uses a convolutional neural network (CNN) pre-trained with the ImageNet dataset and specific algorithms for the pre-processing and post-processing of metallographic images. The results demonstrate that the model is capable of recognizing with good accuracy the microstructures of cast iron, especially graphite types A, B, and C. The quality of the images and the number of training samples in the dataset may have influenced the model's performance. 

## Literature Review

According to Colpaert (2008), cast irons are ferrous alloys with a chemical composition close to the eutectic iron-carbon, as can be seen in Figure 1, whose carbon contents exceed the limit of approximately 2% (maximum solubility in austenite), forming graphite or primary carbides during solidification. Carbon can be present in cast irons in three forms: dispersed phase, cementite or graphite.

*Figure 1 - Iron-carbon phase diagram.*

![figure-colpaert](https://github.com/mkatzor36/gci-classification/assets/54877987/4a954cb2-ed1d-4197-8b97-791d533bf612)

*Source: Colpaert, 2008.*

Cast irons are usually classified according to their fracture: for alloys with carbon in the form of cementite, the fracture is crystalline and has a light appearance (white cast iron); for alloys that contain graphite, the fracture has a grayish appearance (gray cast iron). With microscopy, it is possible to classify them according to their microstructure. Cast irons that have graphite can have distinct morphologies (such as lamellar, nodular or vermicular). (COLPAERT, 2008)

### Gray Cast Iron

Its chemical composition includes mainly carbon, silicon and iron. Its usual microstructure consists of nonuniformly shaped bodies of graphitic carbon (called graphite flakes) dispersed in a matrix of pearlite. The morphology of the graphite depends on the foundry processing parameters. (ASM INTERNATIONAL, 1998; ASM INTERNATIONAL, 2004)

### Graphite Classification for Gray Cast Iron

The classifications for cast irons, according to shape, distribution, size, nodularity and nodule count are defined by ASTM standard A247. The distribution of flake graphite is categorized into five types (A to E), as can be seen in Figure 2. (ASM INTERNATIONAL, 1998; ASM INTERNATIONAL, 2004; ASTM, 2019)

*Figure 2 - Graphite distributions specified in ASTM A247.*

![figure-asmHandbook](https://github.com/mkatzor36/gci-classification/assets/54877987/0afe0f43-cc7a-4b98-8286-8cb33e0a5978)

*Source: ASM International, 1998.*

Type A consists of homogeneous random graphite distribution, formed during solidification with minimum undercooling. Type B presents rosette patterns and are formed in irons of near-eutectic composition that solidify faster than in Type A. Type C presents straight, coarse plates known as Kish graphite and is formed in hypereutectic irons with high carbon content. Types D and E are formed with high amount of undercooling, and occurs in interdendritic regions. The main difference is that D presents random distribution while E presents preferred orientation. (ASM INTERNATIONAL, 1998)

## Methodology

To create a classification model, the Custom Vision tool was used on the Microsoft Azure platform. The initial database was created using images of gray cast iron micrographs collected from the literature review. For each test, micrographs were selected without a predefined criterion. After the first test, the test images were categorized and added to the database, and the model was subjected to a new training process. The same procedure was repeated after the second test.

### Creating the Workspace on Custom Vision

On the Custom Vision main page (https://www.customvision.ai/), a new project was created as "gray-cast-iron", on the "cast-iron" resource, as can be seen in Figure 3.

*Figure 3 - Custom Vision main page.*
![Captura de Tela (183)](https://github.com/mkatzor36/gci-classification/assets/54877987/460802a9-7b95-4108-93a8-e6834b5c58bf)
*Source: Author, 2024.*

The following project parameters were chosen:
* **Project types:** Classification;
* **Classification types:** Multiclass (single tag per image);
* **Domains:** General (compact);
* **Export capabilities:** Basic platforms.

The dataset was uploaded to the Custom Vision (Figure 4), and the micrographies were separated and categorized according to the ASTM A247 classification (types A, B, C, D and E). All images used (for training and testing) are available in the *inputs* folder.

*Figure 4 - Uploaded dataset.*
![Captura de Tela (194)](https://github.com/mkatzor36/gci-classification/assets/54877987/65ce3d34-172d-439f-9691-c18f284bc1e8)
*Source: Author, 2024.*

### Training the Model

With the dataset categorized, the "Quick Training" option was selected, as can be seen in Figure 5.

*Figure 5 - Quick Training option selected.*
![Captura de Tela (195)](https://github.com/mkatzor36/gci-classification/assets/54877987/26ed16d6-1dda-4923-8a3d-32d7c6ecbee4)
*Source: Author, 2024.*

With the training completed, the results of Precision, Recall, AP and performance per tag for the first iteration were shown in Figure 6.

*Figure 6 - Model perfomance results for first iteration.*
![Captura de Tela (197)](https://github.com/mkatzor36/gci-classification/assets/54877987/2e74386b-892a-4a50-90d8-16a21ae86d26)
*Source: Author, 2024.*

On which:
* **Precision:** The likeliness that a tag predicted by the model is right;
* **Recall:** The percentage of tags correctly predicted by the model;
* **AP:** A measure of the model performance, summaries the precision and recall at different threshold.

### Testing the Model

After the first iteration, eight tests were performed: three tests with type A samples, two tests with type B samples, and three other tests were performed with types C, D, and E samples each. The Figure 7 shows the quick test predictions result for the *report-fei-2* sample.

*Figure 7 - Quick test result for the report-fei-2 sample.*
![Captura de Tela (210)](https://github.com/mkatzor36/gci-classification/assets/54877987/bb0fef48-3e08-4748-8aba-24c0eb76ddd9)
*Source: Author, 2024.*

After the tests, the samples were categorized and included in the dataset, and the model was retrained. For the second iteration, the procedure was repeated.

## Results and Discussion

After each iteration, the overall performance results for the model was measured by the Custom Vision platform, and are available in Table 1.

*Table 1 - Overall performance results in each iteration.*
| Iteration | Precision (%) | Recall (%) | AP (%) |
|---|---|---|---|
| 1 | 71.4 | 71.4 | 89.8 |
| 2 | 66.7 | 66.7 | 82.4 |
| 3 | 72.7 | 72.7 | 56.3 |

### First Iteration

The performance per tag results for the first iteration are shown in Table 2.

*Table 2 - Perfomance per tag for the first iteration.*
| Tag | Precision (%) | Recall (%) | A.P. (%) | Image Count |
|---|---|---|---|---|
| type-A | 100 | 50 | 100 | 7 |
| type-B | 50 | 100 | 100 | 5 |
| type-C | 50 | 100 | 100 | 6 |
| type-D | 100 | 50 | 100 | 7 |
| type-E | 100 | 100 | 100 | 5 |

To evaluate the model's ability to interpret micrographs in the first iteration, eight tests were performed, the results of which are available in Table 3. Of these, the model was able to correctly predict the types of six samples. However, it is possible to observe that the model has a tendency to confuse types B, D, and E. This can be explained due to the visual similarities between the types and the image count close to the minimum required value (five) for model training.

*Table 3 - Quick test prediction results for probability in the first iteration.*
| Sample | Type A (%) | Type B (%) | Type C (%) | Type D (%) | Type E (%) | Correct? |
|---|---|---|---|---|---|---|
| asmHandbook-type-A | **97.3** | 0.1 | 0.6 | 0.0 | 1.8 | Yes |
| asmHandbook-type-B | 0.0 | **54.1** | 0.0 | 42.7 | 3.1 | Yes |
| asmHandbook-type-C | 12.0 | 0.6 | **84.4** | 0.2 | 2.6 | Yes |
| asmHandbook-type-D | 0.0 | 7.4 | 0.0 | **84.6** | 7.8 | Yes |
| asmHandbook-type-E | 0.0 | 33.2 | 0.0 | 6.0 | **60.6** | Yes |
| report-fei-1 | 0.2 | 0.3 | 0.0 | 0.0 | **99.4** | No |
| report-fei-1-mod | 0.0 | 0.1 | 0.0 | 0.0 | **99.8** | No |
| report-fei-2 | 0.0 | **72.5** | 0.1 | 2.7 | 24.5 | Yes |

The sample *report-fei-1* had a prediction result of type E, although it presents a graphite distribution of type A. One possibility raised for this error was the fact that the micrograph (Figure 8) had a yellow coloration, coming from the microscope lighting, different from the micrographs used in the training dataset.

*Figure 8 - The report-fei-1 sample.*
![report_fei_1](https://github.com/mkatzor36/gci-classification/assets/54877987/82ba8891-97a5-4de5-8ef0-320d8ae3de28)
*Source: Author, 2024.*

Therefore, the image color was changed (Figure 9), in order to standardize it according to the other images in the dataset. However, the prediction result remained the same. This can be explained due to the image size. Discrepancies in image sizes can cause the model to interpret uniformly distributed graphite (type A) as oriented interdendritic segregation (type E). The image coloration does not appear to have a significant influence on this interpretation.

*Figure 9 - The report-fei-1-mod sample.*
![report_fei_1_mod](https://github.com/mkatzor36/gci-classification/assets/54877987/cf74782f-c1a3-4cac-b7b7-56ca3bea2c9b)
*Source: Author, 2024.*

### Second Iteration

The performance per tag results for the second iteration are shown in Table 4.

*Table 4 - Perfomance per tag for the second iteration.*
| Tag | Precision (%) | Recall (%) | A.P. (%) | Image Count |
|---|---|---|---|---|
| type-A | 100 | 100 | 100 | 10 |
| type-B | 40 | 100 | 100 | 7 |
| type-C | 100 | 100 | 100 | 7 |
| type-D | 0 | 0 | 83.3 | 8 |
| type-E | 0 | 0 | 20 | 6 |

For the second iteration, nine tests were performed, and the model correctly predicted only three samples, one of type A and two of type B. The training results are in Table 5. There was a tendency for the model to interpret most microstructures as type B. There is a possibility that the images used in this training may have misled the model: in the *soffrittiEtAl-type-A* sample, the dispersed graphite has a different appearance from most training samples; the *mci-type-C* and *soffrittiEtAl-type-C* samples also have distinct Kish graphite compared to the training images; and the model may have misidentified rosette groups (typical of type B) in the *mci-type-D*, *mci-type-E*, and *soffrittiEtAl-type-C* samples. Possibly, using a tool that trains the model to identify certain image features may lead to an increase in its accuracy.

*Table 5 - Quick test prediction results for probability in the second iteration.*
| Sample  | Type A (%) | Type B (%) | Type C (%) | Type D (%) | Type E (%) | Correct? |
|---|---|---|---|---|---|---|
|mci-type-A| **84.9**    | 1.2     | 13.8    | 0       | 0       | Yes |
|mci-type-B| 0       | **99.9**    | 0       | 0       | 0       | Yes |
|mci-type-C| 0       | **90.4**    | 9.3     | 0       | 0.1     | No |
|mci-type-D| 0       | **99.8**    | 0       | 0.1     | 0       | No |
|mci-type-E| 12.8    | **77.5**    | 0.9     | 0       | 8.6     | No |
|soffrittiEtAl-type-A| 0      | **99.9**    | 0       | 0       | 0       | No |
|soffrittiEtAl-type-B| 6.7    | **83.8**    | 9.3     | 0       | 0       | Yes|
|soffrittiEtAl-type-C| **55.1**   | 44.3    | 0.5     | 0       | 0       | No |
|soffrittiEtAl-type-D| 0      | **99.9**    | 0       | 0       | 0       | No |

### Third Iteration

The performance per tag results for the third iteration are shown in Table 6.

*Table 6 - Perfomance per tag for the third iteration.*
| Tag | Precision (%) | Recall (%) | A.P. (%) | Image Count |
|---|---|---|---|---|
| type-A | 50 | 33.3 | 34.8 | 12 |
| type-B | 66.7 | 100 | 66.7 | 9 |
| type-C | 100 | 50 | 59.1 | 9 |
| type-D | 66.7 | 100 | 58.3 | 10 |
| type-E | 100 | 100 | 100 | 7 |

For the third iteration, ten test samples were analyzed, the results of which are shown in Table 7. The model was able to correctly predict the microstructure of six samples. For the *iso-type-C_2* sample, the model possibly interpreted the Kish graphite as a rosette group. The misinterpretation of the *zhyCasting-type-A_1* and *zhyCasting-type-A_2* samples possibly occurred due to the image quality. For the *iso-type-E* sample, it is possible that the smaller training image sample size (seven) may have led to a lower model accuracy; another factor could be the model's difficulty in interpreting oriented interdendritic segregation. For the correctly analyzed samples, all had a probability of 99.9%, indicating that a training dataset with approximately ten images can be effective in generating a model that correctly identifies microstructures and classifies gray cast iron graphite according to its type.

*Table 7 - Quick test prediction results for probability in the third iteration.*
| Sample | Type A (%) | Type B (%) | Type C (%) | Type D (%) | Type E (%) | Correct? |
|---|---|---|---|---|---|---|
| iso-type-A | **99.9** | 0 | 0 | 0 | 0 | Yes |
| iso-type-B | 0 | **99.9** | 0 | 0 | 0 | Yes |
| iso-type-C_1 | 0 | 0 | **99.9** | 0 | 0 | Yes |
| iso-type-C_2 | 0 | **91.1** | 8.8 | 0 | 0 | No |
| iso-type-D | 0 | 0 | 0 | **99.9** | 0 | Yes |
| iso-type-E | 0.2 | **97** | 0 | 0 | 2.7 | No |
| zhyCasting-type-A_1 | 0 | **94.3** | 0 | 0 | 5.5 | No |
| zhyCasting-type-A_2 | 0 | **93.1** | 0 | 0.1 | 6.6 | No |
| zhyCasting-type-A_3 | **99.9** | 0 | 0 | 0 | 0 | Yes |
| zhyCasting-type-A_4 | **99.9** | 0 | 0 | 0 | 0 | Yes |

## Conclusions 

The present study provides several insights:
* It is possible to train a computer vision model to analyze and classify gray cast iron microstructures;
* The best results were obtained for types A, B, C, and D;
* The model had difficulty identifying type E graphite distribution;
* The size of the training dataset and the variety of sample images improve the model's accuracy.

Furthermore, to improve the computer vision model's performance, the following procedures should be taken:
* Increase the number of samples in the training dataset;
* Organize and standardize the training dataset samples;
* Improve the quality and image size of the micrographs;
* Train the model to identify specific graphite form types in the micrographs;
* Include etched micrographs to the training dataset.

## Future Works

* Detection of the different graphite form types for cast iron, such as nodular, ductile, malleable and vermicular;
* Measurement of nodularity for nodular cast iron according to ASTM A257;
* Measurement of nodule count for nodular cast iron according to ASTM A247;
* Classification of microstructure features in micrographs of ferrous and non-ferrous alloys using machine learning.

## References
 
1. ASM International. **ASM Handbook, Volume 9: Metallography and Microstructures.** ASM International, 2004
2. ASM International. **Metals Handbook Desk Edition** (edited by Joseph R. Davis). ASM International, 1998.
3. ASTM Standard A247, 2019, **"Standard Test Method for Evaluating the Microstructure of Graphite in Iron Castings"**. ASTM International, West Conshohocken, PA, 2019, DOI: 10.1520/A0247-19, www.astm.org. 
4. COLPAERT, Hubertus. **Metalografia dos Produtos Siderúrgicos Comuns** (revisão técnica André Luiz V. da Costa e Silva). 4ª Edição - São Paulo: Edgard Blucher, 2008.
5. ELLIOTT, Roy. **Cast Iron Technology.** Butterworth & Co. (Publishers) Ltd., 1988.
6. ISO International Standard 945-1, 2008, **"Microstructure of Cast Irons - Part 1: Graphite Classification by Visual Analysis"**. ISO, Geneva, CH, 2008.
7. RADZIKOWSKA, Janina M. **Mettalography and Microstructures of Cast Iron**. The Foundry Research Institute, 2004. https://doi.org/10.31399/asm.hb.v09.a0003765.
8. SOFFRITTI, C. et al. Mettalurgical and Statistical Approaches to the Study of Cast Iron Street Furniture. Metall Mater Trans A 52, 1127—1141 (2021). https://doi.org/10.1007/s11661-021-06135-6.
9. METAL CASTING INSTITUTE. **Iron Types (page 1), Gray & Ductile Irons.** Michigan Consulting Services, LLC, 2024. *Available at:* https://metalcastinginstitute.com/iron-types/.
10. ZHENGYI CASTING. **Effect of different proportion of pig iron added to gray cast iron cylinder head.** HanLoo, 2022. *Available at:* https://www.zhycasting.com/effect-of-different-proportion-of-pig-iron-added-to-gray-cast-iron-cylinder-head/.

