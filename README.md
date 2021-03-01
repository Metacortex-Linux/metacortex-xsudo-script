# metacortex-xsudo-script

This method allow to replace gksudo with bash script and pkexec.

Create xsudo file:

    touch xsudo

Make it executable:

    chmod +x xsudo

Insert this:

    #!/bin/bash
    if [ -z $1 ]; then
     echo -e "at least 1 argument required!\n" >> /dev/stderr
     exit 1
    fi
    COMMAND=$1
    shift #shift first arg
    for ARG in "$@"
    do
     if [ -z "$ARGS" ]; then
      ARGS="$ARG"
     else
      ARGS="$ARGS $ARG"
     fi 
    done
    ARGS=\'$ARGS\'
    eval pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY $COMMAND $ARGS
    exit 0

Now you can use xsudo script to run application as root. Example:

    xsudo geany /etc/shadow

This will open /etc/shadow with geany editor.
