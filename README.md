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

The dataset was uploaded to the Custom Vision (Figure 4), and the micrographies were separated and categorized according to the ASTM A247 classification (types A, B, C, D and E).

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

After each iteration, the overall performance results for the model was measured by the Custom Vision platform, and appears in Table 1.

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






