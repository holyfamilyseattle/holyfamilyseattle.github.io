# holyfamilyseattle.github.io

For running the website locally, install hugo and run the below command from project directory.

hugo server -D 

For update the underlying theme (alpha-church)

-  De-initialize the theme submodule from themes directory

git submodule deinit alpha-church

- Delete alpha-church directory from themes

- Remove alpha-church directory recursively from .git repository

IT-MB5:themes q1440401$ pwd
/Users/ajith/IdeaProjects/holyfamilyseattle.github.io/.git/modules/themes
IT-MB5:themes q1440401$ rm -rf alpha-church

- Add the theme back as sub-module

IT-MB5:themes ajith$ git submodule add https://github.com/holyfamilyseattle/alpha-church
Cloning into '/Users/ajith/IdeaProjects/holyfamilyseattle.github.io/themes/alpha-church'...
remote: Enumerating objects: 3059, done.
remote: Counting objects: 100% (390/390), done.
remote: Compressing objects: 100% (230/230), done.
remote: Total 3059 (delta 186), reused 283 (delta 117), pack-reused 2669
Receiving objects: 100% (3059/3059), 9.34 MiB | 25.44 MiB/s, done.
Resolving deltas: 100% (1700/1700), done.

