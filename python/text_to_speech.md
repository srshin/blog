# tensorflow를 이용한 text-to-speech 
* reference: https://github.com/srshin/multi-speaker-tacotron-tensorflow
* forked from carpedm20/multi-speaker-tacotron-tensorflow

### 개발환경
* Python3.6
* Tensorflow 1.3 
```
pip install tensorflow==1.3.0
```
* install requirements  
`pip install -r requirements.txt`
* error발생 : comment처리해줌
```
#certifi==2017.7.27.1
#scipy==0.19.1
```
* nltk 설치 (Natural Language Toolkit)  
`python -c "import nltk; nltk.download('punkt')"`

* ffmpeg 설치
https://ffmpeg.zeranoe.com/builds/  
환경변수설정 path에 추가 : D:\BigData\ffmpeg-4.1.1-win64-static\bin

### audio/text/video file 받기 : news_ids.json, audio, assets, video files 생성
* download file
```
python -m datasets.son.download
```
* encoding error발생 
```
    with open(original_text_path, "w", encoding="utf-8") as f:
    with open(text_path, "w",  encoding="utf-8") as f:
```
* directory error 발생 : 코멘트 처리 
```
    #makedirs(video_dir)
    #makedirs(asset_dir)
    #makedirs(audio_dir)
```
* Segment all audios on silence :  한개의 .wav가 30여개의  .wav로 나눠짐
```
python -m audio.silence --audio_pattern "./datasets/son/audio/*.wav" --method=pydub
```
* file 구조
```
    datasets
    ├── son
    │   ├── news_ids.json
    │   └── audio
    │       ├── 1.wav
    │       ├── 1.00001.wav
    │       ├── 1....wav
    │       ├── 2.wav
    │       └── ...
    │   └── assets
    │       ├── 1.txt
    │       ├── 2.txt
    │       └── ...
    │   └── video
    │       ├── 1.ts
    │       ├── 2.ts
    │       └── ...
```
### Google Speech Recognition API로 segmented aduio에서 text 추출 : recognition.json 생성 
* segmented .wav당 해당하는 .txt가 audio 폴더에 생김. 
* api key받기  
https://cloud.google.com/speech-to-text/  
* 클라우드 홈  
https://console.cloud.google.com/home/dashboard?project=sharp-messenger-235609  
* 환경 설정  
GOOGLE_APPLICATION_CREDENTIALS="[PATH]"   
D:\BigData\Download\My First Project-e0b0d2e75c3c.json  
* install package
```
pip install google-cloud-speech
pip install --upgrade google-cloud-storage
```
* audios에서 text추출
```
python -m recognition.google --audio_pattern "./datasets/son/audio/*.*.wav"
```
### training set 준비  : alignment.json 생성 
* original text와 google에서 나온 text비교
```
python -m recognition.alignment --recognition_path "./datasets/son/recognition.json" --score_threshold=0.5
```
* numpy 생성 : data/*.npz 생성
```
python -m datasets.generate_data ./datasets/son/alignment.json
```
### Training
* hparams.py 수정.
(Change cleaners in hparams.py from korean_cleaners to english_cleaners to train with English dataset)
```
    #'cleaners': 'english_cleaners', 
    'cleaners': 'korean_cleaners', 
```
* Train a single-speaker model 
```
python train.py --data_path=datasets/son
```




