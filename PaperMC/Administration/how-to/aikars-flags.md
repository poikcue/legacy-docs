# Aikar's Flags
> **提醒**    
> 译者不是一名Java开发者。所以，目前不会翻译每一项翻译的具体解释和作用。虽然已经将此部分翻译列入计划中，但是我不清楚ETA，抱歉。  
## 推荐的JVM启动时参数
要使用这些启动参数，只需要调整`-Xms`和`-Xmx`的值。这些参数对于分配任何大小的内存都适用，即使分配的内存仅仅有500MB（对于高版本的Minecraft服务器，这些内存可能不够用。）    
```
java -Xms10G -Xmx10G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar paper.jar --nogui
```
> **不要在服务器上使用全部内存**    
> 当你根据服务器的实际内存进行配置-Xms与-Xmx项时，例如可用8000M时，不要把这8000M全部分出去！在运行Minecraft服务器时，需要在此项的基础上额外占用一部分内存。建议将-Xms/-Xmx减少1000MB-1500M，以避免内存不够用或者提示`OOMKiller`导致服务器强制关闭。同时，这些内存也要给系统预留一部分。有8000M可用？请设定6500M以确保服务器正常运行。*也有一些服务商会为你额外提供这部分内存，例如提供9500M让你分配8000M给Minecraft服务器。有一些服务商会提供的！问问他们就好。*  

## 推荐内存
**我们推荐至少分配6-10GB内存**，无论你的服务器是什么样的规模！如果你的服务器无法分配10GB内存，也不要强行分配，就如上文所说的一样，预留一些内存。G1GC在内存多的情况下运行的更好。  
  
但是，内存多不一定代表性能会更好。最终，超出某一个值的内存是无用的。分配超出32GB的内存只会增大你的预算，而效果微乎其微。  

如果内存分配12GB或更低，就不用在上文的基础上额外修改参数了。  

### 如果-Xmx的值大于12GB
如果-Xmx的值大于12GB，请调整以下参数：
-   `-XX:G1NewSizePercent=40`
-   `-XX:G1MaxNewSizePercent=50`
-   `-XX:G1HeapRegionSize=16M`
-   `-XX:G1ReservePercent=15`
-   `-XX:InitiatingHeapOccupancyPercent=20`

> **调整说明**  
> 如果调整后老年代收集增加，请恢复到原参数。
  

**下文的所有内容都没有翻译，因为我不是一名Java开发者。具体请见文章开头。**  
**以下内容仅供参考，即无需再前往PaperMC文档和本文反复查阅。**  
  
Explanation of these changes:

-   Base flag set aims for 30/40 to reduce risk of to space issues. With more memory, less of an issue. We can give more to new generation with 40/50, as well as reduce reserve percent since the default reserve will already be larger.
-   Region Size increase helps reduce humongous allocations, and speeds up remarking. We need a smaller region size at smaller heaps to ensure an adequate amount of regions available
-   We can start looking for old generation memory to reclaim with more of a delay with IHOP at 20 since we have more old generation available to space on CPU.

## Java GC Logging[​](https://docs.papermc.io/paper/aikars-flags#java-gc-logging "Direct link to heading")

Are you having old gen issues with these flags? Add the following flags based on your java version to enable GC Logging:

**Java 8-10**

```
-Xloggc:gc.log -verbose:gc -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps-XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=5 -XX:GCLogFileSize=1M
```

**Java 11+**

```
-Xlog:gc*:logs/gc.log:time,uptime:filecount=5,filesize=1M
```

GC logging does not hurt your performance and can be left on at all times. The files will not take up much space (5MB)

## Technical Explanation of the Flags[​](https://docs.papermc.io/paper/aikars-flags#technical-explanation-of-the-flags "Direct link to heading")

1.  **-Xms matching -Xmx -- Why:**  You should never run your server with the case that -Xmx can run the system completely out of memory. Your server should always be expected to use the entire -Xmx! You should then ensure the OS has extra memory on top of that Xmx for non MC/OS level things. Therefore, you should never run MC with -Xmx settings you can't support if java uses it all. Now, that means if -Xms is lower than -Xmx  **YOU HAVE UNUSED MEMORY! Unused memory is wasted memory.**  G1 operates better with the more memory it's given. G1 adaptively chooses how much memory to give to each region to optimize pause time. If you have more memory than it needs to reach an optimal pause time, G1 will simply push that extra into the old generation, and it will not hurt you The fundamental idea of improving GC behavior is to ensure short-lived objects die young and never get promoted. With the more memory G1 has, the better assurance you will get that objects are not getting prematurely promoted to the old generation. G1 Operates differently than previous collectors and is able to handle larger heaps more efficiently.
    
    If it does not need the memory given to it, it will not use it. The entire engine operates differently and does not suffer from too large of heaps, and this is industry-wide accepted information that under G1 to keep Xms and Xmx the same!
    
2.  **UnlockExperimentalVMOptions**  -- needed for some the below options
    
3.  **G1NewSizePercent:**  These are the important ones. You now can specify percentages of an overall desired range for the new generation. With these settings, we tell G1 to not use its default 5% for new gen, and instead give it 40%!  **Minecraft has an extremely high a memory allocation rate, ranging to at least 800 Megabytes a second on a 30 player server! And this is mostly short-lived objects (Block Position).**
    
    Now, this means MC REALLY needs more focus on New Generation to be able to even support this allocation rate. If your new gen is too small, you will be running new gen collections 1-2+ times per second, which is awful. You will have so many pauses that TPS has risk of suffering, and the server will not be able to keep up with the cost of GC's. Then combine the fact that objects will now promote faster, resulting in your Old Gen growing faster. Given more New Gen, we are able to slow down the intervals of Young Gen collections, resulting in more time for short-lived objects to die young and overall more efficient GC behavior.
    
