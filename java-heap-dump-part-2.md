If you want to generate the heap dump programmatically, add the following in your env variable or define it in java execution command. 


If you are using it in the env variable .

    HEAP_OPTS="-XX:-UseGCOverheadLimit -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp"


Add the environment variable in the java execution path. 

    java --<jar file> <main class>   $HEAP_OPTS.

When the applications fails due to out of memory exception, it will create a dump in the /tmp path. You can analyze it using     eclipse memory analyzer tool.
