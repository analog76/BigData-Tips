There are 2 ways we can get Java heap dump.

*  Manual heap dump generation  on demand
*  Generate heap dump programmatically when it  throws OOM.

Manual heap dump generation

By default , JVM  provides tools to generate the heap dump.  jmap is the tool to generate heap dump.  

Steps to generate heap dump.

 Find pid of the JVM processes.
 type the following command

    jmap -heap <pid>

 For example,

    jmap -heap 14156


 The result of the above command will be

 	[root@localhost ~]# jmap -heap 14156
	Attaching to process ID 14156, please wait...
	Debugger attached successfully.
	Server compiler detected.
	JVM version is 25.71-b15

	using thread-local object allocation.
	Parallel GC with 8 thread(s)

	Heap Configuration:
	   MinHeapFreeRatio         = 0
	   MaxHeapFreeRatio         = 100
	   MaxHeapSize              = 10737418240 (10240.0MB)
	   NewSize                  = 175112192 (167.0MB)
	   MaxNewSize               = 3578789888 (3413.0MB)
	   OldSize                  = 351272960 (335.0MB)
	   NewRatio                 = 2
	   SurvivorRatio            = 8
	   MetaspaceSize            = 21807104 (20.796875MB)
	   CompressedClassSpaceSize = 1073741824 (1024.0MB)
	   MaxMetaspaceSize         = 17592186044415 MB
	   G1HeapRegionSize         = 0 (0.0MB)

	Heap Usage:
	PS Young Generation
	Eden Space:
	   capacity = 102760448 (98.0MB)
	   used     = 67966272 (64.81768798828125MB)
	   free     = 34794176 (33.18231201171875MB)
	   66.14049794722577% used
	From Space:
	   capacity = 20447232 (19.5MB)
	   used     = 15728688 (15.000045776367188MB)
	   free     = 4718544 (4.4999542236328125MB)
	   76.92331167367789% used
	To Space:
	   capacity = 22544384 (21.5MB)
	   used     = 0 (0.0MB)
	   free     = 22544384 (21.5MB)
	   0.0% used
	PS Old Generation
	   capacity = 497549312 (474.5MB)
	   used     = 479832776 (457.6041946411133MB)
	   free     = 17716536 (16.89580535888672MB)
	   96.43924017726307% used

	17960 interned Strings occupying 1663704 bytes.



To find histogram of this file 


 	jmap -histo:live 14177

	 num     #instances         #bytes  class name
	----------------------------------------------
	   1:         33984        3414648  [C
	   2:          1279         874512  [B
	   3:         33681         808344  java.lang.String
	   4:         17406         556992  java.util.HashMap$Node
	   5:          4490         510496  java.lang.Class
	   6:          3763         295656  [Ljava.lang.Object;
	   7:          7898         252736  java.util.Hashtable$Entry
	   8:          1716         233504  [Ljava.util.HashMap$Node;
	   9:          6373         203936  java.util.concurrent.ConcurrentHashMap$Node
	  10:          5530         158408  [Ljava.lang.String;
	  11:          2781         129608  [I
	  12:          1338         117744  java.lang.reflect.Method
	  13:          5876          94016  java.lang.Object
	  14:          1886          90528  java.util.HashMap
	  15:          1215          77760  java.net.URL
	  ...
	  ...
	  ...
	  ...
	  

