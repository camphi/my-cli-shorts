## Git

Remove merged branches (-d locally)
- ``git branch --merged dev | grep -v -E "(master|dev)" | xargs -n 1 git branch -d``

If file is tracked
- ``git ls-files {}``

Modified files between 2 branches
- ``git diff {} | grep -E "^diff --git" | cut -c14-``
