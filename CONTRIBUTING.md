# MobilityDB Workshop Contribution Guide

MobilityDB uses DocBook v4.5 to generate workshop guides. The instructions below provide a step-by-step guide to contribute to the workshop guide.

## Conventions
- Images are in `.png` format and use pascal case (e.g. `VeryImportantImage.png`) for filename. 
- XML files use lowercase underscores (e.g. `my_filename.xml`) and acronyms remain uppercase (e.g. `my_AWS_example.xml`)

## Contribution Workflow

Steps are as follows:
- Usually, the latest version of the workshop guide is in the `develop` branch. Refer always to this branch.
- Fork the repository and clone it locally.
- Create a new branch from `develop` and name it `feature/<your_feature_name>`. For example, 'feature/correcting_typos'.
- Make your changes and commit them to your branch.
- Push your branch to your forked repository.
- Create a pull request from your branch to the `develop` branch of the main repository. Please, make sure to detail your changes in the pull request description. A nice way to do this is to use the following template:
  
  ```markdown 
  Changes:
  - Fix typos
  - Add new section
  - etc.
  ```

## Changing the Workshop Guide

If you want to make changes to the guide, you will need to edit the xml file corresponding to the chapter you want to change. For example, if you want to propose a change to the `AIS_Dashboard` chapter, you will need to edit the `doc/AIS_Dashboard.xml` file.

## Adding a New Chapter

If you want to add a new chapter to the guide, you will need to create a new xml file in the `doc` folder. For example, if you want to add a new chapter called `My_New_Chapter`, you will need to create a new file called `doc/My_New_Chapter.xml`. 

If you need to insert any images in the new chapter, you will need to add them to the `doc/images` folder. For example, if you want to add an image called `My_New_Image.png`, you will need to add it to the `doc/images` folder.

You will also need to add the following line to the `mobilitydb-workshop.xml` file:

```xml
<!ENTITY My_New_Chapter SYSTEM "doc/My_New_Chapter.xml">
```

Finally, you will need to add the following line to the `mobilitydb-workshop.xml` file, in the appropriate place:

```xml
&My_New_Chapter;
```

This will include the new chapter in the guide.