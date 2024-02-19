# cloud-final

## installing packages

```
sudo apt update && sudo apt upgrade -y
sudo apt install nginx
```

```
curl -sL https://deb.nodesource.com/setup_18.x -o /tmp/nodesource_setup.sh
nano /tmp/nodesource_setup.sh

sudo bash /tmp/nodesource_setup.sh
sudo apt install nodejs
npm install -g npm@10.4.0
```

## configuring nginx
`sudo nano /etc/nginx/sites-available/nextjs`

```
  server {
    listen 80;
    server_name YOUR_IP_ADDRESS;
    location / {
      proxy_pass http://localhost:3000;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
    }
  }
```

`sudo ln -s /etc/nginx/sites-available/nextjs /etc/nginx/sites-enabled/`

```
sudo nginx -t
sudo service nginx restart
```

## building nextjs project
```
cd /var/www/html
rm index.nginx-debian.html
git clone https://github.com/Sakal05/Borey-Management-Company.git

cd Borey-Management-Company
mv * ../
mv .[!.]* ../ 
cd ..
rm -r Borey-Management-Company

npm i
```

### ignoring eslint on build
`nano next.config.js`

```
  eslint: {
    // Warning: This allows production builds to successfully complete even if
    // your project has ESLint errors.
    ignoreDuringBuilds: true
  },
```

`npm run build`

## installing process manager to keep process running

```
sudo npm install -g pm2
pm2 start npm --name "nextjs" -- start
pm2 startup
pm2 save
```
