# F-35-Detector
This notebook was written to detect the naval version of the F-35 (F-35B). We detected the cabin's center of gravity and drew a 100 pixel side square around it to identify the center of the aircraft and perform edge detection. For this we used Detecron2, OpenCV and Pillow. For aircraft prediction, we used Convolutional Neural Networks with Keras/TensorFlow.
## Requirements
- To run the notebook do the following:
  - Install Detectron2 by following this tutorial: https://medium.com/@yogeshkumarpilli/how-to-install-detectron2-on-windows-10-or-11-2021-aug-with-the-latest-build-v0-5-c7333909676f
  - Install ffmpeg by following this tutorial: https://phoenixnap.com/kb/ffmpeg-windows. Before verifying that FFmpeg is correctly added to the Windows PATH, restart the computer
  - Run the command ```python3 -m pip install --upgrade Pillow```
  - Run the command ```pip install -U scikit-learn```
  - Run the command ```pip install tqdm```
  - Run the command ```pip install tensorflow```
  - Run the command ```pip install Keras```
  - Run the command ```pip install -U matplotlib```
  - Run the command ```pip install seaborn```
  - Once you have defined the ```JetDtctnNetBslne```, ```TrainModel```, and ```Detector``` classes, run the following commands to train the model  :
    - ```satWidth, satHeight = 1280, 720```
    - ```imgWidth, imgHeight = 100, 100```
    - ```channels = 3```
    - ```batchSize = 16```
    
    - ```path2Weights = "../NewPredictions/weights/best_weights_baseline_3.h5"```
    - ```trainFile = "Train.py"```
    - ```width, height, channels = 100, 100, 3```
    
    - ```if not os.path.isfile(path2Weights):
        print("---Training The Model---")
        model = JetDtctnNetBslne.build(width, height, channels)
        
        trainHelper = TrainModel(model, 'best_weights_baseline_3.h5')
        trainHelper.trainModel()
        print("---Model Trained---")```
        
    - ```print("---Loading the Model---")```
    - ```model = load_model(path2Weights)```
    - ```print("---Model Loaded---")```

You can predict real images by running the following commands:
  - ```lst_jetsPath = []```
  - ```for i in range(1,49):
      lst_jetsPath.append("../Real images pred set/jets-real-" + str(i) + "/")```
      
  - ```print("Predicting image ", lst_jetsPath[47], "...")```
  - ```detect = Detector(model, lst_jetsPath[47])```
  - ```probas, probaMap = detect.predictProba()```
  - ```results = detect.cleanProba(probas)```
  - ```detect.drawBoxes()```
  - ```detect.drawHeatmap(probaMap)```
  - ```detect = []```
  - ```probas, probaMap = [], []```
  - ```results = []```
  - ```print("Image ", lst_jetsPath[47], "predicted !")```

