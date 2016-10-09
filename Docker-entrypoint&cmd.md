##Difference between Docker entrypoint and CMD 



Its simple. Whatever you fill in CMD will be given to the ENTRYPOINT as an argument.

For ex: If you have a dockerfile like this.

    CMD ["-tupln"]
    ENTRYPOINT ["/usr/bin/netstat"]

and when you run the container without any other command ( For ex:#docker run ….. )

The above instruction basically make it something like “netstat -tulpn” for the container to execute.

Also there is a default entrypoint for each container which is nothing but “/bin/sh -c”

However note that, the CMD used at end of the ” #docker run … .. ” will overwrite the default command



###You have three variables: ENTRYPOINT, CMD and CONTAINERARGS


**Rule #1: Existing CONTAINERARGS replace CMD**

**Rule #2: If ENTRYPOINT exists, the string “ENTRYPOINT CMD” will be executed – If ENTRYPOINT does not exist, the**

**string “CMD” will be executed. – If CMD does not exist but ENTRYPOINT, string “ENTRYPOINT” will be executed.**



###In other other other words:

      ENTRYPOINT + CMD => exec $($ENTRYPOINT $CMD)

      CMD => exec $($CMD)

      ENTRYPOINT + CMD + CONTAINERARGS => exec $($ENTRYPOINT $CONTAINERARGS)

      CMD + CONTAINERARGS => exec $($CONTAINERARGS)

      ENTRYPOINT + CONTAINERARGS => exec $($ENTRYPOINT $CONTAINERARGS)

      ENTRYPOINT => exec $($ENTRYPOINT)

      CONTAINERARGS => exec $($CONTAINERARGS)

      NOTHING => exec NOTHING