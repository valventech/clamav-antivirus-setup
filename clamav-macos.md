## Configuring ClamAV on MacOS

Execute below lines using an admin account (root)

```bash
brew install clamav

cp /usr/local/etc/clamav/freshclam.conf.sample /usr/local/etc/clamav/freshclam.conf

sed -i '' 's/Example/# Example/' /usr/local/etc/clamav/freshclam.conf

freshclam
freshclam -d

cp /usr/local/etc/clamav/clamd.conf.sample /usr/local/etc/clamav/clamd.conf

sed -i '' 's/Example/# Example/' /usr/local/etc/clamav/clamd.conf

crontab -e
# put below line, save and exit
0 12 * * * /usr/local/clamav/bin/freshclam > /dev/null 2>&1
10 12 * * * /usr/local/bin/clamav/clamscan -r /Users/$(whoami) -i -o -l "/var/log/clamscan-$(date +\%b-\%d-\%Y).log" 


```
