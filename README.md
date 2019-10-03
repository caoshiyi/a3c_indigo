# A3C Indigo: Deep Reinforcement Learning in Congestion Control
## Overview
This is a work that completes the a3c implementation of Indigo based on the original codes offered in [StanfordSNR/indigo](https://github.com/StanfordSNR/indigo)

## Running on Pantheon
Make sure your environment is Python 2.7 and tensorflow 1.12.0. Replace the thirdparty/indigo folder in the [StanfordSNR/Pantheon](https://github.com/StanfordSNR/pantheon) with this repo.

There is already a pre-trained model included under a3c/logs, to test without training, run ```src/experiments/test.py -local -schemes a3c -data-dir DIR ```. And then run ```src/analysis/analyze.py -data-dir DIR``` for analysis result. 

For more detailed usage, run ```src/experiments/test.py -local -h```.

To train a new model, go to thirdparty/indigo/a3c and run ```python train.py -ps-hosts 127.0.0.1:9000 -worker-hosts 127.0.0.1:8000 -username YOUR USER-NAME -rlcc-dir /pantheon/third party/indigo```. After training, copy all the model files under logs/TRAINING_TIME into logs and delete the original model files under logs.

## Modified Files
The main model file for A3C algorithm is thirdparty/indigo/a3c/models.py, where you can change the network settings such as the number of layers and the number of LSTM cells.

thirdparty/indigo/a3c/a3c.py is the training file for a3c algorithm. Related training settings like learning rate, max training epoch and other things can be modified according to your own need in this file.

To modify the settings of the DRL formulation, such as the state, action and rewards, go to indigo/env/sender.py. State is defined in ```recv()```, rewards is defined in ```compute_perfomance()``` and actions are defined at the beginning of ```Class Sender```.

## Performance
The A3C version of Indigo (notified as a3c in the figures) is tested on Pantheon, compared to the DAgger version of Indigo (notified as Indigo in the figures).

![5 Runs](https://github.com/caoshiyi/a3c_indigo/blob/master/performance/pantheon_summary.png?raw=true)

![5 Runs Mean](https://github.com/caoshiyi/a3c_indigo/blob/master/performance/pantheon_summary_mean.png?raw=true)
