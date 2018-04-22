# SCRIPTS de generación de datos para #LasCallesDeLasMujeres

Read this in ENGLISH here: [README.en.md](https://github.com/geochicasosm/data_scripts_lascallesdelasmujeres/master/README.en.md)

Visita la web del proyecto: [#LasCallesDeLasMujeres](https://geochicasosm.github.io/lascallesdelasmujeres/) ( Versión beta ) de [GEOCHICAS](https://geochicas.org/)


## Getting Started


Los datos que se visualizan en el proyecto [#LasCallesDeLasMujeres](https://geochicasosm.github.io/lascallesdelasmujeres/) se generan ejecutando los scripts contenidos en este proyecto. A continuación se detallan las instrucciones para reproducir el proceso y poder generar datos para cualquier ciudad.



### Instalación y preparación de entorno

Para poder decargar el proyecto i ejecutar los scripts, es necesario tener instalado:

* GIT (Descargar [AQUí](https://git-scm.com/downloads))
* Node.js (Descargar [AQUí](https://nodejs.org/es/download/))


Descargar el proyecto:

```
git clone https://github.com/geochicasosm/data_scripts_lascallesdelasmujeres.git
```

Instalación de paquetes:

```
npm install
```

Descargar [AQUÍ](http://osmlab.github.io/osm-qa-tiles/) el planet completo de OSM (o la zona que interese) y guardar en una carpeta llamada "data", dentro de la carpeta del proyecto.

```
./data/latest.planet.mbtiles
```


Instrucciones
======

### _Paso 1_

Buscar [AQUÍ](http://tools.geofabrik.de/calc/) la BBOX de la ciudad a tratar.

Crear una carpeta dentro de la carpeta del proyecto con el nombre de la ciudad a tratar, en minúsuclas y sin espacios. Ejemplos: 

 **barcelona** 
 
 **sanjose** 
 
 **buenosaires** 


 

### _Paso 2_

Ejecutar:

```
npm run step1 -- --area=[bbox] --ciudad=nombreciudad
```

* Ejemplo: **npm run step1 -- --area=[2.0875,41.2944,2.2582,41.4574] --ciudad=barcelona** 


Se generan dos ficheros:
* nombreciudad_streets.geojson
* list.csv


### _Paso 3_

Aplicar la clasificación del listado anterior en nombres masculinos o femeninos. Dos opciones:

#### Opción 1:

Se usa un fichero con un listado de nombres clasificados por género, sacados de institutos de estadística. En caso que el nombre no aparezca en el listado, se hace una petición a la API online de NameSor. Ejecutar:

```
npm run step2 -- --ciudad=nombreciudad
```

* Si se alcanza el límite gratuito permitido, usar la opción 2.

#### Opción 2:

Instalar y usar RapidMiner. Descargar [AQUÍ](https://rapidminer.com/)

Seguir [ESTE](https://www.youtube.com/watch?v=wScgijiqA2c) tutorial.

**IMPORTANTE**: 
Se ha de indicar explícitamente que 
-	el formato de salida sea un CSV
-	el encoding sea UTF-8.
-	el nombre del fichero de salida sea 'list_genderize.csv'


### _Paso 4_

Aplicar el script que elimina las calles con factores de fiabilidad por encima y por debajo de -0.25 y 0.25.

Pasar el parámetro **--wikipedia** si se quiere forzar la búsqueda de los artículos de Wikipedia.

```
npm run step3 -- –-ciudad=nombreciudad --wikipedia
```

Se genera el fichero 'list_genderize.csv' o 'list_genderize_w.csv' si hemos forzado la búsqueda en Wikipedia.


### _Paso 5_

Revisar manualmente el fichero anterior:
- Eliminar calles que no son de persona
- Corregir errores en la clasificación male/female
- Corregir y añadir enlaces de Wikipedia (las calles con nombre de hombre no necesitan enlace)

A tener en cuenta:
- Factor de fiabilidad: Valores de 2 a -2 (Mujer a Hombre).

Guardar el fichero corregido en la misma carpeta del proyecto, con el nombre:

**nombreciudad_finalCSV.csv**

### _Paso 6_

Ejecutar:

```
npm run step4 -- –-ciudad=nombreciudad
```

Se generan tres ficheros:
- **final_tile.geojson** Fichero final que se cargará en el mapa
- **stats.txt** fichero con estadísticas de los datos
- **noLinkList.txt** Fichero con el listado de calles sin artículo en wikipedia


## Para acabar

Haznos llegar los tres ficheros generados y añadiremos tu ciudad al mapa! 

---

## Contribuir con el proyecto

Únete a nuestro canal de slack [#lascallesdelasmujeres](https://join.slack.com/t/geochicas-osm/shared_invite/enQtMzIzMzUyMDQyNjczLTU0YjYzNTQ2ZWRkOWQwZGJlNGY4NjhmODY4Y2M2M2Y2MDM3M2EyZTg4NWI0ODY2ZWRhZGIyN2JjMDc0ZDdlODE) si te interesa contribuir.


## Coordinadora Técnica

* **Jessica Sena** (*España*) - [@jsenag](https://jessisena.github.io/myprofile/) 
    
    Ingeniera informática, desarrolladora web/móvil en ámbito geo.
   


## Licencia

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details


## Reconocimientos


* [Proyecto](https://blog.mapbox.com/mapping-female-versus-male-street-names-b4654c1e00d5) _Mapping female versus male street names_ de Mapbox por [Aruna Sankaranarayanan](https://www.mapbox.com/about/team/aruna-sankaranarayanan/) 

* [Open Street Map](https://www.openstreetmap.org/)

* [NameSor](http://api.namsor.com/onomastics/api/)

* [Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page/es)

* [Geofabrik](http://tools.geofabrik.de/calc/)



