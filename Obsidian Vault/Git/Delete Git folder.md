# Delete Git folder
#git

[Trying to remove my .git folder and 'rm -r .git --force' is not working](https://stackoverflow.com/questions/55320699/trying-to-remove-my-git-folder-and-rm-r-git-force-is-not-working)

Solution
```shell
chmod -R +w <repo>
rm -r <repo>
```


Error example:

```shell
(sandbox-17-02-22)  ginalamp@Ginas-MacBook-Air  ~/Workspace  rm -r test
override r--r--r-- ginalamp/staff for test/.git/objects/bb/f6be86079906b2347dd0e9b590ff19043fdd6a? ya
```
