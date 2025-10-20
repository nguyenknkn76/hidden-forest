# Setup Azure Entra ID 

- Azure > Entra ID > App registration > `tennant id`, `client id` & `redirect uri`
  - redirect uri: https or localhost (localhost sus)
  - return :username, name, sessions, ...

- about https setup: 
  - reverse proxy: traefik, nginx (using docker)
  - create domain name: point to server's ip, A record, ... (using `dig domainname.com` to check) 
  - create cert (seft cert): using certbot, ... ()

- flows: login > popup > enter ... > ms account info

- With React.js:
  - msal lib -> sus 
  - should using popup (instead of redirect)