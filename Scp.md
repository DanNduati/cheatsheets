# Secure Copy cheatsheet
### Commands

```bash
$ scp file user@host:/path/to/file                        # copying a file to the remote system using scp command
$ scp user@host:/path/to/file /local/path/to/file         # copying a file from the remote system using scp command
```

```bash
$ scp file1 file2 user@host:/path/to/directory            # copying multiple files using scp command
$ scp -r /path/to/directory user@host:/path/to/directory  # Copying an entire directory with scp command
```