## 1. docker重启后无法启动container。
  docker重启的时候，会有一个bug。我在重启docker后，container的状态是exited，当我启动这个container的时候，报如下异常：

> Error response from daemon: Cannot restart container d87a4ca9e390: Error getting container d87a4ca9e390b967476952ed26196068100608a1aec211c9772899375ea2ce44 from driver devicemapper: Error mounting '/dev/mapper/docker-253:2-12714011-d87a4ca9e390b967476952ed26196068100608a1aec211c9772899375ea2ce44' on '/home/docker/devicemapper/mnt/d87a4ca9e390b967476952ed26196068100608a1aec211c9772899375ea2ce44': device or resource busy

 这个需要umount一下。输入如下命令即可：
```bash
cat /proc/mounts | grep "mapper/docker" | awk '{print $2}' | xargs -r umount
```

