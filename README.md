# FPAR
First Person Activity Recognition exploiting a Self-Supervised motion task, frame selection, a double Conv-LSTM and LSTA. 
Report_Fasce.pdf contains the report of the project.

### Base architecture

The stream on which this project focuses on is the appearance stream which takes RGB images in input. 
The base Ego-RNN architecture is made of a CNN + ConvLSTM exploiting an attention mechanism that uses class activation maps for spatially selective feature extraction.