4.  **G1MixedGCLiveThresholdPercent:**  Controls when to include regions in Mixed GC's in the Young GC collection, keeping Old Gen tidy without doing a normal Old Gen GC collection. When your memory is less than this percent, old gen won't even be included in 'mixed' collections. Mixed are not as heavy as a full old collection, so having small incremental cleanups of old keeps memory usage light.
    
    Default is 65 to 85 depending on Java Version, we are setting to 90 to ensure we reclaim garbage in old gen as fast as possible to retain as much free regions as we can.
    
5.  **G1ReservePercent=20:**  MC Memory allocation rate in up-to-date versions is really insane. We run the risk of a dreaded "to-space exhaustion" not having enough memory free to move data around. This ensures more memory is waiting to be used for this operation. Default is 10, so we are giving another 10 to it.
    
6.  **MaxTenuringThreshold=1:**  Minecraft has a really high allocation rate of memory. Of that memory, most is reclaimed in the eden generation. However, transient data will overflow into survivor. Initially played with completely removing Survivor and had decent results, but does result in transient data making its way to Old which is not good.Max Tenuring 1 ensures that we do not promote transient data to old generation, but anything that survives 2 passes of Garbage Collection is just going to be assumed as longer-lived.
    
    Doing this greatly reduces pause times in Young Collections as copying data up to 15 times in Survivor space for a tenured object really takes a lot of time for actually old memory. Ideally the GC engine would track average age for objects instead and tenure out data faster, but that is not how it works.
    
    Considering average GC rate is 10s to the upwards of minutes per young collection, this does not result in any 'garbage' being promoted, and just delays longer lived memory to be collected in Mixed GC's.
    
7.  **SurvivorRatio=32:**  Because we drastically reduced MaxTenuringThreshold, we will be reducing use of survivor space drastically. This frees up more regions to be used by Eden instead.
    
8.  **AlwaysPreTouch:**  AlwaysPreTouch gets the memory setup and reserved at process start ensuring it is contiguous, improving the efficiency of it more. This improves the operating systems memory access speed. Mandatory to use Transparent Huge Pages
    
9.  **+DisableExplicitGC:**  Many plugins think they know how to control memory, and try to invoke garbage collection. Plugins that do this trigger a full garbage collection, triggering a massive lag spike. This flag disables plugins from trying to do this, protecting you from their bad code.
    
10.  **MaxGCPauseMillis=200:**  This setting controls how much memory is used in between the Minimum and Maximum ranges specified for your New Generation. This is a "goal" for how long you want your server to pause for collections. 200 is aiming for at most loss of 4 ticks. This will result in a short TPS drop, however the server can make up for this drop instantly, meaning it will have no meaningful impact to your TPS. 200ms is lower than players can recognize. In testing, having this value constrained to an even lower number results in G1 not recollecting memory fast enough and potentially running out of old gen triggering a Full collection. Just because this number is 200 does not mean every collection will be 200. It means it can use up to 200 if it really needs it, and we need to let it do its job when there is memory to collect.
    
11.  **+ParallelRefProcEnabled:**  Optimizes the GC process to use multiple threads for weak reference checking. Not sure why this isn't default...
    
12.  **G1RSetUpdatingPauseTimePercent=5:**  Default is 10% of time spent during pause updating Rsets, reduce this to 5% to make more of it concurrent to reduce pause durations.
    
13.  **G1MixedGCCountTarget=4:**  Default is 8. Because we are aiming to collect slower, with less old gen usage, try to reclaim old gen memory faster to avoid running out of old.
    
14.  **G1HeapRegionSize=8M+:**  Default is auto calculated. SUPER important for Minecraft, especially 1.15, as with low memory situations, the default calculation will in most times be too low. Any memory allocation half of this size (4MB) will be treated as "Humongous" and promote straight to old generation and is harder to free. If you allow java to use the default, you will be destroyed with a significant chunk of your memory getting treated as Humongous.
    
15.  **+PerfDisableSharedMem:**  Causes GC to write to file system which can cause major latency if disk IO is high -- See  [https://www.evanjones.ca/jvm-mmap-pause.html](https://www.evanjones.ca/jvm-mmap-pause.html)
    

## Using Large Pages[​](https://docs.papermc.io/paper/aikars-flags#using-large-pages "Direct link to heading")

For Large Pages -- It's even more important to use -Xms = -Xmx! Large Pages needs to have all the memory specified for it, or you could end up without the gains. This memory will not be used by the OS anyway, so use it.

Additionally, use these flags (Metaspace is Java 8 Only, don't use it for Java7): `-XX:+UseLargePagesInMetaspace`

### Transparent Huge Pages[​](https://docs.papermc.io/paper/aikars-flags#transparent-huge-pages "Direct link to heading")

Controversial feature but may be usable if you can not configure your host for real HugeTLBFS. Try adding  but it's extremely important you also have AlwaysPreTouch set. Otherwise, THP will likely hurt you. We have not measured how THP works for MC or its impact with AlwaysPreTouch, so this section is for the advanced users who want to experiment.`-XX:+UseTransparentHugePages`
