
# NYU EAD Plugin Customization

This document describes the customizations made to the default ArchiveSpace EAD export module so that EAD's exported from ArchiveSpace can be imported into the Find Aid Publisher.

## Introduction ##
I originally started my analysis with the assumption that the ead plugin was written scratch.  Because of this, I wasted a significant amount of time trying to understand the function of each line of code.

I later discovered that other institutions had the same use and found the following page showing how to override EAD import and export functionality for ArchiveSpace.  I serendipitously found the link while googling the search terms archivesspace serialize_container:

[Customizing your ArchivesSpace EAD importers and exporters](https://archivesspace.atlassian.net/wiki/x/zAAUAQ) 

https://archivesspace.atlassian.net/wiki/spaces/ADC/blog/2015/03/15/18088140/Customizing+your+ArchivesSpace+EAD+importers+and+exporters.
 
 In the document above, the author refers to the original EAD plugin
 
[Default ArchivesSpace EAD converter](https://github.com/archivesspace/archivesspace/blob/master/backend/app/converters/ead_converter.rb) 
 
 After comparing the original code with that of the NYU ead plugin, it looks like NYU ead plugin developer took the approach of copying all of the code from the original and then modifying accordingly.  With this in mind, the task of analyzing the changes became much easier.
 
 To find the changes, I created a unified diff of the default converter and the customized converter and went through the commits in github.

    diff -wu ead.rb nyu_ead_exporter.rb | vim - -c TOhtml -c ":saveas ead-diff.html" -c ":q" -c ":q!"
 
    diff -wu addresslines_orig addresslines_nyu | vim - -c TOhtml -c ":saveas addresslines-diff.html" -c ":q" -c ":q!"
 
The diffs can be found here:

[EAD Converted diff](ead-diff.html) 
[Address lines diff](addresslines-diff.html) 


## Changes ##

- The address lines in the EAD model has been changed.
    - Add 'name' field
    - We don't add contact fields if they don't exist
    - Don't add telephone info

 