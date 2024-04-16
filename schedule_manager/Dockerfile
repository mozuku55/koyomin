FROM golang:1.22

WORKDIR /app

# Goモジュールの依存関係を管理
COPY go.mod go.sum ./
RUN go mod download

# ソースコードをコピー
COPY . .

# アプリケーションをビルド
RUN CGO_ENABLED=0 GOOS=linux go build -o server

# ステージ2: 実行環境
FROM alpine:latest
RUN apk --no-cache add ca-certificates

WORKDIR /root/

# ビルドしたバイナリをコピー
COPY --from=builder /app/server .

# ポート8080を公開
EXPOSE 8080

# 実行コマンド
CMD ["./server"]
