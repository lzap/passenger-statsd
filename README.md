# passenger-statsd

A shell script that reads passenger-status and sends statsd packets. Only
gathers totals reported by passenger status.

This is not a daemon, run from cron!

Requires netcat (`nc`) utility and a `grep`.

## Example

For actual output of passenger-status:

    # passenger-status --show=xml
    <?xml version="1.0" encoding="iso8859-1"?>
    <info version="2">
       <process_count>7</process_count>
       <max>12</max>
       <utilization>7</utilization>
       <get_wait_list_size>2</get_wait_list_size>
       <get_wait_list/>
       <supergroups>
          ...
       </supergroups>
    </info>

it sends out a single UDP packet like

    passenger_status.total.process_count:7|g
    passenger_status.total.max:12|g
    passenger_status.total.utilization:7|g
    passenger_status.total.get_wait_list_size:2|g
