## Configuring ClamAV on MacOS

Execute below lines using an admin account (root)

Install ClamAV either using brew or download from [ClamAV](https://www.clamav.net/downloads)

```bash
brew install clamav # skip this step if you have downloaded the package from the website

cp /usr/local/clamav/etc/freshclam.conf.sample /usr/local/etc/clamav/freshclam.conf

sed -i 's/Example/# Example/' /usr/local/etc/clamav/freshclam.conf

sudo freshclam

cp /usr/local/clamav/etc/clamd.conf.sample /usr/local/clamav/etc/clamd.conf

sed -i '' 's/Example/# Example/' /usr/local/etc/clamav/clamd.conf

crontab -e -u root

# put below line, save and exit (esc :wq)
0 12 * * * /usr/local/clamav/bin/freshclam > /dev/null 2>&1
10 12 * * * /usr/local/bin/clamav/clamscan -r /Users/USERNAME -i -o -l "/var/log/clamscan-$(date +\%b-\%d-\%Y).log" > /dev/null 2>&1 # Replace your username

# Run this line manually for testing. It will scan your home directory and log the result to /var/log/clamscan-<date>.log
# Accept necessary permissions if prompted
/usr/local/bin/clamav/clamscan -r /Users/USERNAME -i -o -l "/var/log/clamscan-$(date +\%b-\%d-\%Y).log"  # Replace your username

```
