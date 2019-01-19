# docker-mariadb/mysql

> I want my databases (MySQL/Mariadb) automatic backup, that's all. 

In order to realize it, I can create my Dockerfile and use `CMD` or `ENTRYPOINT` directive to do it. But the official have used them.

Fortunately, the official Dockerfile (mysql/mariadb) have a convinience for us.
The official Dockerfile ENTRYPOINT["docker-entrypoint.sh"] will run the script in /docker-entrypoint-initdb.d
``` bash
for f in /docker-entrypoint-initdb.d/*; do
    case "$f" in
        *.sh)     echo "$0: running $f"; . "$f" ;;
        *.sql)    echo "$0: running $f"; "${mysql[@]}" < "$f"; echo ;;
        *.sql.gz) echo "$0: running $f"; gunzip -c "$f" | "${mysql[@]}"; echo ;;
        *)        echo "$0: ignoring $f" ;;
    esac
    echo
done
```
