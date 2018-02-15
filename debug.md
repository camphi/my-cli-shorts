## Git

remove merged branches
- git branch --merged dev | grep -v -E "(master|dev)" | xargs -n 1 git branch -d

If file is tracked
- git ls-files {}
