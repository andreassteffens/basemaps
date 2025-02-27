# Mapserver OSM basemaps

- this package uses a python script and the c preprocessor to build a
  complete mapfile from a set of templates and styling information.

- use the branch corresponding to your mapserver version, e.g.

  - branch-6-2 for mapserver versions 6.2.X
  - master for development/current mapserver versions

- the build process uses the gcc preprocessor extensively, you should have it installed on your
  system. On linux, check that the 'cpp' command is present. On OSX, the provided 'cpp' program is a shell
  wrapper that is not suitable: the Makefile is coded to call 'cpp-4.2', which you can change in case
  you have another version installed.

- The mapfiles rely on the database schema as created by a recent version of imposm. Until recently
  imposm did not create the landusages_gen and waterareas_gen tables. Since 2.3.0 this is not the case anymore.
  If you do not have the generalized tables, you can change the landusage_data and waterareas_data entries in
  generate_style.py so that it queries the non-generalized
  tables on the lower zoom levels (this will be slower for the lower zoom levels).

- The generated mapfile can also be made to query an osm database created with osm2pgsql rather than imposm.
  This setup is not recommended as it will be much slower. To use the osm2pgsql schema, you should add the 'osm2pgsql'
  entry to the list of styles for an entry of style_aliases near the end of generate_style.py, e.g:
  "bingosm2pgsql":"default,outlined,bing,osm2pgsql" then run `make STYLE=bingosm2pgsql` to create the osm-bingosm2pgsql.map

- Most configuration and tweaks should be done in generate_style.py.
  documentation as to how to edit can be found at
  https://mapserver.org/basemaps/style.html.

# Available styles
## default style
zoom 10

![default style, zoom 10](style-default-z10.png)

zoom 14

![default style, zoom 14](style-default-z14.png)

## google style
zoom 10

![google style, zoom 10](style-google-z10.png)

zoom 14

![google style, zoom 14](style-google-z14.png)

## bing style
zoom 10

![bing style, zoom 10](style-bing-z10.png)

zoom 14

![bing style, zoom 14](style-bing-z14.png)

## michelin style
zoom 10

![michelin style, zoom 10](style-michelin-z10.png)

zoom 14

![michelin style, zoom 14](style-michelin-z14.png)

## bw style
zoom 10

![bw style, zoom 10](style-bw-z10.png)

zoom 14

![bw style, zoom 14](style-bw-z14.png)

## Symbol style
To produce a mapfile displaying symbols, load OSM data with imposm3 using the file `imposm3-mapping-symbols.json` as mapping file

After OSM data is loaded, run post-symbols.sql to create some indexes that will speed-up queries.
(this file should be built with make command)

The following style aliases based on symbol style are defined:
 - defaultsymbols
 - googlesymbols
 - bingsymbols
 - michelinsymbols

### default vs defaultsymbols styles


zoom 15

![dzoom 15](style-default-z15.png)
![dszoom 15](style-defaultsymbols-z15.png) 

zoom 16

![szoom 16](style-default-z16.png)
![dszoom 16](style-defaultsymbols-z16.png) 

zoom 17

![dzoom 17](style-default-z17.png)
![dszoom 17](style-defaultsymbols-z17.png) 

zoom 18

![dzoom 18](style-default-z18.png)
![dszoom 18](style-defaultsymbols-z18.png) 


