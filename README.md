# odoo-V18-Community-to-enterprise-using-docker-envs
short  description of the actions to upgrade a odoo community v18 to the enterprise release, being under docker

August 15th 2025
to upgrade to latest V18 from V17, you may refer to my repo https://github.com/lucpierson/odoo17-to-18-community-upgrade-docker

Official doc is here : https://www.odoo.com/documentation/18.0/administration/on_premise/community_to_enterprise.html#

These are descriptions of the actions I did to upgrade a odoo community v18 to the enterprise release, being under docker containers

0) Backup your data (in my case, I have a backup script, gpt can help build yours) 
1) Upgrade your current env to last V18 release
2) Download the latest enterprise modules (link below, you need an account as customer or partner) and place the folders under ./custom/
3) Create a full env based on V18 called V18-ENT (with provided latest V18 Dokerfile)
    

a) under your "custom" dir, download the enterprise content 

b) stop and rm the docker running odoo, KEEPING the database docker running

   			** docker ps -a
   			** docker stop odoo-18-COMMUNITY-20250725
   			** docker rm odoo-18-COMMUNITY-20250725
	
c) run (once ==> no restart) the docker for enterprise upgrade

   			** move docker-compose.InstallPonctuelleWebEnterprise.yml  docker-compose.yml
   			** docker-compose up -d
   			** follow the logs to verify that upgrade goes smoothly
   			** docker stop odoo-18-PONTCUEL-ENTREPRISE-20250725
   			** docker stop odoo-18-PONTCUEL-ENTREPRISE-20250725
   	
d) finally run the docker with enterprise env (still accessing  on the existing running db)

   			** move docker-compose.Enterprise.yml  docker-compose.yml
   			** docker-compose up -d
   			** follow the logs to verify that upgrade goes smoothly
   			** on the interface, parameters, all the way down, verify the current version you are working on
   
links : 
  * odoo Docker images : https://hub.docker.com/_/odoo
  * odoo Enterprise module : http://github.com/odoo/enterprise


Please note that for the migration purpose, I run postgres on 5436 port and expose odoo on 8269 (you may keep you 5432/8069 usual ports) 

This is provided as indication only, HTH, best, Luc
