## Git

Remove merged branches (-d locally)
- ``git branch --merged dev | grep -v -E "^\*?\s+(master|dev)" | xargs -n 1 git branch -d``

If file is tracked
- ``git ls-files {}``

Modified files between 2 branches
- ``git diff {} | grep -E "^diff --git" | cut -c14-``

Force checkout/pull origin/master
- ``git reset --hard origin/master``

## Bash

Convert images
- `find . -type f \( -name "*.jpg" -o -name "*.png" -o -name "*.gif" \) -exec du -ch {} \+ | tail -1 `
- `find . -type f -name "*.jpg" -exec convert {} -sampling-factor 4:2:0 -strip -quality 85 -interlace JPEG -colorspace RGB {} \;`
- `find . -type f \( -name "*.png" -o -name "*.gif" \) -exec convert {} -strip {} \;`

## PHP

Install different version of PHP
- `add-apt-repository ppa:ondrej/php && apt-get update`
- `sudo update-alternatives --set php /usr/bin/php7.2`

## Laravel

Show Queries inside Tinker
- `DB::listen(function ($query) { dump($query->sql); dump($query->bindings); dump($query->time); });`
