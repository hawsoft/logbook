# setup gitweb
### 1.install apache,gitweb,perl_uri

### 2.change /etc/apache2/apache2.conf
```
Listen 8010

LoadModule cgi_module /usr/lib/apache2/mod_cgi.so

User nobody
Group root

<IfModule alias_module>
    ScriptAlias /git "/www/cgi-bin/gitweb.cgi"
    ScriptAlias /repo/ /usr/lib/git-core/git-http-backend/
</IfModule>

<Directory "/www">
    Options Indexes FollowSymLinks ExecCGI
    Require all granted
    AddHandler cgi-script .cgi    
</Directory>

<Location /repo>
    AuthType Basic
    AuthName "Private Git Access"
    AuthUserFile /git-repo/userfile
    Require valid-user
</Location>
```

### 3.change /www/cgi-bin/gitweb.cgi

```
our $projectroot = "/git-repo/projects";
```

# setup file share

### 1.change /etc/apache2/apache2.conf
```
<IfModule alias_module>
    Alias /files/ "/mnt/sda1/web-files/"
</IfModule>

<Directory "/mnt/sda1/web-files/">
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
```
