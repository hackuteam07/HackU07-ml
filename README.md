# HackU07-ml

## 環境構築
- Mecab
  - インストール方法参考 >> https://qiita.com/Sak1361/items/47e9ec464ccc770cd65c

- ライブラリ
  - 下記コマンドでインストール  
  - `pip install -r requirements.txt`  

- 事前学習済みモデル
  - [ここ](https://drive.google.com/drive/folders/1VngpilapaaN-jH3x1KPfzmYkHUItaR8j?usp=sharing )からダウンロードしてください
  - トップディレクトリで解凍、`model`というディレクトリが生成されればok

## 実行方法
- トップディレクトリで`python main.py`

## モデルの読み込みテスト
- 必要なライブラリが揃っている状態でトップディレクトリで下記コードが動けば読み込みはできています
- モデルディレクトリパスを変更するときは`setup.py`の`MODEL_DIR`を変更してください
```python
from setup import *
import torch
from torch.utils.data import Dataset, DataLoader
from transformers import T5ForConditionalGeneration, T5Tokenizer

#　モデルの読み込み部分
tokenizer = T5Tokenizer.from_pretrained(MODEL_DIR, is_fast=True,model_max_length=args.max_input_length)
trained_model = T5ForConditionalGeneration.from_pretrained(MODEL_DIR)
```

## 処理実態
- T5日本語事前学習モデルをwikihowデータを用いて要約タスクへとファインチューニング
- チューニング済みモデルを用いてニュース本文からタイトルを生成
- モデルの出力が正解と見做し実際のタイトルとモデルタイトルのrouge-lスコアの計算

