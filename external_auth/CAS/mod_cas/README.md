Cette configuration permet de se connecter à un serveur Grafana via une authentification CAS. 

En front du serveur Grafana, nous positionons un serveur Apache (port 3000) : auth_cas.conf

Les modules suivants sont nécessaire:
<pre>ssl
proxy
proxy_balancer
proxy_http
headers
</pre>
Ce dernier va rediriger l'utilisateur vers Grafana (port 3001) : grafana.ini.

Le fichier grafana.ini est une configuration minimale pour le bon fonctionnement de l'authentification. Donc si vous avez déjà une configuration, il faut donc juste vous assurer de la présence des ces lignes de conf.
