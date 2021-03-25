# priv_violence_detector
**Privacy-preserving Detection of Violence in Cameras**


By Aaron Margolis

Views are mine alone (not current or former employer)

This proposal presents a technique for detection of violence in camera footage that preserves privacy of camera subjects
while still allowing training to reach sufficient accuracy as to be useful. Camera owners, such as stores and homeowners,
would like police protection from violent crime. They are often willing to trade privacy by supplying access to police 
departments, but an artificial intelligence that detects violence and only provides detection information would provide 
both privacy and protection. Several papers have developed AI techniques for detecting violence in videos, but even 98% 
accuracy is not sufficient due to the infrequency of violent activity. In order to train further on live data, this technique
would apply split learning to the camera feeds. Computing resources local to the camera would train on low-level, granular data, 
while sending the higher-level, privacy-preserving data from false positives, true positives and false negatives to a central 
server to train. This technique requires the use of AI detection as reaching the reasonable suspicion standard in order for the 
central server to use. As this technique trained on live data, it would get increasingly accurate, with fewer false positives 
and negatives.

Surveillance footage is common in stores and increasingly common among homeowners. Some camera providers, such as Ring, have 
partnered with police departments to provide access to footage, potentially at the loss of privacy. This trade is a classic 
example of a privacy trade-off: by seeking to provide a certain piece of information- whether or not crime is occuring- 
camera owners provide a large amount of unnecessary data on activities occuring in or around their property. An AI that 
analyzes video feeds and provides only the necessary data- is crime occuring- would be ideal, but a sufficiently accurate AI 
does noy yet exist.

Detecting of violence in videos is an area of active research in AI. This detection has use cases for social media services
such as YouTube and Facebook, which may want to block or warn viewers of violent imagery. The most common approach is a
combination of Convolutional Neural Networks (CNN) for spatial dimensions and Long/Short Term Memory for time dimensions. See
"Multi-frame feature-fusion-based model for violence detection" (by Mujtaba Asad, Jie Yang, Jiang He, Pourya Shamsolmoali
and Xiangjian He) and "Robust Real-Time Violence Detection in Video Using CNN And LSTM" (by Al-Maamoon R. Abdali and Rana
F. Al-Tuma) for more information. 
https://www.researchgate.net/publication/342428683_Multi-frame_feature-fusion-based_model_for_violence_detection/figures
https://ieeexplore.ieee.org/document/8852616/

<img src="https://www.researchgate.net/publication/342428683/figure/fig5/Visualization-of-low-level-and-high-level-feature-map-from-different-layers-of-CNN-model_W640.jpg"/>
This graphic shows the different levels of the CNN in Asad, et al. Note the increased abstraction for features as each level
becomes higher and higher.

This proposal is concerned with fine-tuning these models to reach the necessary accuracy for usefulness. A camera running 
continuously captures approximately 500,000 minutes every year, so if 1 minute shows violent imagery, a 99% accurate AI would 
report 5,000 false positives and one true positive. Thus, an AI would need to use these networks to further train until 
achieving at least 99.999% accuracy in order to be useful.

One technique would be to send all video feeds to a central server for training. But this technique would be neither feasible 
nor ethical (and possibly not even legal). It would require immense computing resources to train on so much data, likely 
overwhelming the central system. The bandwidth of the network would also be a very significant bottleneck. In theory, one 
could overcome these problems through parallel training. But providing so much video feed to a central server either owned by 
or working with police departments would present serious ethical and legal concerns. In order for a police officer to investigate, 
they require "Reasonable Suspicion," as defined by the US Supreme Court in *Terry v. Ohio* to be be based on "specific and 
articulable facts" and "taken together with rational inferences from those facts." This proposal assumes that the identification 
of a positive by an AI would meet the definition of Reasonable Suspicion because it is based on a trained analysis of objective 
facts, specifically the video feed. Such a definition would eliminate many legal concerns regarding concentration of video feeds 
by a police department or contractor.

Split learning may be a solution to both problems. In split learning, the central computer (or server) would train only on the 
higher level features while resources local to the camera (or client) would train on the lower level features. See "Split learning 
for health: Distributed deep learning without sharing raw patient data" (by Praneeth Vepakomma, Otkrist Gupta, Tristan Swedish and 
Ramesh Raskar) for more information. https://arxiv.org/pdf/1812.00564.pdf This approach  still requires significant computing 
resources for the central server, and some computing resources local to each camera. To further increase privacy and preserve 
resources, the client will only send the high level features if the  camera detects a positive. This technique preserves privacy 
because identifying features such as person's face and clothes remain with the camera operator. It also preserves bandwidth and 
computing power for the central server. The high level features are a small portion of the overall weights, and the positives 
(both true and false) are only 1-2% of the overall frames. In addition, if human review detects violent activity that is not detected 
by the AI, the higher level features from this false negative could be sent to the central computer for training.

<img src="https://github.com/ARMargolis/priv_violence_detector/blob/main/SplitLearning.jpg"/>

By applying adversarial machine learning techniques, the camera owners can send information that will help the central server train 
while preventing this server from reconstructing the underlying information. One accomplishes this by training AIs on the camera 
devices to add noise that prevents reconstruction while also providing the relevant information. Once this training is complete, 
it can require less resources from the camera owner. This notebook from Abishek Singh lays out the training requirements.
https://colab.research.google.com/drive/1BztA7UL9zoCv5mXben2qjJeTWfQRODvC?usp=sharing#scrollTo=VqguUFSNVBXr

<img src="https://github.com/ARMargolis/priv_violence_detector/blob/main/AdversarialSplit.png"/>

With the ability to train, this approach can become increasingly accurate. As the accuracy increases, there will be less false positives 
so less data will be sent to central computer. This decreases preserves the privacy of more people and reduces bandwidth needs. 
The higher level features already preserve privacy to a great degree. By consolidating the most valuable data in a legal and ethical 
manner, it can decrease the need for police patrols and other approaches that are unlikely to catch violent acts while placing officers 
in danger. Ultimately, this approach may make policework safer for both police and civilians.
