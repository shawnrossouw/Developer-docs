# Command to copy files via the rsync transfer protocol from the terminal.

```bash
rsync -r --progress /Users/shawn/websites/meyrbros-splash/* meyerk@meyerbros.co.za:/usr/home/meyerk/public_html
```

## Legend

```bash
Origin : /Users/shawn/websites/meyrbros-splash/* (insert space)
Destination : meyerk@meyerbros.co.za:/usr/home/meyerk/public_html
```
```bash
rsync -r = recursive
--progress = displays progress of file transfer
```

## EXAMPLE

```bash
rsync -r --progress /Users/mj/assets/migrate-db-files/*(space) meyerhpntx@meyerbros.dev.magneticcreative.co.za:/usr/home/meyerhpntx/public_html/wp-content/plugins
```

Go to the file you want to rsync and type PWD - then copy the path
