# svn-commands
Useful SVN commands for daily tasks


## Deleted files

Get a list of relative paths of deleted files in `$SVNBASE` from revision `$FROM`

`svn diff --summarize -r $FROM:HEAD $SVNBASE | grep "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##"`


## Modified files

Get a list of relative paths of modified/added files in `$SVNBASE` from revision `$FROM`

`svn diff --summarize -r $FROM:HEAD $SVNBASE | grep -v "D  " | awk '{ print $2 }' |  sed -e "s#$SVNBASE/##"`


