1. Download docker-compose.yml to dir named `sentry`
2. Change `SENTRY_SECRET_KEY` to random 32 char string
3. Run `docker-compose up -d`
4. Run `docker-compose exec sentry sentry upgrade` to setup database and create admin user
5. (*Optional*) Run `docker-compose exec sentry pip install sentry-slack` if you want slack plugin, it can be done later
6. Run `docker-compose restart sentry`
7. Sentry is now running on public port `9000`


https://gist.github.com/denji/b801f19d95b7d7910982c22bb1478f96#file-readme-md
https://docs.sentry.io/clients/javascript/integrations/angular/