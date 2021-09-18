# FPAR
First Person Activity Recognition exploiting a Self-Supervised motion task, frame selection, a double Conv-LSTM and LSTA. 

<br/>
<br/>
<br/>

The stream on which this project focuses on is the appearance stream which takes RGB images in input. 
The base Ego-RNN architecture proposed by Sudhakaran et Al. is made of a CNN + ConvLSTM exploiting an attention mechanism that uses class activation maps for spatially selective feature extraction.


<br/>

![alt text](https://github.com/emafasce/FPAR/blob/main/Images/1.png)


<br/>
<br/>
<br/>

By visualizing the CAMs, it can be seen that the appearance strem struggles to focus on the objects in motion. To counterbalance this issue, Planamente et Al. proposed a single stream architecture called Self-supervised first Person Action Recognition network (Sparnet) which adds a motion segmentation (MS) self-supervised task to the Ego-RNN architecture. In the MS task the discrepancies between a binary map labeling pixels as either moving or static and the object movement predicted by the network when it looks at a single frame are minimized, forcing the CNN to learn an image embedding that focuses on object movements. This self-supervised task is applied on the second stage of the RGB stream of the Ego-RNN network.

<br/>

![alt text](https://github.com/emafasce/FPAR/blob/main/Images/2.png)


<br/>
<br/>
<br/>

An implemented variation is based on the assumption
that frames that contain more movement are more useful to
represent the activity than the others. In this case IDT maps
are exploited for a very simple preprocessing task called
frame selection. Instead of sampling K frames uniformly
from videos, the K frames with the brightest maps are selected for each video. 


<br/>

![alt text](https://github.com/emafasce/FPAR/blob/main/Images/3.png)


<br/>
<br/>
<br/>

This variation is based on the idea that egocentric and
especially manipulation activities involve the interaction of
more than one object present in the video. For example, in
GTEA-61 one hand or also two hands are used to perform
an action on a object, like opening or taking it. However, the
input of the LSTM is only the CAM of the winner class, so
the LSTM could not be able to track the positions of more
objects at the same time, leading to a possible loss of information. In this simple approach the conv-LSTM is replaced
with two Conv-LSTM merged through a fully connected
layer. Obviously, the choice of using two conv-LSTM is
given by the hardware constraints, but additional experiments could be performed using more networks or more
input combinations.


<br/>

![alt text](https://github.com/emafasce/FPAR/blob/main/Images/4.png)

<br/>
<br/>
<br/>

Long-Short Term Attention is a network proposed by
Sudhakaran et Al. a few years after the publication of their
Ego-RNN model. Two important elements characterize this
network are a built-in attention mechanism and an output
pooling mechanism. The attention pooling enables the network to identify the relevant regions in the input frame and
to maintain a history of the relevant regions seen in the past
frames, while the output pooling enables the network to
propagate a filtered version of the memory which is localized on the most discriminating components. One of the
innovations of this architecture consists in moving the attention mechanism from the CNN level to the RNN.


<br/>

![alt text](https://github.com/emafasce/FPAR/blob/main/Images/5.png)
