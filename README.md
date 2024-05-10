# Trajectory-Guided-Control-End-to-End-Driving-Model

## Architecture
![image](https://github.com/Heng-Henry/Trajectory-Guided-Control-End-to-End-Driving-Model/assets/90209480/e10e86ce-d392-4294-9f6a-b1f08b3ac5a4)








## Result 
![image](https://github.com/Heng-Henry/Trajectory-Guided-Control-End-to-End-Driving-Model/assets/90209480/551e0833-fbbc-438c-9430-75a5e2c3552c)




## Dataset

Download our dataset through [GoogleDrive](https://drive.google.com/file/d/1HZxlSZ_wUVWkNTWMXXcSQxtYdT7GogSm/view?usp=sharing). The total size of our dataset is aroung 130G, make sure you have enough space.

## Training
First, set the dataset path in ``e2e_driving/config.py``.
Training:
```
python e2e_driving/train.py --gpus NUM_OF_GPUS
```
Please check ``e2e_driving/train.py`` for other arguments usage (epochs, learning rate, batch size, etc.), data processing and loss function.

Check training curve.
```
tensorboard --logdir ./log
```
## Evaluation
First, launch the carla server,
```
cd CARLA_ROOT
./CarlaUE4.sh --world-port=2000 -opengl
```
Set the carla path, model ckpt for evaluation in ``leaderboard/scripts/run_evaluation.sh``.

Note that we will save some data for visualization, 
please check ``self.save(tick_data)`` in ``e2e_driving/vision_agent.py``

Start the evaluation.
```
sh leaderboard/scripts/run_evaluation.sh
```

Parse the results from ``results_VA.json`` (Please check [here](https://leaderboard.carla.org/#evaluation-and-metrics) for metric description.)
```
python e2e_driving/statistics.py
```
