# java-heap

- This is a brief listing of issues faced when using java garbage collection. If your team has a large heap for a large application, there would be gains in peformance when tuning the garbage collection options. Also, note that if the applciation is running on jdk7 or prior, it is likely using the first set of collectors introduced in jdk1.2, whereas if the application is running with jdk1.9 or above, the G1 collector is the default. The G1 collector is available in the JDK7 update 4 and all later JDKs.

# JAVA Garbage Collection

- Java has long relied on Garbage Collection to manage the heap memory over the years starting in java 1.2 in 1998. These have been well known for years and consist of the Young, Tenured and Perm generations. The collectors have consisted of the Parallel, Serial and the Concurent collectors.
- See more details in the java 1.6 documentation.
  https://www.oracle.com/java/technologies/javase/gc-tuning-6.html#available_collectors.selecting

# G1 Collector
- Starting in JDK7 update 4, Oracle introduced the G1 (Garbage First) collector. The idea here being to setup your minimum and maximum heap sizes and let the garbage collection do its job. For starters, the configuration can be set something as below. Additionally, setup the Print logs. THe G1 collector introduces the concept of regions. Each Region can be from 1MB to 32MB.
  ~~~
  java –Xmx1G –Xms1G –XX:+UseG1GC –XX:+PrintGCDetails –XX:+PrintGCTimeStamps JavaApp
  ~~~
# JDK17
  - Note that in jdk15, another option was introduced: ZGC collector. In some scenarios, it performs better than the G1 collector. Note also that with jdk17, both G1 and GCZ perform better than in previous versions of JDK. In general, larger heap sizes will benefit from G1 and GCZ.

# ERRORS

- When analyzing application errors, note that when a "java.lang.OutOfMemoryError",  “GC (Allocation Failure)” or “concurrent mode failure” logs are frequent, this is a sign your application needs to be tuned with the GC collector.

# JDK Options
~~~
G1 (JDK7 update 4):
–XX:+UseG1GC

GCZ (JDK15):
-XX:+UseZGC
~~~

# REFERENCE
- Oracle G1
  https://docs.oracle.com/en/java/javase/17/gctuning/garbage-first-g1-garbage-collector1.html#GUID-ED3AB6D3-FD9B-4447-9EDF-983ED2F7A573
- Java command line inspector:
  https://jacoline.dev/inspect
