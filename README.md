# fbsd-zabbix

mkdir /root/zabbix-agent && cd /root/zabbix-agent

fetch http://www.zabbix.com/downloads/3.0.4/zabbix_agents_3.0.4.freebsd8_2.i386.tar.gz

tar -xzvf  zabbix_agents_3.0.4.freebsd8_2.i386.tar.gz

mkdir /usr/local/bin
mkdir /usr/local/sbin
mkdir /usr/local/etc

cp bin/* /usr/local/bin
cp sbin/* /usr/local/sbin
cp conf/zabbix_agentd.conf /usr/local/etc

/etc/rc.conf строку:
zabbix_agentd_enable="YES"

mkdir /usr/local/etc/rc.d
cd /usr/local/etc/rc.d

vi zabbix_agentd.sh
_______________________________________________________
#!/bin/sh

# REQUIRE: DAEMON
# PROVIDE: zabbix_agentd

. /etc/rc.subr

name="zabbix_agentd"
rcvar=`set_rcvar`
command="${prefix:-"/usr/local"}/sbin/${name}"

load_rc_config ${name}
run_rc_command "$1"
________________________________________________________

chmod 0754 zabbix_agentd.sh

adduser zabbix


