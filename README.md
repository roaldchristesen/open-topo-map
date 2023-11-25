# open-topo-map

Scripts zur Darstellung der topografischen Flächen in Schleswig-Holstein



## Setup Application

```
sudo apt install python3 virtualenv tree git jq
git clone https://github.com/oklabflensburg/open-topo-map.git
cd open-topo-map
virtualenv venv
. venv/bin/activate
pip install -r requirements.txt
```


## Run script

```
python tile_downloader.py 843 18685
```


## Render bbox

```
psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250gem GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250gem_bbox.csv

psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250vwg GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250vwg_bbox.csv

psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250krs GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250krs_bbox.csv

psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250rbz GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250rbz_bbox.csv

psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250lan GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250lan_bbox.csv

psql -U postgres -h localhost -d postgres -p 5433 -c "WITH j (ars, gen, wkb_geometry) AS (SELECT ars, gen, ST_Union(wkb_geometry) FROM vg250sta GROUP BY gen, ars) SELECT ars, gen, ST_Extent(wkb_geometry) FROM j GROUP BY gen, ars;" -o vg250sta_bbox.csv
```
