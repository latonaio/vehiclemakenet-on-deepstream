# vehiclemakenet-on-deepstream
vehiclemakenet-on-deepstream は、DeepStream 上で VehicleMakeNet の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- VehicleMakeNet
- Docker
- TensorRT Runtime

## VehicleMakeNetについて
VehicleMakeNet は、画像内の車を検出し、２０種類の車種のカテゴリラベルを返すAIモデルです。  
VehicleMakeNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、VehicleMakeNet の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の VehicleMakeNet でストリーミングを開始します。  
```
stream-start: ## ストリーミングを開始する
        xhost +
        docker exec -it deepstream-vehiclemakenet deepstream-app -c /app/src/deepstream_app_source1_dashcamnet_vehiclemakenet_vehicletypenet.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために VehicleMakeNet の AIモデルを最適化する手順は、[vehiclemakenet-on-tao-toolkit](https://github.com/latonaio/vehiclemakenet-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである vehiclemakenet.engine は、[vehiclemakenet-on-tao-toolkit](https://github.com/latonaio/vehiclemakenet-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  
