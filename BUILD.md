\c heliumpop
create extension h3 cascade;
select fid, st_x(center)as lng, st_y(center) as lat,population from population where hex_res8 is null limit 10;
select fid, geoToH3(st_x(center), st_y(center)),population from population where hex_res8 is null limit 10;
select fid, h3_geo_to_h3(st_x(center), st_y(center)),population from population where hex_res8 is null limit 10;
select fid, h3_cell_to_lat_lng(center,8),population from population where hex_res8 is null limit 10;
select fid, h3_cell_to_lat_lng(center,8),population from population where hex_res8 is null limit 10;
select oid, extname,extversion from pg_extension;
select fid, h3_geo_to_h3(center,8),population from population where hex_res8 is null limit 10;
\d population;
select fid, substring(h3_geo_to_h3(center,8),0,10),population from population where hex_res8 is null limit 10;
select fid, substring(h3_geo_to_h3(center,8),0,10)::string,population from population where hex_res8 is null limit 10;
select fid, substring(h3_geo_to_h3(center,8),0,10)::text,population from population where hex_res8 is null limit 10;
select fid, substring(h3_geo_to_h3(center,8)::text,0,10)::text,population from population where hex_res8 is null limit 10;
update population set hex_res8=substring(h3_geo_to_h3(center,8)::text,0,11)::text where hex_res8 is null;
alter table population drop column geom;
alter table population drop column center;


copy population to '/tmp/population_hex.csv' with delimiter ',' CSV HEADER;

