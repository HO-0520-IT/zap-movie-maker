# zap-movie-maker
自動で音声とテロップを付けた動画を生成するプログラム
<br/><br/><br/><br/>
# 利用までの手順

## 注意

```
このコードはまだ個人用ツールレベルの状態です。
様々な素材、動画フォーマット、利用形態では使い物にならない可能性が高いです。
また、コードのテスト、記述方法も十分ではありません。
```

## セットアップ
<br/>

### ■ Image Magickのインストール
`Windowsを利用している場合、` ImageMagickのポータブル版をダウンロードして、中身を「./image_magick」配下に全て置いてください
「./image_magick」直下に「magick.exe」等が配置される構成になります
現在、「ImageMagick-7.1.0-portable-Q16-HDRI-x64.zip」での動作を確認しています

Image Magick
https://imagemagick.org/script/download.php


`Linuxを利用している場合、` それぞれのディストリビューションの手順に従ってImageMagickをインストールしてください。
<br/><br/>

### ■ VOICEVOXのインストール
VOICEVOXをインストールし、起動しておいてください
https://voicevox.hiroshiba.jp/
<br/><br/>

### ■ Pythonのインストール
Python3をインストールしてください。
Python 3.10.6で動作を確認しています
<br/><br/>

### ■ ライブラリのインストール
以下のコマンドを実行し、ライブラリをインストールしてください。
```
pip install -r requirements.txt
```

以上でセットアップは完了です。
<br/><br/>

# サンプル動画の生成

サンプル素材を使用して、サンプル動画を生成してみます。
Windowsの場合はcmd.exeから、
```
create_movie.bat
```
を実行してください。実行後 `./output/` ディレクトリに動画が生成されます。
<br/><br/>


# スクリプトの作成、背景の変更

動画を生成するためのスクリプトは `./script.csv` です。

背景画像の変更や、詳細設定は `config.yml`　を変更することで行えます。

(設定方法についての説明は、後日追記します)
<br/><br/><br/><br/>



# スクリプトのコマンド

スクリプトに使用できるコマンドは次の通りです。
空行や、「#」で始まる行はコメントとして無視されます.
<br/><br/>

## ■ メイン動画の表示

メイン動画を欄にメイン動画を表示します
```
main_visual, (表示したいメディアのパス),
```

表示したいメディアには、動画と画像が使用できます

[例]
```
main_visual, ./resource/main_visual/title.png,
```
<br/><br/>

##  ■ テキストテロップの表示と読み上げ

テロップ欄にテキストを表示してそれを読み上げます
```
voice,(表示したいテキスト),(読み方),
```
読み方はオプションで、指定されていない場合は表示したいテキストがVOICEVOXに渡されます。
[例]
```
voice,こんにちは、VTuberのユーミィです,こんにちは、ブイチューバーのユーミィです
```
```
voice,今日は動画生成プログラムを作りました
```
<br/><br/>

##  ■ テキストテロップのみ表示する

テロップ欄にテキストを表示します。
表示時間はVOICEVOXで読み上げた場合の時間ですが、
音声は再生されません。
```
text,(表示したいテキスト),(読み方),
```
読み方はオプションで、指定されていない場合は表示したいテキストがVOICEVOXに渡されます。

[例]

```
text,今日は動画生成プログラムを作りました
```
<br/><br/>


## ■ 間を入れる

何も読み上げない、空白時間を入れます
```
wait,(空白時間[秒])
```

[例]
```
wait,0.5
```
<br/><br/>

## ■ 効果音を鳴らす
効果音を鳴らします
```
se, (表示したいメディアのパス),
```

[例]
```
se, ./resource/se/pon.mp3
```
<br/><br/>

## ■ キャラクターを表示する、キャラクターの表示を切り替える
```
char,(表示したい立ち絵)
```

[例]
```
char,./resource/character/tachie-normal.png,
```
<br/><br/>

# Configファイルについて

`config.yml` が設定ファイルです
<br/><br/>

## ■　プレビューモード

`preview.enable` を有効にすると、 `preview.start` から `preview.end` までの範囲を書き出します。時間の単位は秒です。
<br/><br/>

## ■　GPUエンコードを有効化
NVIDIAのGPUを搭載している場合 `hasNvidiaGpu` を `true` にすると、動画の書き出しが高速化する場合があります。
対応していない場合エラーで終了してしまうので、`false` を設定してください

##  ■　Linuxで使用する場合

日本語に対応したフォントをインストールして、 `movie.text.font_normal` にそのフォントのパスを指定してください。

