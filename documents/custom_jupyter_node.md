# 以下を変更してください

```:bash
gcloud container node-pools create highcpu --cluster $clusterName --zone $zone \
        --machine-type=n1-standard-1 --disk-size 10 --preemptible \
        --num-nodes 0 --enable-autoscaling --min-nodes=0 --max-nodes=1 \
        --node-taints=node=highcpu:NoSchedule --node-labels=node=highcpu
```

インスタンスタイプを変更したい場合

```:bash
--machine-type=n1-standard-2
```

ディスクサイズを変更したい場合

```:bash
--disk-size 50
```

Node Poolの名前を変更したい場合

```:bash
highcpu -> highcpu-2
```
