# Handle remote files via only sftp access

Assuming I have only sftp access to a remote file system. Then two very helpful tools are:

## access via `sshfs`

You can mount a directory via [sshfs](https://github.com/libfuse/sshfs), and the host only sees a sftp protocol.
That way you have all the comfort of file system access, to find lists of interesting files with your buddy Bash.
Just remember:

```
sshfs [user@]hostname:[directory] mountpoint
fusermount -u mountpoint
```

## passing commands into `sftp`

Since the mysterious batch mode expects non-interactive authorization: Just pass the arguments via input redirection!
So if you found a list of interesting files via sshfs, for me it is a bit quicker to download not via FUSE but directly via sftp:

```
 sft username@example.com < commands.txt
```

where you can update the filenames in `commands.txt` via the tool of your choice to include some `get -r ... somewhere` fun.

