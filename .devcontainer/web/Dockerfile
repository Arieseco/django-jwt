FROM python:3.11-rc-slim

# パッケージのインストール
# apt-get update /etc/apt/sources.listに書かれているURLから、パッケージインデックスファイルを引っ張ってきて、cd /var/lib/apt/listsに格納している
# apt-get install -y tzdata Linuxシステムで使用されるタイムゾーンデータをインストールしている -yはyes/noの入力を求められた場合yesと答えるの意味
# rm -rf /var/lib/apt/lists/* "/var/lib/apt/lists/*"の削除 -r フォルダ -f 強制的 
RUN apt-get update \ 
  && apt-get install -y tzdata \
  && rm -rf /var/lib/apt/lists/*

# モジュールのインストール
# WORKDIR 作業ディレクトリの指定
# COPY requirements.txt ${PWD} ローカルのrequirements.txtを${PWD}に移動
WORKDIR /tmp/work
COPY requirements.txt ${PWD}
RUN pip install -r requirements.txt

# 環境変数の定義
ENV TZ=Asia/Tokyo
ENV USER user1

# 一般権限のユーザーを追加
RUN useradd -m ${USER} --uid 1000
RUN gpasswd -a ${USER} sudo
RUN echo "${USER}:passwd" | chpasswd

# ユーザーの切り替え
USER ${USER}
