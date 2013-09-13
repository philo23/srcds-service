# srcds-service

Created to be able to quickly manage a Source Dedicated Server using `service srcds {start|stop|restart|status}` / `/etc/init.d/srcds {start|stop|restart|status}` command in Ubuntu with a simple config file without any `screen` or `tmux` processes.


## Installing

1. Locate your SRCDS/SteamCMD install, by default its configured as `/opt/steam`, and then update the DIR variable in `srcds`.
2. I'd highly recommend creating a seperate user to run SRCDS from, say "steam". `adduser steam` should setup everything you need. Then set which ever user and group you want SRCDS to run as in the USER and GROUP variables in `srcds_defaults`. Make sure this user can execute the `srcds_run` executable.
3. Setup the command line options that will be passed onto SRCDS, by default its setup as a Team Fortress 2 server with a maximum of 14 players and `sv_pure` enabled. `-norestart` is required to stop SRCDS from restarting it self when you try to stop it.
4. Setup the CVars to be set on start up, by default it's setup to run the map `cp_badlands`.
5. Copy the config file `sudo cp srcds_defaults /etc/defaults/srcds` with the correct permissions: `sudo chmod 644 /etc/defaults/srcds`
6. Copy the service file `sudo cp srcds /etc/init.d/srcds` with the correct permissions: `sudo chmod 755 /etc/init.d/srcds`


## Usage

* Start: `sudo service srcds start`
* Stop: `sudo service srcds stop`
* Restart: `sudo service srcds restart`
* Status: `sudo service srcds status`

You can also use `sudo /etc/init.d/srcds {start|stop|restart|status}` if you prefer.


### Checking its properly installed

1. First run `sudo service srcds start` to start SRCDS.
2. Next open `top` and check that you can see `srcds_linux` some where in the list, note down the related number in the PID column and press `Q` to quit.
3. Now run `cat /var/run/srcds.pid` and you should see the same number you noted down in step 2.
4. Run `sudo service srcds status` which should tell you ` * srcds is running`.
5. Now run `sudo service srcds stop` which will stop SRCDS.
6. Check `top` again to see that `srcds_linux` has disappeared from the list
7. Finally run `sudo service srcds status` which will now tell you ` * srcds is not running`
8. You're all done!


## Credits

Inspired by [stevenbenner/srcds-service](https://github.com/stevenbenner/srcds-service) after wanting to run SRCDS without using screen.

And the [Valve Developer Wiki](https://developer.valvesoftware.com/wiki/Main_Page) for containing lots of useful (but well hidden) information.
