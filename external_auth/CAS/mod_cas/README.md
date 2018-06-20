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

<b>Les bonnes pratiques demandent de ne pas écraser le fichier de conf mais de le mettre à jour. Une aide assez intéressante est que Grafana peut surcharger son fichier de conf avec les variables d'environnement. </b>

Un export suffit en BASH mais dans le cas de DOCKER, vous pouvez les déclarer à la création du conteneur avec les options : 
<pre>
  -e "GF_SERVER_HTTP_PORT=3001"  \
  -e "GF_USERS_ALLOW_SIGN_UP=false"  \
  -e "GF_USERS_AUTO_ASSIGN_ORG=true"  \
  -e "GF_USERS_AUTO_ASSIGN_ORG_ROLE=Editor"  \
  -e "GF_AUTH.BASIC_ENABLED=true"  \
  -e "GF_AUTH_PROXY_ENABLED=true"  \
  -e "GF_AUTH_PROXY_HEADER_NAME=X-WEBAUTH-USER"  \
  -e "GF_AUTH_PROXY_HEADER_PROPERTY=username"  \
  -e "GF_AUTH_PROXY_AUTO_SIGN_UP=true"  \
 </pre>
