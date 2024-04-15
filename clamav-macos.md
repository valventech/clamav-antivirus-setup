## Configuring ClamAV on MacOS

Execute below lines using an admin account (root)

```bash
brew install clamav

cp /opt/homebrew/etc/clamav/freshclam.conf.sample /opt/homebrew/etc/clamav/freshclam.conf

sed -i 's/Example/# Example/' /opt/homebrew/etc/clamav/freshclam.conf

sudo freshclam

cp /opt/homebrew/etc/clamav/clamd.conf.sample /opt/homebrew/etc/clamav/clamd.conf

sed -i 's/Example/# Example/' /opt/homebrew/etc/clamav/clamd.conf

crontab -e -u root

# put below lines in the crontab file, save and exit (esc :wq)
# Replace USERNAME with your username in the below lines
0 12 * * * /opt/homebrew/Cellar/clamav/1.3.0/bin/freshclam > /dev/null 2>&1

10 12 * * * /opt/homebrew/Cellar/clamav/1.3.0/bin/clamscan -r /Users/USERNAME -i -o -l "/var/log/clamscan-$(date +\%b-\%d-\%Y).log" > /dev/null 2>&1

# Run this line manually for testing. It will scan your home directory and log the result to /var/log/clamscan-<date>.log
# Accept necessary permissions if prompted
# Replace your username in the below line
/opt/homebrew/Cellar/clamav/1.3.0/bin/clamscan -r /Users/USERNAME -i -o
```
