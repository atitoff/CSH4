# ROCK 4

Удаление GUI из Debian
```bash
sudo apt-get remove -y --purge x11-common
sudo apt-get autoremove -y --purge
sudo apt-get install -y deborphan
sudo deborphan | sudo xargs dpkg -P # do this a bunch of times
```