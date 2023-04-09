# h3pop

## Data import

login to psql

create database h3demo;

\c h3demo

create table pop8(fld serial, population int, hindex text, geometry(polygon,4326));

copy pop8(hindex,population) from '/home/atlantageek/dev/h3pop/population.csv' delimiter ',' csv;

update pop8 set geom=h3_to_geo_boundary_geometry(hindex::h3index);

create index geom_idx on pop8 using gist(geom);

## Creating hex6 table
