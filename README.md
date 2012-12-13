# Munin ActiveMQ plugin

Display queues status graphs in Munin.

# Requirements

## Perl modules

`WWW::Mechanize`

`XML::Simple`

# Plugin install

## Debian


#### Download script

download `queue_` script to `/usr/share/munin/plugins/queue_` as root

~~~
	git clone git@github.com:labynocle/munin-activemq-plugin.git
~~~

#### Install requirements

Test if your system has a required modules by the following command:

~~~
	/usr/share/munin/plugins/queue_ autoconf
~~~

as result you should have yes, else you can install them:

_System_:

	apt-get install libwww-mechanize-perl

	apt-get install libxml-simple-perl

_by user_:

	perl -MCPAN -e "install WWW::Mechanize"

	perl -MCPAN -e "install XML::Simple"


you can also use `force install`:

	perl -MCPAN -e "force install XML::Simple"


!! You might have a lot of dependencies to install. !!

=> *TODO*: use another perl lib with less dependencies

#### Create symlink

Create a symlink to this script:

	cd /etc/munin/plugins/

	ln -s /usr/share/munin/plugins/queue_ /etc/munin/plugins/queue_<name.of.my.queue>

if you want display multi-graph for the same ActiveMQ queue try this:

	ln -s /usr/share/munin/plugins/queue_ /etc/munin/plugins/queue_<name.of.my.queue>--<what_you_want_to_display>

    what_you_want_to_display: could be equal to dequeueCount,enqueueCount and size

#### Configure graphs

Configure the plugin environment variables:

In your Munin-node, edit the file `munin-node` in _/etc/munin/plugin-conf.d/_ and add the following lines:

	[queue_*]
		env.host <my.activemq_host>
		env.port <my.activemq.port>
		env.category activemq_queues

here an exemple:
	[queue_*]
		env.host 127.0.0.1
		env.port 8161
		env.category activemq_queues

#### Test configuration

Test your config:
	munin-run /etc/munin/plugins/queue_<name.of.my.queue>

#### Restart Node

Restart your Munin-node:
	/etc/init.d/munin-node restart
