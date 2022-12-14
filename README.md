fleet-optimizer
========
Fleet Management Software (FMS)

### index
source code:
- library: https://github.com/trabur/fleet-optimizer
- server: https://github.com/trabur/pro.istrav.dev
- clients:
  - browser: https://github.com/trabur/istrav.pro
  - mobile: coming soon!

apps:
- osrm: https://osrm.istrav.dev
- database: https://couchdb.istrav.dev
- server: https://pro.istrav.dev
- clients:
  - browser: https://istrav.pro
  - mobile: coming soon!

library tech:
- TypeScript
- rxdb.info
- couchdb.apache.org
- project-osrm.org

### install
```bash
# https://www.npmjs.com/package/fleet-optimizer
npm i fleet-optimizer
```

### about
The most optimal solution is the outcome where time is saved and where each member of the group makes more money than if they were to work individually. 

- a fleet could be a company or team
- the goal is to process orders and make deliveries as a fleet
- fleets may have many professionals, vehicles, customers, orders
- trades are what give professionals abilities
- professionals with a trade in trucking may move materials from source to factory
- professionals with a trade in trucking may move products from factory to warehouse
- professionals with a trade in trucking may move products from warehouse to store
- professionals with a trade in dashing may move products from store to customer
- customers may have many contacts and many locations
- factories generate products
- warehouses hold products temporarily
- stores sell products to customers
- factories, warehouses, and stores may be shared or limited between fleets

tests:
```bash
fleet1 Expert Services
vehicle1 SDF123
location1 Austin, TX
```

examples:
```bash
# npm run examples:storedash
```

```bash
# npm run examples:mrclean
```

```bash
# npm run examples:hvacpro
```

```bash
# npm run examples:trucking
```

### istrav-couchdb
We use CouchDB for data persistance.
- https://couchdb.istrav.dev/_utils/

```bash
# on ubuntu 22
sudo snap install couchdb

# https://github.com/apache/couchdb-pkg/blob/main/README-SNAP.md

$ sudo ufw enable
$ sudo ufw allow 5984/tcp
$ sudo ufw reload
```

### istrav-osrm
We use OSRM for our distance matrix api calculator:
- https://github.com/Project-OSRM/osrm-backend

Setup:
```bash
# install dependencies
sudo apt install build-essential git cmake pkg-config \
libbz2-dev libxml2-dev libzip-dev libboost-all-dev \
lua5.2 liblua5.2-dev libtbb-dev

# clone repository
cd ~/Projects
git clone https://github.com/Project-OSRM/osrm-backend.git
cd ./osrm-backend

# compile and install OSRM binaries
mkdir -p build
cd build
cmake ..
cmake --build .
sudo cmake --build . --target install

# return
cd ~/Projects/osrm-backend

# extract open street maps after downloading files from:
# http://download.geofabrik.de/

# because files are big they need swap enabled on them
fallocate -l 100G ~/osm/swapfile
chmod 600 ~/osm/swapfile
mkswap ~/osm/swapfile
swapon ~/osm/swapfile

# load
osrm-extract ~/osm/north-america-latest.osm.pbf -p profiles/car.lua
osrm-contract ~/osm/north-america-latest.osrm

# run
osrm-routed ~/osm/north-america-latest.osrm
```

### versioning
```bash
# tag a vew version
$ npm version v1.0.1 --no-git-tag-version

# check everything in
$ git add . && git commit -m "version" && git push

# then check version tag in
$ git tag v1.0.1
$ git push --tags
```