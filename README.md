# priv_violence_detector
**Privacy-preserving Detection of Violence in Cameras**


By Aaron Margolis

Views are mine alone (not current or former employer)

This proposal presents a technique for detection of violence in camera footage while also preserving the privacy of camera subjects
while still allowing (or improving) training to reach sufficient accuracy as to be useful. Camera owners, such as stores and homeowners,
would like police protection from violent crime. They are often willing to trade privacy by supplying access to police  departments, but
an artificial intelligence that detects violence and only provides detection information would provide both privacy and protection.
The techniques in this proposal, split learning with an adversarial component, would also have many applications for global organizations
performing video analytics at scale. The results of this research would be possible to preserve privacy of videos while still training 
neural networks on them. 

The application of adversarial machine learning may be able to further advance the state-of-the-art for violence detection in videos,
while also improving privacy protection. Several papers have developed AI techniques for detecting violence in videos, but even 98% 
accuracy is not sufficient due to the infrequency of violent activity. In order to train further on live data, this technique
would apply split learning to the camera feeds. Computing resources local to the camera would train on low-level, granular data, 
while sending the higher-level, privacy-preserving data from false positives, true positives and false negatives to a central 
server to train. As this technique trained on live data, it would get increasingly accurate, with fewer false positives 
and negatives.

Detection of violence in videos is an area of active research in AI. This detection has use cases for social media services
such as Facebook and YouTube, which may want to block or warn viewers of violent imagery.The most common approach is a
combination of Convolutional Neural Networks (CNN) for spatial dimensions and Long/Short Term Memory for time.  (1, 2)
This proposal is concerned with fine-tuning these models to reach the necessary accuracy for usefulness. A camera running 
continuously captures approximately 500,000 minutes every year, so if 1 minute shows violent imagery, a 99% accurate AI would 
report 5,000 false positives and one true positive. Thus, an AI would need to use these networks to further train until 
achieving at least 99.999% accuracy in order to be useful.

<img src="https://www.researchgate.net/publication/342428683/figure/fig5/Visualization-of-low-level-and-high-level-feature-map-from-different-layers-of-CNN-model_W640.jpg"/>
This graphic shows the different levels of the CNN in Asad, et al. Note the increased abstraction for features as each level
becomes higher and higher.

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

Split learning using an adverserial component may be a solution to both problems. In split learning, the central computer (or server)
would train only on the higher level features while resources local to the camera (or client) would train on the lower level features. (3)
This approach  still requires significant computing  resources for the central server, and some computing resources local to each camera.
To further increase privacy and preserve resources, the client will only send the high level features if the  camera detects a positive. 
This technique preserves privacy because identifying features such as person's face and clothes remain with the camera operator. It also 
preserves bandwidth and  computing power for the central server. The high level features are a small portion of the overall weights, and 
the positives  (both true and false) are only 1-2% of the overall frames. In addition, if human review detects violent activity that is not
detected by the AI, the higher level features from this false negative could be sent to the central computer for training.

<img src="https://github.com/ARMargolis/priv_violence_detector/blob/main/SplitLearning.jpg"/>

By applying adversarial machine learning techniques, the camera owners can send information that will help the central server train 
while preventing this server from reconstructing the underlying information. One accomplishes this by training AIs on the camera 
devices to add noise that prevents reconstruction while also providing the relevant information. Once this training is complete, 
it can require less resources from the camera owner. (4)

<img src="https://github.com/ARMargolis/priv_violence_detector/blob/main/AdversarialSplit.png"/>

With the ability to train, this approach can become increasingly accurate. As the accuracy increases, there will be less false positives 
so less data will be sent to central computer. This decreases preserves the privacy of more people and reduces bandwidth needs. 
The higher level features already preserve privacy to a great degree. By consolidating the most valuable data in a legal and ethical 
manner, it can decrease the need for police patrols and other approaches that are unlikely to catch violent acts while placing officers 
in danger. Ultimately, this approach may make policework safer for both police and civilians.

Video analytics at scale is a common problem not only for police departments but for many others, such as social media and self-driving vehicles.
Social media companies are often spread out across many jurisdictions, which often have different rules and philosophies related to privacy.
Video analytics, including violence detection, is an important use case. The more data they can train on, and more variety within the data,
the more accurate their models can be. However, many jurisdictions have strong requirements on preserving privacy, often including keeping the
data within that jurisdiction. Self-driving vehicles will have trouble increasing their accuracy in countries that prohibit the taking and retention
of photographs of people without their permission. Split learning, using adversarial training, can allow training across jurisdictions while also 
maintaining the privacy of the people on the video.

References:
1. Mujtaba Asad, Jie Yang, Jiang He, Pourya Shamsolmoali and Xiangjian He, "Multi-frame feature-fusion-based model for violence detection," June 2020.
https://www.researchgate.net/publication/342428683_Multi-frame_feature-fusion-based_model_for_violence_detection/figures

2. A. M. R. Abdali and R. F. Al-Tuma, "Robust Real-Time Violence Detection in Video Using CNN And LSTM," 2019 2nd Scientific Conference of Computer Sciences,
Baghdad, Iraq, 2019, pp. 104-108, doi: 10.1109/SCCS.2019.8852616. https://ieeexplore.ieee.org/document/8852616/

3. Praneeth Vepakomma, Otkrist Gupta, Tristan Swedish and Ramesh Raskar, "Split learning for health: Distributed deep learning without sharing raw patient data,"
Dec 3, 2018. https://arxiv.org/pdf/1812.00564.pdf 

4. Abhishek Singh, "Hands-on training workshop," Workshop on Split Learning for Distributed Machine Learning (SLDML’21), 5:43:00, filmed March 5, 2021.
https://www.youtube.com/watch?v=bxn3-BtPNjw Notebook: https://colab.research.google.com/drive/1BztA7UL9zoCv5mXben2qjJeTWfQRODvC?usp=sharing#scrollTo=VqguUFSNVBXr,
