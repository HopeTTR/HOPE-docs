Git important commands
=======================

.. toctree::
   :maxdepth: 2


git status
git branch
git stash
git status
git pull origin wdmhd
git stash pop
go to that conflict file look for >>>> edit they way u want save it then
git add path to that file


##### for checking the difference 

git difftool HEAD Simulation_initBlock.F90
git difftool HEAD <path_to_file_or_file_name>
inside it can do `esc` then `za` to see full code of unchanged part.

whenever did some change first commit it but first add it and then push it


git add flash.par
git add <file_name>
git commit -m"added resistivity in flas.par"
git commit -m"message"
git push origin wdmhd

when some changes has commited from amin and u want to pull.

get merge main
git fetch origin

if shows uptodate and nothings changes then, try

git merge origin/main

then for safe side 

git pull origin wdmhd
git push origin wdmhd

To add shortcuts for git, go to config file
~/.gitconfig
and add )available on zulip)


