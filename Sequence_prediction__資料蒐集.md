# Sequence_prediction__資料蒐集

[toc]
<!-- toc --> 

## 太陽黑子預測

- [Time Series Deep Learning, Part 1: Forecasting Sunspots With Keras Stateful LSTM In R](http://www.business-science.io/timeseries-analysis/2018/04/18/keras-lstm-sunspots-time-series-prediction.html)
- [Time Series Deep Learning, Part 2: Predicting Sunspot Frequency with Keras LSTM In R](http://www.business-science.io/timeseries-analysis/2018/07/01/keras-lstm-sunspots-part2.html)

## CNN+RNN

- [Combining CNNs and RNNs – Crazy or Genius? - Data Science Central](https://www.datasciencecentral.com/profiles/blogs/combining-cnns-and-rnns-crazy-or-genius)

    > There are things that just don't seem to go together.  Take oil and water for instance.  Both valuable, but try putting them together? 
    > 
    > That was my reaction when I first came across the idea of combining CNNs (convolutional neural nets) and RNNs (recurrent neural nets).  After all they're optimized for completely different problem types.
    > 
    > -   **CNNs** are good with hierarchical or spatial data and extracting unlabeled features. Those could be images or written characters.  CNNs take fixed size inputs and generate fixed size outputs.
    > -   **RNNs** are good at temporal or otherwise sequential data. Could be letters or words in a body of text, stock market data, or speech recognition.  RNNs can input and output arbitrary lengths of data.  LSTMs are a variant of RNNs that allow for controlling how much of prior training data should be remembered, or more appropriately forgotten.
    > 
    > We all know to reach for the appropriate tool based on these very unique problem types.
    > 
    > **So are there problem types that need the capability of both these tools?**
    > 
    > [![](https://api.ning.com/files/2sIBZeVc-HK0kJHviuClGiSw2rukTzwuMt0i33WB69KvR6Xww9TrrLbguqPYL7HmHhwGMQ7FifHWrLjVj5F-8HQO9AjpV0xM/CRFCNNRNNFusion.png?width=250)](https://api.ning.com/files/2sIBZeVc-HK0kJHviuClGiSw2rukTzwuMt0i33WB69KvR6Xww9TrrLbguqPYL7HmHhwGMQ7FifHWrLjVj5F-8HQO9AjpV0xM/CRFCNNRNNFusion.png)
    > As it turns out, yes.  Most of these are readily identified as images that occur in a temporal sequence, in other words video.  But there are some other clever applications not directly related to video that may spark your imagination.  We'll describe several of those below.
    > 
    > There are also several emerging models of how to combine these tools.  In most cases CNNs and RNNs have been married as separate layers with the output of the CNN being used as input to the RNN.  But there are some researchers cleverly combining these two capabilities within a single deep neural net. 
    > 
    > **Video Scene Labeling**
    > 
    > The classical approach to scene labeling is to train a CNN to identify and classify the objects within a frame and perhaps to further classify the objects into a higher level logical group.  For example, the CNN identifies a stove, a refrigerator, a sink, etc. and also up-classifies them as a kitchen.
    > 
    > Clearly the element that's missing is the meaning of the motion over several frames (time).  For example, several frames of a game of pool might correctly say, the shooter sinks the eight ball in the side pocket.  Or several frames of a young person learning to ride a two-wheeler followed by the frame of the rider on the ground, might reasonably be summarized as 'boy falls off bike'.
    > 
    > Researchers have used layered CNN-RNN pairs where the output of the CNN is input to the RNN.  Logically the RNN has also been replaced with LSTMs to create a more 'in the moment' description of each video segment.  Finally there has been some experimentation done with combined RCNNs where the recurrent connection is directly in the kernels as in the diagram above.  See more [*here*](http://proceedings.mlr.press/v32/pinheiro14.pdf).
    > 
    > **Emotion Detection**
    > 
    > Judging the emotion of individuals or groups of individuals from video remains a challenge.  There is an annual competition around this held by the ACM International Conference on Multimodal Interaction known as the EmotiW Grand Challenge.
    > 
    > Each year the target data changes somewhat in nature and typically there are different tests for classifying groups of people versus individuals appearing in videos.
    > 
    > 2016: Group based happiness intensity.
    > 
    > 2017: Group based three class (positive/neutral/negative) emotion detection.
    > 
    > 2018 (scheduled for November) is even more complex.  The challenge will involve classification of eating conditions.  There are three sub-challenges:
    > 
    > 1.  Food-type Sub-Challenge: Perform seven-class food classification per utterance.
    > 2.  Food-likability Sub-Challenge: Recognize the subjects' food likability rating.
    > 3.  Chew and Speak Sub-Challenge: Recognize the level of difficulty to speak while eating.
    > 
    > The key to this challenge is not only the combination of CNNs and RNNs but also the inclusion of an audio track that can be separately modeled and integrated. 
    > 
    > In 2016 the winners created a hybrid network consisting of a RNN and 3D convolutional networks (C3D).  Data fusion and classification takes place late in the process as is traditional.  The RNN takes appearance features extracted by the CNN from individual frames as input and encodes motion later, while C3D models appearance and motion of video simultaneously, subsequently also merged with the audio module. 
    > 
    > Accuracy in this very difficult field still isn't great.  The 2016 winners scored 59.02% on the individual faces.  By 2017 the individual face scores were up to 60.34% and the group scores were up to 80.89% -- keeping in mind that the nature of the challenge changes each year so year-over-year comparison isn't possible.  More on this annual challenge [*here*](https://icmi.acm.org/2018/index.php?id=challenges).
    > 
    > **Video Based Person Re-identification / Gait Recognition**
    > 
    > The goal here is to identify a person when seen in video (from a database of existing labeled individuals) or simply to recognize if this person has been seen before (re-identification -- not labeled).  The dominant line of research has been in gait recognition and the evolving field uses full body motion recognition (arm swing, limps, carriage, etc.).
    > 
    > [![](https://api.ning.com/files/2sIBZeVc-HIN4Zq6aiFj2hMBNjX9p1WRwf*iIu76zefF1t7uVKzPlFe0mCvzccJfMFTiid6wDjUmS-8PpSPbwf9M1mSN59SV/fullbodyrecognition.png?width=250)](https://api.ning.com/files/2sIBZeVc-HIN4Zq6aiFj2hMBNjX9p1WRwf*iIu76zefF1t7uVKzPlFe0mCvzccJfMFTiid6wDjUmS-8PpSPbwf9M1mSN59SV/fullbodyrecognition.png)There are some evident non-technical challenges here the most obvious being change in clothing, shoes, partial obscurity from coats or packages, and the like.  The technical problems well known in CNN are multiple viewpoints (in fact multiple view points as a single person passes say from right to left offering first front, then side, then back views) and the classical image problems of lighting, albedo, and size.
    > 
    > Prior efforts were based on combining several frames of CNN derived data representing one full step (gait) into a type of heat map called a Gait Energy Image (GEI).
    > 
    > Addition of an LSTM allowed several 'steps' to be analyzed together and the time series capability of the LSTM works as a frame-to-frame view transformation models to adjust for perspective.
    > 
    > This study including the image can be found [*here*](https://vision.unipv.it/CV/materiale2016-17/3rd%20Choice/0213.pdf).  Not surprisingly given the application to surveillance, gait recognition has the highest number of cited research papers, almost all of which are being conducted in China.
    > 
    > Full human pose recognition, both for recognition and for labeling (the person is standing, jumping, sitting, etc.) is the next frontier with separate convolutional models for each body part.  Gesture recognition as part of a UI especially in augmented reality is becoming a hot topic.
    > 
    >  [![](https://api.ning.com/files/2sIBZeVc-HJLKZxxKFxF0FHTQNKo9okXYyjUAsPzCPmN15kI3sUgbioJgfdzyrcYKmYMxBBUY2t7oz6oFdPVOgwsJ0ydKVNt/gesturerecognition.png?width=500)](https://api.ning.com/files/2sIBZeVc-HJLKZxxKFxF0FHTQNKo9okXYyjUAsPzCPmN15kI3sUgbioJgfdzyrcYKmYMxBBUY2t7oz6oFdPVOgwsJ0ydKVNt/gesturerecognition.png)
    > 
    > **Weather Prediction**
    > 
    > The objective is to predict the intensity of rainfall over a localized region and over a fairly short time span.  This field is known as 'nowcasting'.
    > 
    > **Quantifying the Functions of DNA Sequences**
    > 
    > Some 98% of human DNA is non-coding, known as Introns.  Originally thought to be evolutionary leftovers with no value, geneticists now know that for example 93% of disease associated variants lie in these regions.  Modeling properties and functions of these regions is an ongoing challenge recently made somewhat easier by a combination CNN/LSTM called DanQ.
    > 
    > According to the developers "the convolution layer captures regulatory motifs, while the recurrent layer captures long-term dependencies between the motifs in order to learn a regulatory 'grammar' to improve predictions. DanQ improves considerably upon other models across several metrics. For some regulatory markers, DanQ can achieve over a 50% relative improvement in the area under the precision-recall curve metric compared to related models."  The study is [*here*](https://academic.oup.com/nar/article/44/11/e107/2468300).
    > 
    > **Creating Realistic Sound Tracks for Silent Videos**
    > 
    > MIT researchers created an extensive collection of labeled sound clips of drumsticks hitting pretty much everything they could think of.  Using a combined CNN/LSTM, the CNN identifies the visual context (what the drumstick is hitting in the silent video) but since the sound clip is temporal and extends over several frames, the LSTM layer is used to match the sound clip to the appropriate frames.
    > 
    > The developers report that humans were fooled by the predicted sound match more than 50% of the time.  See video [*here*](https://www.youtube.com/watch?t=0s&v=flOevlA9RyQ).
    > 
    > **Future Direction**
    > 
    > I was surprised to find such a wealth of examples in which researchers combine CNNs and RNNs to gain the advantages of both.  There are even some [*studies utilizing GANs*](http://openaccess.thecvf.com/content_cvpr_2018/papers/Liu_Multi-Task_Adversarial_Network_CVPR_2018_paper.pdf) in hybrid networks that are quite interesting.
    > 
    > However, while these mashups seem to provide additional capabilities there is another, newer and perhaps more prominent line of research that says that CNNs alone can do the job and that the days of RNNs/LSTMs are numbered.
    > 
    > One group of researchers used [*a novel architecture of deep forests*](https://www.datasciencecentral.com/profiles/blogs/off-the-beaten-path-using-deep-forests-to-outperform-cnns-and-rnn) embedded in a node structure to outperform CNNs and RNNs, with significant savings in compute and complexity.
    > 
    > We also reviewed the more mainstream movement by both Facebook and Google who recently abandoned their RNN/LSTM based tools for speech-to-speech translation in favor of [*Temporal Convolutional Nets (TCNs)*](https://www.datasciencecentral.com/profiles/blogs/temporal-convolutional-nets-tcns-take-over-from-rnns-for-nlp-pred). 
    > 
    > Especially in text problems, but more generally in any time series problem RNNs have an inherent design problem.  Because they read and interpret the input text one word (or character or image) at a time, the deep neural network must wait to process the next word until the current word processing is complete. 
    > 
    > This means that RNNs cannot take advantage of massive parallel processing (MPP) in the same way the CNNs can.  Especially true when the RNN/LSTMs are running both ways at once to better understand context. 
    > 
    > This is a barrier that won't go away and seems to place an absolute limit on the utility of RNN/LSTM architecture.  Temporal Convolutional Neural Nets get around this by using CNN architecture which can easily use MPP acceleration with the emerging concepts of attention and gate hopping.  For more detail [*please see our original article*](https://www.datasciencecentral.com/profiles/blogs/temporal-convolutional-nets-tcns-take-over-from-rnns-for-nlp-pred).
    > 
    > I'm certainly not one to write off an entire line of research, especially where the need for minimum latency is not as severe as speech-to-speech translation.  However, all of these problems described above do seem ripe for a repeated examination using this newer methodology of TCNs.
    > 
    > [*Other articles by Bill Vorhies.*](https://www.datasciencecentral.com/profiles/blog/list?user=0h5qapp2gbuf8)
    > 


## TCN

- [Temporal Convolutional Nets (TCNs) Take Over from RNNs for NLP Predictions - Data Science Central](https://www.datasciencecentral.com/profiles/blogs/temporal-convolutional-nets-tcns-take-over-from-rnns-for-nlp-pred)

    > It's only been since 2014 or 2015 when our DNN-powered applications passed the 95% accuracy point on text and speech recognition allowing for whole generations of chatbots, personal assistants, and instant translators.
    > 
    > Convolutional Neural Nets (CNNs) are the acknowledged workhorse of image and video recognition while Recurrent Neural Nets (RNNs) became the same for all things language.
    > 
    > One of the key differences is that CNNs can recognize features in static images (or video when considered one frame at a time) while RNNs exceled at text and speech which were recognized as sequence or time-dependent problems.  That is where the next predicted character or word or phrase depends on those that came before (left-to-right) introducing the concept of time and therefore sequence.
    > 
    > Actually RNNs are good at all types of sequence problems, including speech/text recognition, language-to-language translation, handwriting recognition, sequence data analysis (forecasting), and even automatic code generation in many different configurations.
    > 
    >  [![](https://api.ning.com/files/iIlSVBG0bp*u5kZnSvL5xoCLJw960*axGU6QL0FMjjbTKTe*khoLLvb12qFTL2zQgGK5VwFgNY8qnQEVk50A6CvZxmwBRsxt/rnndiagrams.jpeg?width=500)](https://api.ning.com/files/iIlSVBG0bp*u5kZnSvL5xoCLJw960*axGU6QL0FMjjbTKTe*khoLLvb12qFTL2zQgGK5VwFgNY8qnQEVk50A6CvZxmwBRsxt/rnndiagrams.jpeg)
    > 
    > In a very short period of time, major improvements to RNNs became dominant including LSTM (long short term memory) and GRU (gated recurring units) both of which improved the span over which RNNs could remember and incorporate data far from the immediate text into its meaning.
    > 
    > **Solving the 'Not' Joke Problem**
    > 
    > With RNNs reading characters or words from left-to-right in time, context became a problem.  For example, in trying to predict the sentiment of a review, the first few comments might be positive (e.g. good food, good atmosphere) but might end with several negative comments (e.g. terrible service, high price) that might ultimately mean the review was negative.  This is the logical equivalent of the 'Not' joke.  'That's a great looking tie. NOT!'.
    > 
    > The solution was to read the text in both directions at once by having two LSTM encoder working at once (bi-directional encoders).  This meant having information from the future (further down the text) leaking into the present but it largely solved the problem.  Accuracy improved.
    > 
    > **Facebook and Google Have a Problem**
    > 
    > Early on when Facebook and Google were launching their automatic language translators, they realized they had a problem.  The translations were taking too long.
    > 
    > RNNs have an inherent design problem.  Because they read and interpret the input text one word (or character) at a time, the deep neural network must wait to process the next word until the current word processing is complete. 
    > 
    > This means that RNNs cannot take advantage of massive parallel processing (MPP) in the same way the CNNs can.  Especially true when the RNN/LSTMs are running both ways at once to better understand context. 
    > 
    > It also means they are very compute intensive since all the intermediate results must be stored until the processing of the entire phrase is complete.
    > 
    > In early 2017 both Google and Facebook came to similar solutions, a way to use CNNs with their MPP capability to process text for language-to-language translation.  In CNNs the computation doesn't rely on information from the previous time step, freeing each computation to be conducted separately with massive parallelization.
    > 
    > Google's solution is called ByteNet, Facebook's is FairSeq (named after their internal Facebook Artificial Intelligence Research (FAIR) team.  FairSeq is available on GitHub.
    > 
    > Facebook says their FairSeq net runs 9X faster than their RNN benchmark.
    > 
    > **How Does It Work -- The Basics**
    > 
    > Thinking about CNNs and how they process images as a 2D 'patch' (height and width), making the jump to text requires only that you think of text as a 1D object (1 unit high and *n* units long). 
    > 
    > But while RNNs do not directly predefine object length, CNNs do so by definition.  So using CNNs requires us to add more layers until the entire receptive field is covered.  This can and does result in very deep CNNs, but with the advantage being, no matter how deep, each can be processed separately in parallel for the huge time savings.
    > 
    > **The Special Sauce: Gating + Hopping = Attention**
    > 
    > Of course it's not quite as simple as that and both the Google and Facebook techniques add something called an 'Attention' function.
    > 
    > The original Attention function appears to have been introduced last year by researchers at Google Brain and the University of Toronto under the name Transformer.  [*Read the original*](https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf) research paper here.
    > 
    > By the time the basically identical function was adopted by both Facebook and Google it had become the 'Attention' function which has two unique features.
    > 
    > The first is identified by Facebook as 'multi-hoping'.  Rather than the traditional RNN approach of looking at the sentence only once, multi-hoping allows the system to take multiple 'glimpses' of the sentence in a manner more like human translators. 
    > 
    > Each glimpse might focus on a noun or verb, not necessarily in sequence, which offers the most insight into meaning for that pass.  Glimpses might be independent or might be dependent on the previous look to then focus on a related adjective, adverb, or auxiliary verb.
    > 
    > [![](https://api.ning.com/files/iIlSVBG0bp9*sLbkNQbbly2DmvOsRMirzdj5nhO67J1SmbrWC-KBffhPyE87*Juq2RtNFZg7gdm1OdCxiwpYmaw-yBKaJ61n/Facebookhopping.png?width=350)](https://api.ning.com/files/iIlSVBG0bp9*sLbkNQbbly2DmvOsRMirzdj5nhO67J1SmbrWC-KBffhPyE87*Juq2RtNFZg7gdm1OdCxiwpYmaw-yBKaJ61n/Facebookhopping.png)Facebook offers this illustration to show the first pass of the French-to-English translation is a single pass to encode each French word, then the multi-hoping routine of the decoder to select the most appropriate English translation.
    > 
    > The second feature is gating which controls the information flow between the hidden layers.  Gating determines what information best produces the next word by essentially allowing the CNN to zoom in or out on the translation in process to achieve the best context for making the next decision.
    > 
    > **Beyond Language Translation -- Temporal Convolutional Nets (TCNs)**
    > 
    > By mid-2017 Facebook and Google had solved the problem of speed of translation by using CNNs combined with the attention function.  The larger question however was this technique good for more than just speeding up translation.  Should we be looking at all the problem types previously assumed to be solvable only with RNNs?  And the answer of course is yes.
    > 
    > There were a number of studies published in 2017; some coming out literally at the same time that Facebook and Google published.  One which does a good job of covering the broader question of what's beyond translation is "An Empirical Evaluation of Generic Convolutional and Recurrent Networks for Sequence Modeling" by Shaojie Bai, J. Zico Kolter, and Vladlen Koltun ([*original here*](https://arxiv.org/pdf/1803.01271.pdf)). 
    > 
    > These are the folks who have labeled this new architecture **Temporal Convolutional Nets (TCNs)** though it's possible that may change as the industry continues to implement them.
    > 
    > Their study is a series of head-to-head benchmark competitions of TCNs versus RNNs, LSTMs, and GRUs across 11 different industry standard RNN problems well beyond language-to-language translation. 
    > 
    > Their conclusion: TCNs are not only faster but also produced greater accuracy in 9 cases and tied in one *(bold figures in the table below drawn from the original study).* [![](https://api.ning.com/files/iIlSVBG0bp-rJSpXg2IE30wWWGbot5GDeBw8WMEgz7zvzWDSQOuqYUHC83KhEvFNgB6mmDPwrN2DYesV4vdgSgX*NsbaXdzo/TCNbenchmarks.png?width=400)](https://api.ning.com/files/iIlSVBG0bp-rJSpXg2IE30wWWGbot5GDeBw8WMEgz7zvzWDSQOuqYUHC83KhEvFNgB6mmDPwrN2DYesV4vdgSgX*NsbaXdzo/TCNbenchmarks.png)
    > 
    > **TCN Advantages / Disadvantages**
    > 
    > Shaojie Bai, J. Zico Kolter, and Vladlen Koltun also provide this useful list of advantages and disadvantages of TCNs.
    > 
    > -   Speed is important. Faster networks shorten the feedback cycle.  The massive parallelism available with TCNs shortens both training and evaluation cycles.
    > -   TCNs offer more flexibility in changing its receptive field size, principally by stacking more convolutional layers, using larger dilation factors, or increasing filter size. This offers better control of the model's memory size.
    > -   TCNs have a backpropagation path different from the temporal direction of the sequence. This avoids the problem of exploding or vanishing gradients which are a major issue with RNNs.
    > -   Lower memory requirement for training, especially in the case of long input sequences.
    > 
    > However, the researchers note that TCNs may not be as easy to adapt to transfer learning as regular CNN applications because different domains can have different requirements on the amount of history the model needs in order to predict. Therefore, when transferring a model from a domain where only little memory is needed to a domain where much longer memory is required, the TCN may perform poorly for not having a sufficiently large receptive field.
    > 
    > **Going Forward**
    > 
    > TCNs have been implemented in major applications with significant benefits that appear to apply across all types of sequence problems.  We'll need to rethink our assumption that sequence problems are exclusively the domain of RNNs and begin to think of TCNs as the natural starting point for our future projects.





