# 以下を変更してください

```:bash
gcloud container node-pools create gpu-k80-1 --cluster $clusterName --zone $zone \
        --machine-type=custom-4-26624 --accelerator type=nvidia-tesla-k80,count=1 --disk-size 30 --preemptible \
        --num-nodes 0 --enable-autoscaling --min-nodes=0 --max-nodes=1
        --node-labels=node=gpu-k80-1

```

インスタンスタイプを変更したい場合

```:bash
--machine-type=custom-8-53248
```

ディスクサイズを変更したい場合

```:bash
--disk-size 50
```

GPUのタイプと枚数を変更したい場合

```:bash
type=nvidia-tesla-v100,count=8
```

Node Poolの名前を変更したい場合

```:bash
gpu-k80-1 -> gpu-v100-8
```
