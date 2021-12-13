# cv-fitness
Testato su sistema windows 10.


# 1. Algoritmo


Otto tipi di azioni: ['arms','circlesArms','cross', 'crunch', 'foldedLegs','hip', 'shoulders','legs','neck','push','sideLegs','squat','twist','turnLegs']. 



# 2. Installa Dipendenze (OpenPose)

Python <= 3.6.

Scaricare la cartella tf-pose-estimation e copiarla in src/githubs, prima di scaricarlo:

```
export MyRoot=$PWD
cd src/githubs  

```
Link:
https://drive.google.com/file/d/1TRkQg1vWf_47MRtFH5BJdMgtkwauoHuN/view?usp=sharing.

Versione aggiornata(non testata): https://github.com/ZheC/tf-pose-estimation.

Installa le dipendenze
```
conda create -n tf tensorflow-gpu
conda activate tf

cd $MyRoot
pip install -r requirements.txt
pip install jupyter tqdm
pip install tensorflow-gpu==1.13.1
sudo apt install swig
pip install "git+https://github.com/philferriere/cocoapi.git#egg=pycocotools&subdirectory=PythonAPI"

cd $MyRoot/src/githubs/tf-pose-estimation/tf_pose/pafprocess
swig -python -c++ pafprocess.i && python setup.py build_ext --inplace
```


## Scripts
I 5 script principali sono sotto src, sono denominati in base all'ordine di esecuzione:
```
src/s1_get_skeletons_from_training_imgs.py    
src/s2_put_skeleton_txts_to_a_single_txt.py
src/s3_preprocess_features.py
src/s4_train.py 
src/s5_test.py
```


# 3. Come eseguire lo scipt

## Introduzione
Lo script src / s5_test.py serve per il riconoscimento delle azioni in tempo reale.


## Prova su file video
``` bash
python src/s5_test.py \
    --model_path model/trained_classifier.pickle \
    --data_type video \
    --data_path data_test/exercise.avi \
    --output_folder output
```

## Prova su una cartella di immagini
``` bash
python src/s5_test.py \
    --model_path model/trained_classifier.pickle \
    --data_type folder \
    --data_path data_test/apple/ \
    --output_folder output
```

## Prova sulla webcam
``` bash
python src/s5_test.py \
    --model_path model/trained_classifier.pickle \
    --data_type webcam \
    --data_path 0 \
    --output_folder output
```

# 5. Dati di training
link:https://drive.google.com/file/d/1TQzF1ICqiWr8v95iwn23M6viaHUVJnT9/view?usp=sharing

Decomprimere il file e sostituire la cartella source_images3 estratta con quella presente in data/source_images3.

All'interno della cartella si trova il file valid_images.txt, che descrive l'etichetta di ogni immagine che ho usato per l'allenamento. (puoi visualizzarlo su data / source_images3 / valid_images.txt .)

# 6. Come eserguire il training

* Esegui i seguenti script uno per uno:
    ``` bash
    python src/s1_get_skeletons_from_training_imgs.py
    python src/s2_put_skeleton_txts_to_a_single_txt.py 
    python src/s3_preprocess_features.py
    python src/s4_train.py 
    ```

Al termine dell'addestramento, e' possibile eseguire lo script src/s5_test.py


