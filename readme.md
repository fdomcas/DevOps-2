# Paso 1 
- sudo systemctl restart docker.service 
###### uso este devido a que yo no tengo networking.service
- sudo systemctl restart systemd-networkd.service  

# Paso 2 instalacion
- python3 -m venv .venv
- source venv/bin/activate
- pip install -r requirements.txt 
- brave http://localhost:5000 &
- python src/app.py  [inicio](https://imgur.com/a/5P4whmb)

- gunicorn --chdir src app:app --bind 0.0.0.0:5000
[inicio gunicorn](https://imgur.com/a/qR4qDzV)

# Paso 3 imagen
- docker build -t fdomcas/galeria:latest .
- docker run -d -p 80:5000  --name testgaleria fdomcas/galeria
- brave http://localhost:5000 &
- docker stop testgaleria && docker rm testgaleria

# Paso 4 
- docker compose up -d
- brave http://localhost:5000 &

# Paso 5 subir la imagen
- docker login
- docker push fdomcas/galeria

# Paso 5 token dokerhub
- Generamos de dockerhub el token
- Añadimos 2 secretos al repo que creamos con los siguientes nombres
-  DOCKERHUB_USERNAME = nombre del usuario de dockerhub
-  DOCKERHUB_TOKEN = Token que generamos de docker hub
# Paso 5.1 action
una vez tenemos el repo creado ya solo nos falta configurar el action para que cada ve que subamos algo a repo se ejecute

# Paso 6 AWS
- De AWS necesitamso 3 cosas ip-publica, nombre de usario de la instancia y por ultimo el contenido del vockeys
- AWS_USERNAME = usuario de la instacia por lo generar es admin 
- AWS_HOSTNAME = ip publica o elastica(ip fija)
- AWS_PRIVATEKEY= contenido del vockeys

# PASO 6.1 Volvemos a modificar el action del repo
Esta vez lo que aremos es añadirle un tabajo al action para que cunado se ejecuta un push al repo y se cree la imagen depues automaticamente se despliege en AWS