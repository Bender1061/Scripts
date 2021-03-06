# Troubleshooting oref0-setup script process

## Re-run the script again

You won't hurt anything by running the script (step 2) multiple times, as long as you name it something different. If you already have a working loop and are testing the setup scripts, just make sure to comment out in cron the loop you don't want running.

## Should I enact cron?

Cron is the scheduler that runs the loop. I.e. this is the automation feature to automate your closed loop. If you're using a test pump, it's pretty safe to go ahead and automate your loop. But if you're not sure, you can always come back and do this later.

If you're troubleshooting and looking to use `openaps` manually, cron must be momentarly disabled to free access to local resources.  To check if cron is running use `crontab -e` or `crontab -l`.  If you see a file filled with content, chances are cron is enabled.

To stop cron'd jobs and enter an openaps command:  `killall -g openaps; openaps <whatever>` 

If you'd like to run multiple commands without having to do `killall -g openaps; ` before each one, you can run `sudo service cron stop` first.
<br>
To start cron: `sudo service cron start`

To prevent cron running on initial boot, either clear the `crontab -e` file or "comment out" (`#`) each line of the crontab file.  If you've cleared the crontab file, but would like to enable cron'd tasks, rerun the initial setup script (step 2) and indicate you'd like to use cron.  This will regenerate the configuration.

## How do I know if it is working?

* Check your pump to see if it is setting temp basals.
* "Tail" the pump log to see what is is doing: `tail -F /var/log/openaps/pump-loop.log`
* Check Nightscout to see if it is updating with your information
* Run commands manually (check out the [openaps toolkit basics here](http://openaps.readthedocs.io/en/latest/docs/openaps-guide/core/medtronic.html#openaps-use-pump)) 

## It's not working yet:

* Check to make sure that your pump is in absolute and not % mode for temp basals.
* Did you put in the right SN for the pump? Should be numbers only...
* Check to make sure your carelink and/or radio stick is plugged in.
* Check to make sure your receiver is plugged in, if you're plugging a receiver in.
* Don't have data in Nightscout? Make sure there is no trailing slash `/` on the URL that you are entering and that the API secret is correct.
* Check and make sure your receiver is >50% charged (if battery low, it may drain the Pi and prevent it from operating).
* Check and make sure your pump is in range of the radio stick.
* Check and make sure your pump is not suspended or stuck in rewind or prime screens. If it's a test pump, you don't even have to fill a reservoir, but put your pinky finger or eraser-end of a pencil in for slight pressure when priming so the pump will "sense" it and stop. Make sure to back out of the prime screen.
