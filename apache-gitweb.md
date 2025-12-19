# install apache,gitweb,perl_uri
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
