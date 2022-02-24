# Revert Changes on Git

## Reverting changes from working directory

If you have a bug in working directory and want to restore code from local repository.

```sh
   git restore <file_name> 
          or
   git checkout -- <file_name>
```

> ***Note***: `You can even remove changes manually by deleting lines, but in case of multiple files and you don’t know which lines to remove this command is really helpful.`

## Reverting changes from Staging Area

If you already added files with bug to staging area and and to unstage and restore code from local repository.

```sh
   git restore --staged <file_name>  #to revert changes from Staging area to working directory  
   git restore <file_name> #to revert changes from working directory  
```

## Reverting changes from Local Repository

If the file with bug already added to local repository.

```sh
   git reset HEAD~           # to revert changes from local repo to working directory
   git restore <file_name(s)> # to revert changes from working directory  
```

## Revert changes from Remote Repository

We dont have direct way to do this.
