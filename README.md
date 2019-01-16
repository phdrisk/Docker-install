# Docker-install
Instalaçao Correta do Docker

# site: https://github.com/docker/docker-snap

# 0) instalar virtual box

# 1) 
snap install docker
# 2) 
snap connect docker:home
# 3) 
addgroup --system docker
# 4) 
adduser $USER docker
# 5) 
newgrp docker
# 6) 
snap disable docker
# 7) 
snap enable docker
