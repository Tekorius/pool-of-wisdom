# Supervisor.d

Supervisor.d is a queue thingy for the server. Not the best one, but
it is used by [JMSJobQueueBundle](https://github.com/schmittjoh/JMSJobQueueBundle).

## Guides

### Restarting

It may happen that the JMSQueue stops for no reason. To check if the queue is running you can go to your configured jms queue url and check if there old pending jobs.

If there are any **old** pending jobs, it may be that the queue has stopped. One of the causes can be supervisor.d service in the server.

Here's how to restart it

1. SSH to the offending server
2. Check if supervisor is running: `ps aux | grep supervisor`
3. Start or restart supervisor
	
    a) If supervisor is running, restart the service:
    `sudo service supervisor restart`

	b) If supervisor is not running, start the service:
    `sudo service supervisor start`
    
4. Check the queue again to see if the problem is solved

TLDR:

```
ssh yo.srv.ip
ps aux | grep supervisor
sudo service supervisor restart
```

