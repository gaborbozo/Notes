# JVM properties
```bash
# max heap size
java -Xmx1024[m,G]

# max metaspace size
java --XX:MaxMetaspaceSize=1024[m,G]

# garbage collector setting
-XX+[UseSerialGC|UseParallelGC|UseConcMarkSweepGC|G1GC|UseZGC]
```

# Metrics
## Command-line tools
### [jstat](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/jstat.html)
```bash
# 500 - every half seconds
# 10 - total num of outputs
jstat -gcutil pid 500 10

# returning columns
# S0 - survivor space
# S1 - survivor space
# E - eden space
# O - old space
# M - meta space
# YGC - young gen gc events
# YGCT - young gen gc time
# FGC - full garbage collector events
# FGCT - full garbage collector time - a really relevant one
# CGC - 
# CGCT -
# GCT - full garbage collection time

```
## [VisualVM](https://visualvm.github.io/)

## Profilers
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MTY3ODM1MDhdfQ==
-->