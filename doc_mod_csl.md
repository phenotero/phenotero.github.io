---
layout: page
title: Modify a CSL file
subtitle: How to make an existing style work with Phenotero
---

This is an example showing how we extended the nature csl to enable Phenotero support for displaying Phenotero entries together with conventional references in a single document. Please note that this is only feasible if you are not using any other items of type ‘entry-dictionary’ in your reference list. This should usually be the case for journal articles and clinical letters. Please be also aware, that other CSL-files might be very different and may require different approaches to enable Phenotero-style bibliographies. 

### Change file name and title

In the info section, file name and title have to be changed for the new file to function in Zotero: 

```
<info>
	<title>Nature Pheno</title>
	<id>http://www.zotero.org/styles/nature-pheno</id>
…
</info>
```

### Add Macros

Next, we added Macros to change the default numbering of the citation to the ontology identifiers and to separate the ontology entries from the ‘normal’. These macros can be added anywhere in the MACRO section of the template CSL-file. 
This allows Phenotero to display all bibliography references first, followed by a list of all ontology identifiers.
```
 <macro name="citation-locator">
    <group delimiter=" ">
      <choose>
        <if type="entry-dictionary">
			<text variable="container-title"/>
	</if>
        <else>
          <text variable="citation-number"/>
        </else>
      </choose>
      <text variable="locator"/>
    </group>
  </macro>
```
  
```
 <macro name="sort-key">
	<choose>
		<if type="entry-dictionary" match="any">
			<text value="2"/>
		</if>
		<else>
			<text value="1"/>
		</else>
	</choose>
</macro>
```

### Adapt citation block

The macro which correctly displays the ontology identifiers as citation labels in the text has to be called from within the citation block of the template CSL-file. In the case of the Nature CSL file, we simply replaced the variable ‘citation-number’ and added a group-delimiter as exemplified here: 

#### Original file: 
```
   <citation collapse="citation-number">
	<sort>
  	<key variable="citation-number"/>
	</sort>
	<layout vertical-align="sup" delimiter=",">
  	<text variable="citation-number"/>
	</layout>
  </citation>
```
#### Altered Phenotero-file: 
```
  <citation collapse="citation-number">
	<sort>
  	<key variable="citation-number"/>
	</sort>
	<layout vertical-align="sup" delimiter=",">
  	<group delimiter=", ">
    	<text macro="citation-locator"/>
  	</group>
    </layout>
  </citation>
```


#### Alter Bibliography section

The sorting macro has to be called from within the bibliography section to ensure that ontology identifiers and bibliography references are displayed separately. We added the call right at the start of the bibliography section as displayed here: 
```
<bibliography et-al-min="6" et-al-use-first="1" second-field-align="flush" entry-spacing="0" line-spacing="2">
    <sort>
   	 <key macro="sort-key"/>
    </sort>
```
In addition, the program has to distinguish between Phenotero items and normal references. As Phenotero lists its items as ‘entry-dictionary’, we set up a separate condition for these items in the layout-part of the bibliography: 
```
<layout>
   	 <choose>
   		 <if type="entry-dictionary">
   			 <!-- Citation Number -->
   			 <text variable="container-title"/>
   			 <!-- Rest of Citation -->
   			 <text variable="title" font-style="normal"/>
   		 </if>
   		 <else>    
   			 <text variable="citation-number" suffix="."/>
   			 <group delimiter=" ">
   				 <text macro="author" suffix="."/>
   				 <text macro="title" suffix="."/>
   				 <choose>
   					 <if type="chapter paper-conference" match="any">
   						 <text term="in"/>
   					 </if>
   				 </choose>
   				 <text macro="container-title"/>
   				 <text macro="editor"/>
   				 <group font-weight="bold">
   					 <text variable="volume" suffix=","/>
   				 </group>
   				 <text variable="page"/>
   				 <text macro="issuance"/>
   				 <text macro="access"/>
   			 </group>
   		 </else>
   	 </choose>
	</layout>
```
