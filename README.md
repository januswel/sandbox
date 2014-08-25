sandbox
=======

git sandbox

Setting upstream for local branch to remote branch
--------------------------------------------------

```zsh
git checkout <local branch>
git push -u origin <remote branch>
```

or

```zsh
git checkout <local branch>
git branch -u origin <remote branch>
```


Rebasing a remote branch
------------------------

```zsh
> git branch -vv
  extended 5b2bc12 [origin/extended] Add file c
* master   5ea8c19 [origin/master] Modify a
```

```zsh
> git log --graph --all --oneline --decorate
* f6b09b0 (HEAD, master) Modify a
| * 5b2bc12 (origin/extended, extended) Add file c
|/  
* 5ea8c19 (origin/master, origin/HEAD) Modify a
* d1f1d0e Add content of b
* 19e4ca9 Add commands to set upstream for local to remote
* 4f74315 Add content of a
* 30fd1cf Add files a and b
* 66fa74e Initial commit
```

First, at the branch "extended", rebase master.

```zsh
> git co extended
> git rebase master
```

Now, commit history is below. See the commit id of the local branch "extended"
HEAD and the one of the remote branch "origin/extended". There is a difference.
The local one is <ffecadd> but the remote one is <5b2bc12>.

```zsh
> git log --graph --all --oneline --decorate
* ffecadd (HEAD, extended) Add file c
* f6b09b0 (master) Modify a
| * 5b2bc12 (origin/extended) Add file c
|/  
* 5ea8c19 (origin/master, origin/HEAD) Modify a
* d1f1d0e Add content of b
* 19e4ca9 Add commands to set upstream for local to remote
* 4f74315 Add content of a
* 30fd1cf Add files a and b
* 66fa74e Initial commit
```

Then, use below command to push rebased local branch.

```zsh
git push -f origin extended
```

```zsh
> git log --graph --all --oneline --decorate
* ffecadd (HEAD, origin/extended, extended) Add file c
* f6b09b0 (master) Modify a
* 5ea8c19 (origin/master, origin/HEAD) Modify a
* d1f1d0e Add content of b
* 19e4ca9 Add commands to set upstream for local to remote
* 4f74315 Add content of a
* 30fd1cf Add files a and b
* 66fa74e Initial commit
```

As you know, this operation overwrites remote branch's history. So don't push
to remote branch that is shared other members. Commits by your members will
come to nothing.
