# Minecraft Server Runbook

This is a guide to common administrative tasks on the Minecraft server.

## Stopping the Server

The Minecraft server is running in a screen session.
This allows you to start the server, then disconnect and keep the server running in the background.
To attach to the screen session, run...

    screen -r minecraft

You should now see the Minecraft server console, and a log of activity on the server.

To stop the server, run...

    stop

This will drop you back to the shell prompt. You are still within the screen session.

If you would like to detach from the screen session (i.e. leave the session running in the background), you can press `Ctrl-a` then `d`.
You can later attach to the screen session again by running `screen -r minecraft`.
This is the recommended option.

If you would like to stop the screen session, run `exit`.
If you do this, you will need to start a new screen session later before you start the server again.

## Starting the Server

Attempt to attach to the screen session.

    screen -r minecraft

This will attach to an existing screen session.

If you get an error message, go to to the Screen Troubleshooting section.

Once you are in the screen session, you can start the server by running the following commands.

    cd ~
    ./run

This will run the `run` script.
This script will automatically restart the server if it exits with an error, for example, when the server crashes.
This script will not restart the server if the server exits cleanly, for example, if the server stops due to someone issuing the `stop` command.

Once the server is running, detach from the screen session by pressing `Ctrl-a` then `d`.

## Screen Troubleshooting

If you are not able to attach to the screen session with `screen -r minecraft`, there are a couple common causes.

### No Screen Session Running

If `screen -r minecraft` gives you the following output...

    hayden@localhost:~$ screen -r minecraft
    There is no screen to be resumed matching minecraft.

... it's possible there are no screen sessions running.
You can check by running the following command.

    screen -ls

If it gives you output like this...

    hayden@localhost:~$ screen -ls
    No Sockets found in /run/screen/S-hayden.

... that means there are no screen sessions, and you need to create one.

Create a screen session with the name `minecraft` with the following command.

    screen -S minecraft

This will create the screen session and attach to it.
You can now start the server, or continue with whichever task you were attempting.

### A Screen Session Exists with the Wrong Name

If `screen -r minecraft` gives you the following output...

    hayden@localhost:~$ screen -r minecraft
    There is no screen to be resumed matching minecraft.

... it's possible a screen session is running, but with the wrong name.

Check for running screen sessions with the following command.

    screen -ls

If there are running screen sessions, you will see output similar to this.

    hayden@localhost:~$ screen -ls
    There is a screen on:
            3812.nuncruft   (03/28/2020 05:52:48 PM)        (Detached)
    1 Socket in /run/screen/S-hayden.

This says that there is one screen session running with the name `nuncruft`.
It's also possible for there to be multiple screens running simultaneously.

If you see this, there may already be a Minecraft server, or something else, running in this screen.
You can attach to this screen to see what is running there with the following command.

    screen -r <screen name>

If there is a Minecraft server running in this screen, stop it with the `stop` command, then exit the screen session with `exit`.
Confirm that the screen session is no longer active with `screen -ls`.
Once this is resolved, you can create a screen session with the proper name with the following command.

    screen -S minecraft

This will create the screen session and attach to it.
You can now start the server, or continue with whichever task you were attempting.
