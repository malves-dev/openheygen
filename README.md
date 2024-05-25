# Solução de código aberto da HeyGen

## Agradecimentos a [coqui](https://github.com/coqui-ai/TTS) e [video-retalking](https://github.com/OpenTalker/video-retalking)

### Uso

Coloque seu arquivo de áudio e vídeo facial original na pasta `source`.

Execute `openheygen.py` para gerar o áudio clonado para o texto de entrada.

```shell
$ pip install -r requirements.txt
$ python3 openheygen.py --text "Insira seu texto aqui" --language "pt"
--text: O texto que você deseja gerar.
--language: A linguagem do texto. Atualmente suporta árabe: ar, português brasileiro: pt, chinês: zh-cn, tcheco: cs, holandês: nl, inglês: en, francês: fr, alemão: de, italiano: it, polonês: pl, russo: ru, espanhol : es, turco: tr, japonês: ja, coreano: ko, húngaro: hu.
--speaker_wav: O arquivo wav do falante que você deseja usar. O padrão é `source/test.wav`.
--output_path: O caminho de saída do áudio gerado. O padrão é `result/output.wav`.
```

Após a geração do áudio, vá para a pasta `video-retalking` e execute `video-retalking.py` para gerar o vídeo final.


### Configuração do ambiente

```shell
$ conda create -n openheygen python=3.8
$ conda activate openheygen
$ conda install ffmpeg
$ pip install -r requirements.txt

$ mkdir ./checkpoints  
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/30_net_gen.pth -O ./checkpoints/30_net_gen.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/BFM.zip -O ./checkpoints/BFM.zip
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/DNet.pt -O ./checkpoints/DNet.pt
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/ENet.pth -O ./checkpoints/ENet.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/expression.mat -O ./checkpoints/expression.mat
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/face3d_pretrain_epoch_20.pth -O ./checkpoints/face3d_pretrain_epoch_20.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/GFPGANv1.3.pth -O ./checkpoints/GFPGANv1.3.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/GPEN-BFR-512.pth -O ./checkpoints/GPEN-BFR-512.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/LNet.pth -O ./checkpoints/LNet.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/ParseNet-latest.pth -O ./checkpoints/ParseNet-latest.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/RetinaFace-R50.pth -O ./checkpoints/RetinaFace-R50.pth
$ wget https://github.com/vinthony/video-retalking/releases/download/v0.0.1/shape_predictor_68_face_landmarks.dat -O ./checkpoints/shape_predictor_68_face_landmarks.dat
$ unzip -d ./checkpoints/BFM ./checkpoints/BFM.zip
```

```shell
$ python3 inference.py \
  --face ../source/test.mp4 \
  --audio ../result/output.wav \
  --outfile ../result/output.mp4
  
--face: O vídeo facial que você deseja usar.
--audio: O áudio que você deseja usar é gerado por `openheygen.py`.
--outfile: O caminho de saída do vídeo gerado.
```

