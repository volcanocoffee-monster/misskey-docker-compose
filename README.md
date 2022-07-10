# misskey-docker-compose

## Guide
### Step 1: Initial Setup
```
# clone repo
git clone --recurse-submodules --remote-submodules https://github.com/volcanocoffee-monster/misskey-docker-compose.git
cd misskey-docker-compose/
# remove git files to help prevent possible issues with updates
rm -rf .git .gitmodules
# copy  example files
cp misskey/.config/example.yml misskey/.config/default.yml
cp misskey/.config/docker_example.env misskey/.config/docker.env

```
### Step 2: Configure
Edit `default.yml` and `docker.env` according to the instructions in the files.

In the `default.yml`, the hosts that set with `localhost` from `Postgresql`/`Redis` should be set to `db`/`redis` respectively.
### Step 3: Building Misskey
Note: make sure to be in /path/to/misskey-docker-compose not /path/to/misskey-docker-compose/misskey
```
sudo docker-compose build
sudo docker-compose run --rm web yarn run init

```
### Step 4: Launching
Note: make sure to be in /path/to/misskey-docker-compose not /path/to/misskey-docker-compose/misskey
```
sudo docker-compose up -d
```
### Updating: misskey
When updating, be sure to check the [release notes](https://github.com/misskey-dev/misskey/blob/master/CHANGELOG.md) to know in advance the changes and whether or not additional work is required (in most cases, it is not).
```
cd misskey
git stash
git checkout master
git pull
git submodule update --init
git stash pop
sudo docker-compose build
sudo docker-compose stop && sudo docker-compose up -d
```
### Updating: hosts
```
cd hosts
git pull
```
