# Ceph-Luminous-with-Bluestore
Performance test for Ceph v12.2.1 Luminous

## System information
- Number of node: 3
- OSD: 15 SSD (5 SSD per node).
- 02 x 10Gbps per node.
- 02 x E5-2620 per node.
- 64GB RAM per node.

## Result
```javascript
[root@centos7-ceph home]# fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=test --bs=4k --iodepth=64 --size=4G --readwrite=randrw --rwmixread=75
test: (g=0): rw=randrw, bs=4K-4K/4K-4K/4K-4K, ioengine=libaio, iodepth=64
fio-2.2.8
Starting 1 process
Jobs: 1 (f=1): [m(1)] [100.0% done] [399.5MB/133.3MB/0KB /s] [102K/34.2K/0 iops] [eta 00m:00s]
test: (groupid=0, jobs=1): err= 0: pid=2164: Thu Oct 12 02:20:33 2017
  read : io=3071.7MB, bw=394307KB/s, iops=98576, runt=  7977msec
  write: io=1024.4MB, bw=131493KB/s, iops=32873, runt=  7977msec
  cpu          : usr=18.67%, sys=80.63%, ctx=666, majf=0, minf=29
  IO depths    : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.1%, >=64=0.0%
     issued    : total=r=786347/w=262229/d=0, short=r=0/w=0/d=0, drop=r=0/w=0/d=0
     latency   : target=0, window=0, percentile=100.00%, depth=64

Run status group 0 (all jobs):
   READ: io=3071.7MB, aggrb=394307KB/s, minb=394307KB/s, maxb=394307KB/s, mint=7977msec, maxt=7977msec
  WRITE: io=1024.4MB, aggrb=131492KB/s, minb=131492KB/s, maxb=131492KB/s, mint=7977msec, maxt=7977msec

Disk stats (read/write):
    dm-2: ios=779110/259856, merge=0/0, ticks=48517/17133, in_queue=71085, util=98.79%, aggrios=786347/262229, aggrmerge=0/0, aggrticks=48274/17066, aggrin_queue=70629, aggrutil=98.76%
  vda: ios=786347/262229, merge=0/0, ticks=48274/17066, in_queue=70629, util=98.76%
  ```
  ## Issues:
  OSD will crash if you enable jemalloc. Bug tracker at http://tracker.ceph.com/issues/20557
