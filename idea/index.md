# IDEA 卡成球了 ！咋优化 ?


# 默认设置

```
-Xms128m
-Xmx750m
-XX:MaxPermSize=350m
-XX:ReservedCodeCacheSize=240m
-XX:+UseCompressedOops
```
# 设置为大内存  `Big`
```
-Xms1024m
-Xmx4096m
-XX:ReservedCodeCacheSize=1024m
-XX:+UseCompressedOops
```
# 平衡模式  `Balanced`
```
-Xms2g
-Xmx2g
-XX:ReservedCodeCacheSize=1024m
-XX:+UseCompressedOops
```
# 复杂配置  `Sophisticated`
```
-server
-Xms2g
-Xmx2g
-XX:NewRatio=3
-Xss16m
-XX:+UseConcMarkSweepGC
-XX:+CMSParallelRemarkEnabled
-XX:ConcGCThreads=4
-XX:ReservedCodeCacheSize=240m
-XX:+AlwaysPreTouch
-XX:+TieredCompilation
-XX:+UseCompressedOops
-XX:SoftRefLRUPolicyMSPerMB=50
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-Djsse.enableSNIExtension=false
-ea
```

三者之间的差异不大，但是 `Big` 配置下的
`Full GC` 执行时间最快。此外， `Xmx` 内存大些对响应能力提升的帮助非常明显。

