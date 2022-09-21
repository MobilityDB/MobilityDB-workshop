# MobilityDB Workshop Contribution Guide

MobilityDB uses DocBook v4.5 to generate workshop guides. The instructions below provide a step-by-step guide to convert from a Notion markdown export to the XML format required to successfully compile using `dblatex`. The process uses a tool called `pandoc` to convert into DocBook v5 and then some manual editing to work with v4.5 of DocBook.

## Conventions
- Images are in `.png` format and use pascal case (e.g. `VeryImportantImage.png`) for filename. 
- XML files use lowercase underscores (e.g. `my_filename.xml`)and acronyms remain uppercase (e.g. `my_AWS_example.xml`)

## Start

Steps are as follows:
- Export from notion to Markdown
- Change folder to "images"
- Rename file to AIS_Dashboard

IN MARKDOWN
Find and replace image folder `(Dashboard%20and%20Visualization%20of%20Ship%20Trajectories%20(%20845afa91ff30470181ea3a0b5ddf08b5/` with `(images/`
Find and replace `%20` with `" "`. Refactor all image file names (use caption as image name, refactor name + pascal case)
Remove initial heading
Remove all caption duplicate text

### Convert Markdown to DocBook v5

From terminal run the following commands. Command arguments:
- `FlightDataDashboard.md` -> The name of your notion markdown file.
- `FlightDataDashboard.xml` -> Name of the output file.
```bash
cd <folder_with_markdown>
pandoc FlightDataDashboard.md -f markdown -t docbook5 -s -o FlightDataDashboard.xml
```

## In Generated XML 

- Delete header information `<!DOCTYPE ... </info>`
- Insert `<chapter id ="AIS_Dashboard">` at beginning
- Insert `<title>Dashboard and Visualization of Ship Trajectories (AIS)</title>`
- Remove `</article>` at end
- Insert `</chapter>` at end
- Find/replace `<link xlink:href` with `<ulink url`
- Find/replace `</link>` with `</ulink>`
- Find/replace `<imagedata fileref` with `<imagedata width='80%' fileref`
  - note: some pictures will need to have their width set manually.
- Remove `xml:id=...` from the "section" tag which looks like: `<section xml:id=...>`
  - `<section xml:id=...>` becomes `<section>`
- Replace `<` with `&lt;`
- Replace `>` with `&gt;`

COPY AIS_Dashboard.xml into parent doc folder
COPY all images from the notion export folder into the doc/images folder

IN mobilitydb-workshop.xml
ADD <!ENTITY GPX SYSTEM "[filename].xml"> at header
ADD &FlightDataDashboard; at end

# In Terminal
```bash
cd ..
dblatex -s texstyle.sty -T native -t pdf -o mobilitydb-workshop.pdf mobilitydb-workshop.xml
```

TODO: change image filename