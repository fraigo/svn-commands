# svn-commands
Useful SVN commands for daily tasks


## Deleted files

Get a list of relative paths of deleted files in `$SVNBASE` from revision `$FROM`

`svn diff --summarize -r $FROM:HEAD $SVNBASE | grep "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##"`


## Modified files

Get a list of relative paths of modified/added files in `$SVNBASE` from revision `$FROM`

`svn diff --summarize -r $FROM:HEAD $SVNBASE | grep -v "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##"`

## Export files modified in `$SVNBASE` from revision `$FROM` 

```bash
export FROM=$1
export SVNBASE=$2
DELFILES=$(svn diff --summarize -r $FROM:HEAD $SVNBASE | grep "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##")
for f in $DELFILES ; do
	echo "deleting $f"
	rm -rf "./$f"
done
FILES=$(svn diff --summarize -r $FROM:HEAD $SVNBASE | grep -v "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##")
for f in $FILES ; do
	mkdir -p $(dirname "./$f")
	svn export --force "$SVNBASE/$f" "./$f"
done
```

