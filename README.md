# WEBSYS2023 サーバ・ネットワーク構築・運用 サンプルアプリ

# App Install

Production Install

```sh
sudo install -d -o $(id -u) -g $(id -g) -m 755 /opt/websys2023-srvnet-example-app
python3 -m venv /opt/websys2023-srvnet-example-app/venv
source /opt/websys2023-srvnet-example-app/venv/bin/activate

pip install --upgrade wheel setuptools
pip install -e "git+https://github.com/netmarkjp/websys2023-srvnet-example-app.git#egg=websys2023_srvnet_example_app[prod]"

cd /opt/websys2023-srvnet-example-app/venv/src/websys2023-srvnet-example-app/app/
export DJANGO_SETTINGS_MODULE=mysite.settings
export MYSITE_MY_CNF=/opt/websys2023-srvnet-example-app/venv/src/websys2023-srvnet-example-app/conf/my.cnf
export MYSITE_STATIC_ROOT=/var/www/html/static
sudo install -d -o $(id -u) -g $(id -g) -m 755 /var/www/html/static
python3 manage.py migrate
python3 manage.py collectstatic
```

Development Install

```sh
pip install -e "git+https://github.com/netmarkjp/websys2023-srvnet-example-app.git#egg=websys2023_srvnet_example_app[dev]"
```

# Setup on Ubuntu 20.04

## Apache2

```
sudo apt install apache2
sudo rm /etc/apache2/sites-enabled/000-default.conf
sudo ln -s /opt/websys2023-srvnet-example-app/venv/src/websys2023-srvnet-example-app/conf/virtualhost.conf /etc/apache2/sites-enabled/000-virtualhost.conf
sudo ln -s /etc/apache2/mods-available/proxy.* /etc/apache2/mods-enabled/.
sudo ln -s /etc/apache2/mods-available/proxy_http.* /etc/apache2/mods-enabled/.
sudo apache2ctl configtest
sudo systemctl reload apache2
```

## MySQL

```
sudo apt install mysql-server-8.0 libmysqlclient-dev build-essential libpython3.8-dev
```
