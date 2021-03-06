# check_mongo_replica_stat README

# IMPETUS

A few days after setting up my first <a href="http://www.mongodb.org/">Mongo</a> Replica set, I found one of the
members had become stale.  It had actually been stale for four days.  I looked around and couldn't find
a script to monitor the replica set with <a href="http://www.nagios.org/">Nagios</a>.

My solution simply pulls the status from the Mongo admin web server and parses it.

# NOTES

Simply save check_mongo_replica_stat.rb with the rest of your Nagios plugins.  I save mine in
/usr/lib/nagios/local-plugins.

Create a Nagios command

    define command {
	    command_name    check-mongo-replica-set
	    command_line    /usr/lib/nagios/local-plugins/check_mongo_replica_stat.rb
	    # Note, you can pass --host and --port as well
    }


Then create a service check

    define service {
        host				            sample_host
        service_description             Mongo Replica Status
        check_command                   check-mongo-replica-set
	    notification_interval		    5
        use                             generic-service
    }

Reload your Nagios configuration and the new monitor should be running.

# License

 Copyright (C) 2011 Tony Nelson.

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
