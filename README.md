# Instalação do OpenVAS no Debian-12

Vamos a instalação dos pacotes necessários:
 # apt install curl docker.io python3 python3-pip docker-compose

Vamos adicionar o docker ao grupo root.
 # usermod -aG docker root
 
Crie um diretório onde iremos criar a composição do docker, em seguinta entre no diretório.
 # mkdir -p /opt/greenbone-community-container
 # cd /opt/greenbone-community-container

Baixe o arquivo de composição do docker.
 # curl -f -L https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml -o docker-compose.yml
 
Puxe os contêiners.
 # docker-compose -f opt/greenbone-community-container/docker-compose.yml -p greenbone-community-edition pull

 
Inicie os contêiner.
 # docker-compose -f /opt/greenbone-community-container/docker-compose.yml -p greenbone-community-edition up -d
 

Instalando o Nginx
# apt install nginx
# sed -i 's/# server_tokens/server_tokens/' /etc/nginx/nginx.conf
# vim /etc/nginx/sites-available/greenbone.conf


Criar arquivo greenbone.conf
 
    server {
    	listen 80;
    	listen [::]:80;
			server_name "IP DO SERVIDOR";
 
    # Descomente para restringir o acesso apenas aos IPs Listados
    # allow 127.0.0.1;
    # allow ::1;
    # allow 192.168.0.0/16;
    # allow 2801:db8::/32;
    # deny  all;
 
    location / {
        proxy_pass http://localhost:9392;
        proxy_set_header   Host $host;
    }
}



Acesse em seu navegador com usuário e senha admin.
http://IP_SERVIDOR:9392

