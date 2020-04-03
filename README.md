## Vim

Disable vim automatic visual mode on mouse select
- `mouse-=a`

## Git

Remove merged branches (-d locally)
- ``git branch --merged dev | grep -v -E "^\*?\s+(master|dev)" | xargs -n 1 git branch -d``

If file is tracked
- ``git ls-files {}``

Modified files between 2 branches
- ``git diff {} | grep -E "^diff --git" | cut -c14-``

Force checkout/pull origin/master
- ``git reset --hard origin/master``

Checkout/Rm by Regex
- ``git status --porcelain | cut -c 4- | grep {} | xargs git checkout``
- ``git status --porcelain | cut -c 4- | grep {} | xargs rm``

Compare with Meld
- ``git difftool -gdt meld``

Revert deleted files from previous commit
- ``git log --diff-filter=D --summary -n1 | grep -E '^ delete' | cut -d\  -f5- | xargs git checkout {} --``

Return to origin
- ``git reset --hard origin/<branch_name>``

## Git-Svn

maintaining a read only svn mirror of a git repository
- http://www.kerrybuckley.org/2009/10/06/maintaining-a-read-only-svn-mirror-of-a-git-repository/
```bash
git clone ~git/repositories/foo/mainline.git ~git/repositories/svn-mirror/foo
cd ~git/repositories/svn-mirror/foo
vim .git/config
...
[svn-remote "svn"]
	url = http://svn.example.com/foo/trunk
	fetch = :refs/remotes/git-svn
...
git svn fetch svn
git checkout -b svn git-svn
git merge master
git svn dcommit
git checkout master
git rebase svn
git branch -d svn
...
git svn dcommit
```

## Awk

Csv FPAT
- `(?:[^",]|"(?:[^"]|"")*")*`

## Image

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

## Bash

Remove CR from file with CRLF
 - ``tr -d '\r' < input.file > output.file``

First line to lowercase
 - ``sed -i '1s/.*/\L&/' file.csv``

First line to uppercase
 - ``sed -i '1s/.*/\U&/' file.csv``
 
Php array to bash assoc hash
 - ``arr=($(php -r '$arr = include("arr.php"); foreach($arr as $key => $val){echo " [\"" . addslashes($key) . "\"]=\"" . addslashes($val) . "\" ";    }'));``
 - ``function _php_arr_echo_segment(){php -r '$a=include($argv[1]);foreach(explode(".",$argv[2]) as $s){if(isset($a[$s])){$a=$a[$s];}else{echo $argv[3];exit;}}echo json_encode($a);' -- $1 $2 $3}``

## MySql
Get only one table from MySQL dump
 - ``sed -n -e '/DROP TABLE.*`mytable`/,/UNLOCK TABLES/p' dump.sql``

Get only one table structure from MySQL dump
 - ``sed -n -e '/DROP TABLE.*`mytable`/,/ENGINE/p' dump.sql``
 - ``sed -n -e '/DROP TABLE.*`mytable`/,/;/p' dump.sql``

Quickly load CSV into table
 - ``mysql -p -uusername -e "LOAD DATA LOCAL INFILE 'file.csv' INTO TABLE \`databasename\`.\`tablename\` CHARACTER SET UTF8 FIELDS TERMINATED BY ',' ENCLOSED BY '\"' LINES TERMINATED BY '\n'"``

Replace user for tiggers and views
 - ``sed -e 's/DEFINER=`\w\+`/DEFINER=`{}`/' -i mysqldump.sql``

## JSON
Prettify
```bash
jq <(cat <<EOL
{}
EOL
)
```

## XML
Prettify
```bash
xmllint --format <(cat <<EOL
{}
EOL
)
```

## Magento 2
 Flush All
 - `rm -rf pub/static/_cache/* pub/static/_requirejs/* pub/static/adminhtml/* pub/static/frontend/* generated/* var/di/* var/cache/* var/generation/* var/view_preprocessed/* var/page_cache/* && redis-cli flushall && php bin/magento cache:flush;`
 
 Log
```PHP
$writer = new \Zend\Log\Writer\Stream(BP . '/var/log/test.log');
$logger = new \Zend\Log\Logger();
$logger->addWriter($writer);
$logger->info('Your text message');
```

 Find block that break full page cache
- `grep -rnw 'app/' -e 'cacheable="false"'`

 PhpStorm URNs highlight
- `bin/magento dev:urn-catalog:generate .idea/misc.xml`

## PHP-FPM
 Continue working after giving the 200 OK. https://www.php.net/manual/en/function.fastcgi-finish-request.php
```PHP
session_write_close(); //close the session
fastcgi_finish_request(); //this returns 200 to the user, and processing continues
```
