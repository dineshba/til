## exec (buildin command)

We can use exec for two use cases (as far as I learned today :-P)

#### To create independent shell from current shell

Usual way:
```bash
$ bash # created a bash shell
$ #do whatever you wanted
$ exit # will go back to the shell which it created
 ```

Using exec:
```bash
$ exec bash #created a bash shell and killed the current shell
$ #do whatever you wanted
$ exit  # will not go back to the shell which it created.
```

#### To change output/error stream of current process

```bash
echo 'Hi'        # printed in output stream
echo 'Hi' 1>&2   # printed in error stream (output -> error)
exec 2>/dev/null # redirect error stream of current process to null (error -> null)
echo 'Hi' 1>&2   # will not get printed (as output -> error -> null)
exec 1>/dev/null # redirect output stream of current process to null (output -> null)
echo 'Hi' # will not get printed (as output -> null)
```