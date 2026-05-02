# MobilityDB Workshop


Every module in this workshop illustrates a usage scenario of MobilityDB. The data sets and the tools are described inside each
of the modules.

## Documentation

You can generate the workshop documentation from the sources. Go to `/docs` directory and run: 
*  In HTML format
    ```bash
    xsltproc --stringparam html.stylesheet "docbook.css" --stringparam chunker.output.encoding "UTF-8"  --xinclude -o index.html /usr/share/xml/docbook/stylesheet/docbook-xsl/html/chunk.xsl mobilitydb-workshop.xml
    ```
*  In PDF format
    ```bash
    dblatex -s texstyle.sty -T native -t pdf -o mobilitydb-workshop.pdf mobilitydb-workshop.xml 
    ```
* In EPUB format
    ```bash
    dbtoepub -o mobilitydb-workshop.epub mobilitydb-workshop.xml
    ```
In addition, pregenerated versions of them are available for both the master and develop branches.

*   HTML: [master](https://mobilitydb.github.io/MobilityDB-workshop/master/html/index.html), [develop](https://mobilitydb.github.io/MobilityDB-workshop/develop/html/index.html)
*   PDF: [master](https://mobilitydb.github.io/MobilityDB-workshop/master/mobilitydb-manual.pdf), [develop](https://mobilitydb.github.io/MobilityDB-workshop/develop/mobilitydb-manual.pdf)
*   EPUB: [master](https://mobilitydb.github.io/MobilityDB-workshop/master/mobilitydb-manual.epub), [develop](https://mobilitydb.github.io/MobilityDB-workshop/develop/mobilitydb-manual.epub)

## How the Repo is Organized
- `/data`: raw data files used for some workshops
- `/docs`: files needed to generate the workshop documentation from sources

## Docker container

A prebuilt Docker image is available with PostgreSQL 18, PostGIS 3.6, and MobilityDB 1.3.

* Pull the image and create a persistent volume:

    ```bash
    docker pull mobilitydb/mobilitydb:18-3.6-1.3
    docker volume create mobilitydb_data
    ```

* Unzip the workshop data files on the host so the container can read them through a bind-mount:

    ```bash
    cd data && unzip -o ais_data.zip && unzip -o gtfs_data.zip && cd ..
    ```

    This produces `data/ais.csv` and the GTFS files (`data/stops.txt`, `data/routes.txt`, etc.).

* Run the container, mounting `data/` at `/workshopData/` inside it:

    ```bash
    docker run --name mobilitydb -d \
        -e POSTGRES_USER=docker \
        -e POSTGRES_PASSWORD=docker \
        -e POSTGRES_DB=mobilitydb \
        -p 5432:5432 \
        -v mobilitydb_data:/var/lib/postgresql \
        -v "$(pwd)/data":/workshopData \
        mobilitydb/mobilitydb:18-3.6-1.3
    ```

    The workshop data files are then accessible inside the container under `/workshopData/`. Chapters that load CSV/TXT files can `\copy` from there, e.g. `\copy stops FROM '/workshopData/stops.txt' DELIMITER ',' CSV HEADER`.

* Connect to the database:

    ```bash
    docker exec -it mobilitydb psql -U docker -d mobilitydb
    ```


## License

This workshop is licensed under a [Creative Commons Attribution-Share Alike 3.0 License](https://creativecommons.org/licenses/by-sa/3.0/)
