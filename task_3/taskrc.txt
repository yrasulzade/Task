#!/bin/sh

. /etc/init.d

[ -f /usr/local/sbin/taskrc.sh ] || exit 0

case "$1" in

        start)
                echo "script started...."
                /usr/local/sbin/taskrc.sh &
                echo "--------------------"
                touch /var/lock/subsys/taskrc
                ;;
        stop)
                echo -n "stopping"
                killall -q -9 taskrc.sh &
                rm -f /var/lock/subsys/taskrc
                ;;
        status)
                status taskrc
                ;;
        restart|reload)
                $0 stop
                $0 start
                ;;
        *)
                echo "start, stop, restart|reload, status"
                exit 1
esac

exit 0

