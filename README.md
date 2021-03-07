# public_debian10_repository
Trying something out, need to host a Debian package

## How to add repo

```
sudo curl -s --compressed -o /etc/apt/sources.list.d/nextpertise_public_debian10_repository.list "https://nextpertise.github.io/public_debian10_repository/public_debian10_repository.list"
```

## How to add new packages
Just put your new .deb files inside the git repo `public_debian10_repository` and execute:

```
# Packages & Packages.gz
dpkg-scanpackages --multiversion . > Packages
gzip -k -f Packages

# Release, Release.gpg & InRelease
apt-ftparchive release . > Release
gpg --default-key "${EMAIL}" -abs -o - Release > Release.gpg
gpg --default-key "${EMAIL}" --clearsign -o - Release > InRelease

# Commit & push
git add -A
git commit -m update
git push
```

Followed howto: https://assafmo.github.io/2019/05/02/ppa-repo-hosted-on-github.html
