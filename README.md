## Git

Remove merged branches (-d locally)
- ``git branch --merged dev | grep -v -E "(master|dev)" | xargs -n 1 git branch -d``

If file is tracked
- ``git ls-files {}``

Modified files between 2 branches
- ``git diff {} | grep -E "^diff --git" | cut -c14-``

## Bash

Convert images
- `find . -type f \( -name "*.jpg" -o -name "*.png" -o -name "*.gif" \) -exec du -ch {} \+ | tail -1 `
- `find . -type f -name "*.jpg" -exec convert {} -sampling-factor 4:2:0 -strip -quality 85 -interlace JPEG -colorspace RGB {} \;`
- `find . -type f \( -name "*.png" -o -name "*.gif" \) -exec convert {} -strip {} \;`
