[![Build Status](https://travis-ci.org/incertae-sedis/cavatica.svg?branch=master)](https://travis-ci.org/incertae-sedis/cavatica) [![github release](https://img.shields.io/github/release/incertae-sedis/cavatica.svg?label=current+release)](https://github.com/incertae-sedis/cavatica/releases)

**Author**: Team Mango -- Will Sutherland, Ashley Griffin, Elmira Kalhor, and Chola Chhetri  | **Initial Commit**: July 2018 
<p style="text-align: center;">***** This is a reprodcution of Cavatica by Team Mango at the Cyber Carpnetry 2018 *****</p>

## Cavatica [by original author Jennifer Chang]  
Code and pipeline for fetching PubMed and PubMed Central data and co-author network analysis. This tool can be used to identify author trends among several search terms. 

An example, I've used these scripts to do a multi-network analysis of network analysis papers and their software. 
[Wiki Page Here](https://github.com/incertae-sedis/cavatica/wiki)

<img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/Adder.png" width="600" alt="Added">

The name comes from Charlotte's Web since her full name was Charlotte A. Cavatica. Although Cavatica also refers to barn spider.

## Pipeline

<p style="text-align: center;">***** Cavatica pipeline has been modified so no longer relies on Ebot. *****</p>

<img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/plan.png" width="600" alt="Plan">

<!--
[List of Entrez Databases](https://eutils.ncbi.nlm.nih.gov/entrez/eutils/einfo.fcgi)

[EBot](http://www.ncbi.nlm.nih.gov/Class/PowerTools/eutils/ebot/ebot.cgi)
-->

## Dependencies

* Some type of Linux Terminal where you can run Bash. (Cygwin if you're on Windows. Terminal already preinstalled on Mac)
* R (check if installed by typing Rscript --version)
* perl (check if installed by typing perl --version)
* Mango Graph Studio for multi-network analysis

## Installation

```
git clone https://github.com/incertae-sedis/cavatica.git
```

## Basic Example

Here is a basic example fetching PubMed and PMC papers containing the word "Neo4j" and "Cytoscape". 

```
cd cavatica/data
mkdir test
cd test
echo "Neo4j" > config.txt
echo "Cytoscape" >> config.txt
../../code/script.sh
```

This will create tabular files (list of papers `Neo4j_papers_pm.tsv` and list of authors `Neo4j_authors_pm.tsv`). Open the png files `Neo4j_pm.png` to see a barchart of the number of papers by year.


<img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/Neo4j-pubmedcounts.png" width="400" alt="Neo4j count"><img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/Cytoscape-pubmedcounts.png" width="400" alt="Cavatica count">

Can also open the html files to check the one sentence usages of Neo4j and Cavatica

<table>
<tr>
<td>
<h1>Sentences that contain Neo4j</h1>
<p>2018 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=29377902">29377902</a>
 Reactome graph database: Efficient access to complex pathway data.<ul><li>Here 
we present the rationale behind the adoption of a graph database (<b>Neo4j</b>) as well as the new ContentService (REST API) that provides access to these data. </ul></p><p>2018 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=28936969">28936969</a> Systematic integration of biomedical knowledge prioritizes drugs for repurposing.<ul><li>First, we constructed Hetionet (<b>neo4j</b>.het.io), an integrative network encoding knowledge from millions of biomedical studies. </ul></p><p>2017 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=28416946">28416946</a> Use of Graph Database for the Integration of Heterogeneous Biological Data.<ul><li>Here, we demonstrate the feasibility of using a graph-based database for complex biological relationships by comparing the performance between MySQL and <b>Neo4j</b>, one of the most widely used graph databases. <li>When we tested the query execution performance of MySQL versus <b>Neo4j</b>, we found that <b>Neo4j</b> outperformed MySQL in all cases. <li>These results show that using graph-based databases, such as <b>Neo4j</b>, is an efficient way to store complex biological relationships. </ul></p>

...
</td>
</tr>
</table>

<table>
<tr>
<td>
<h1>Sentences that contain Cytoscape</h1>
<p>2018 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=29894068">29894068</a> Identification of potential miRNAs and candidate genes of cervical intraepithelial neoplasia by bioinformatic analysis.<ul><li>Then the miRNA- mRNA regulatory network was constructed using <b>Cytoscape</b> software. </ul></p><p>2018 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=29872319">29872319</a> An integrated analysis of key microRNAs, regulatory pathways and clinical relevance in bladder cancer.<ul><li>Protein-protein interaction (PPI) and miRNA-mRNA regulatory networks were established by using the Search Tool for the Retrieval of Interacting Genes/Proteins and <b>Cytoscape</b> tool. </ul></p><p>2018 <a href="http://www.ncbi.nlm.nih.gov/pubmed/?term=29760609">29760609</a> Identification of potential crucial genes and construction of microRNA-mRNA negative regulatory networks in osteosarcoma.<ul><li>Protein-protein interaction (PPI) network was constructed by STRING and visualized in <b>Cytoscape</b>. </ul></p>

...
</td>
</tr>
</table>

It will also create a script `pubmed.gel`. Open [Mango Graph Studio](https://www.complexcomputation.com/en/product/mango-community-edition/), open `pubmed.gel` and type the following into the Mango Console.

```
run "pubmed.gel";
```

This will create a transition table and export the file. It will also load and visualize the author-paper networks.

<table>
<tr><td>Neo4j</td><td>Cytoscape</td</tr>
<tr><td><img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/Neo4j.png" width="300" alt="Neo4j network"></td>
<td><img src="https://github.com/incertae-sedis/cavatica/blob/master/IMG/Cytoscape.png" width="300" alt="Cavatica network"></td</tr>
</table>
Going back to your terminal, rerun the script file and it will continue.

```
../../code/script.sh
```

The transitions should be saved in `trends_pm.txt`. The following trends_pm.txt indicates that authors switched from cytoscape to Neo4j 9 times, while authors switched from Neo4j to Cytoscape 3 times.

```
Cytoscape:Neo4j 9
Neo4j:Cytoscape 3
```

It will then commence searching PMC, fetching list of papers and authors and generating a "pmc.gel" file. Once again open the "pmc.gel" file in Mango and type the following into Mango Console.

```
run "pmc.gel";
```

Then rerun the script to continue tabulating the trends which should be saved in `trends_pmc.txt`.

The output of a 2017 run comparing "Neo4j", "Gephi", "GraphViz" and "iGraph" is shown below:

```
=============PubMed Transitions
Neo4j:Gephi 1
Neo4j:GraphViz 1
Neo4j:iGraph 1
=============PubMed Central Transitions
Gephi:GraphViz 2
Gephi:Neo4j 3
Gephi:iGraph 31
GraphViz:Gephi 19
GraphViz:Neo4j 10
GraphViz:iGraph 58
Neo4j:Gephi 4
Neo4j:GraphViz 4
Neo4j:iGraph 1
iGraph:Gephi 34
iGraph:GraphViz 9
iGraph:Neo4j 13
```

PMC results usually return more papers since search terms like "Neo4j" or "Cytoscape" are being matched to the fulltext, instead of just the title and abstract. This may return more accurate trend tables since sometimes software names are only mentioned in the methods and not in the abstract.

## Publications

* J. Chang and H. Chou, "[Cavatica: A pipeline for identifying author adoption trends among software or methods](https://www.computer.org/csdl/proceedings/bibm/2017/3050/00/08217990-abs.html)," 2017 IEEE International Conference on Bioinformatics and Biomedicine (BIBM), Kansas City, MO, USA, 2017, pp. 2145-2150.

