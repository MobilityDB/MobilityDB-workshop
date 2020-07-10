MobilityDB Workshop
===================

Every module in this workshop illustrates a usage scenario of MobilityDB. The data sets and the tools are described inside each
of the modules.

Documentation
-------------

You can generate the workshop documentation from the sources.
*  In HTML format

        xsltproc --stringparam html.stylesheet "docbook.css" --xinclude -o index.html /usr/share/xml/docbook/stylesheet/docbook-xsl/html/chunk.xsl mobilitydb-workshop.xml
*  In PDF format

        dblatex -s texstyle.sty -T native -t pdf -o mobilitydb-workshop.pdf mobilitydb-workshop.xml
* In EPUB format

        dbtoepub -o mobilitydb-workshop.epub mobilitydb-workshop.xml

In addition, pregenerated versions of them are available.

*  In HTML format: https://docs.mobilitydb.com/MobilityDB/master/workshop/
*  In PDF format: https://docs.mobilitydb.com/MobilityDB/master/workshop/workshop.pdf
* In EPUB format: https://docs.mobilitydb.com/MobilityDB/master/workshop/workshop.epub

License
-------

This workshop is licensed under a [Creative Commons Attribution-Share Alike 3.0 License](https://creativecommons.org/licenses/by-sa/3.0/)