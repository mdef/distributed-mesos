FROM alpine

RUN apk add --update tinc avahi
ADD ./tinc /etc/tinc
RUN sed -i -e "s/^#enable-dbus=yes$/enable-dbus=no/" /etc/avahi/avahi-daemon.conf
CMD avahi-daemon -D && /usr/sbin/tincd -d -D -n mana
 
