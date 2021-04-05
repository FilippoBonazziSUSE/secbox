# Secbox

TODO

[...]

## SSHFS

In order to get some of the internal tools properly working you need to provide NFS exports in fixed mountpoint (`/mounts`).
Secbox supports nfs mount via `--nfs` and will ask for your user password to get enough permissions to successfully mount the nfs shares.

A better approach is to use `--sshfs` option. Secbox can use sshfs (installed in the container) to mount `wotan.suse.de:/mounts` with the container at `/mounts`. In order to work you need to configure your local ssh client to be able to access wotan with the command-line `ssh wotan`, to do that you need to configure your `~/.ssh/config`. You can use the following stanza template

    Host wotan
        HostName wotan.suse.de
        User <YOUR_USERNAME>
        PreferredAuthentications publickey
        IdentityFile /path/to/your/key

you could avoid IdentityFile in case your key is loaded in the ssh-agent, in this case secbox will be able to get it from there.
If you encotuner issues, try to delete the container and create once again via `secbox --destroy` and then use `secbox` again with any command.