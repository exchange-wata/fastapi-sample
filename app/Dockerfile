# FROM python:3.9-alpine
# RUN apk --update add \
#     curl \
#     gcc \
#     musl-dev \
#     linux-headers \
#     build-base \
#     libffi-dev \
#     openssl-dev \
#     bash
# RUN pip install --upgrade pip
# COPY ./ /app
# WORKDIR /app
# RUN pip install -r requirements.txt
# CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]


# Python 3.9の軽量なDebianベースイメージを使用
FROM python:3.9-slim-buster

# pipで必要なパッケージをビルドするために、システムの依存関係をインストールします。
# これが、以前のエラーを修正する鍵となります。
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libssl-dev \
    libffi-dev \
    python3-dev \
    && rm -rf /var/lib/apt/lists/*

# ローカルのファイルを作業ディレクトリにコピー
COPY . .

# アプリケーションの作業ディレクトリを設定
WORKDIR /app

# requirements.txt をコピーし、依存関係をインストール
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# アプリケーションを起動
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]