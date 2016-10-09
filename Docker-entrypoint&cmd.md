##Difference between Docker entrypoint and CMD 



Its simple. Whatever you fill in CMD will be given to the ENTRYPOINT as an argument.

For ex: If you have a dockerfile like this.

    CMD ["-tupln"]
    ENTRYPOINT ["/usr/bin/netstat"]

and when you run the container without any other command ( For ex:#docker run ….. )

The above instruction basically make it something like “netstat -tulpn” for the container to execute.

Also there is a default entrypoint for each container which is nothing but “/bin/sh -c”

However note that, the CMD used at end of the ” #docker run … .. ” will overwrite the default command