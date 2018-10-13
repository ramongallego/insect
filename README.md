[![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/insect)](https://cran.r-project.org/package=insect)
[![CRAN\_Downloads\_Badge](http://cranlogs.r-pkg.org/badges/grand-total/insect)](https://cran.r-project.org/package=insect)
[![DOI](https://zenodo.org/badge/87808693.svg)](https://zenodo.org/badge/latestdoi/87808693)
[![ORCiD](https://img.shields.io/badge/ORCiD-0000--0002--7332--7931-brightgreen.svg)](http://orcid.org/0000-0002-7332-7931)
[![Build\_Status](https://travis-ci.org/shaunpwilkinson/insect.svg?branch=master)](https://travis-ci.org/shaunpwilkinson/insect)
[![Project\_Status](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active)
[![License](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)

------------------------------------------------------------------------

### Informatic sequence classification trees

`insect` is an R package for taxonomic identification of amplicon
sequence variants generated by DNA meta-barcoding analysis. The learning
and classification algorithms implemented in the package are based on
full probabilistic models (profile hidden Markov models) and offer
highly accurate taxon IDs, albeit at a relatively high computational
cost.

The package also contains functions for searching and downloading
reference sequences and taxonomic information from NCBI, a "virtual PCR"
tool for sequence trimming, a function for "purging" erroneously labeled
reference sequences, and several other handy tools.

`insect` is designed to be used in conjunction with the
[dada2](https://benjjneb.github.io/dada2/index.html) pipeline or any
other de-noising tool that produces a list of amplicon sequence variants
(ASVs). While unfiltered sequences can also be processed with high
accuracy, the **insect** classification algorithm is relatively slow,
since it uses a computationally intensive dynamic programming algorithm
to find the likelihood values of each sequence given the models at each
node of the classification tree. Hence an appropriately filtered input
dataset will generally be much faster to process.

### Installation

To download **insect** from CRAN and load the package, run

    install.packages("insect")
    library(insect)

To download the latest development version from GitHub, run:

    devtools::install_github("shaunpwilkinson/insect", build_vignettes = TRUE) 
    library(insect)

### Classifying sequences

Training an **insect** classifier will be the subject of another
tutorial; however, several classifiers are already available for some of
the more common metabarcoding primer sets:

<!-- note newlines needed between html tags and code chunk -->
<table>
<thead>
<tr class="header">
<th align="left">Marker</th>
<th align="left">Target</th>
<th align="left">Primers</th>
<th align="left">Source</th>
<th align="left">Version</th>
<th align="right">Date</th>
<th align="left">Download</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">16S</td>
<td align="left">Marine crustaceans</td>
<td align="left">Crust16S_F/Crust16S_R (<a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5528208/">Berry et al 2017</a>)</td>
<td align="left">GenBank</td>
<td align="left">4</td>
<td align="right">20180626</td>
<td align="left"><a href="https://www.dropbox.com/s/9vl9gj3frw7ng1m/classifier.rds?dl=1">RDS (7.1 MB)</a></td>
</tr>
<tr class="even">
<td align="left">16S</td>
<td align="left">Marine fish</td>
<td align="left">Fish16sF/16s2R (<a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5528208/">Berry et al 2017</a>; <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1959119/">Deagle et al 2007</a>)</td>
<td align="left">GenBank</td>
<td align="left">4</td>
<td align="right">20180627</td>
<td align="left"><a href="https://www.dropbox.com/s/fvfrd46exdah037/classifier.rds?dl=1">RDS (6.8MB)</a></td>
</tr>
<tr class="odd">
<td align="left">18S</td>
<td align="left">Marine eukaryotes</td>
<td align="left">18S_1F/18S_400R (<a href="https://www.ncbi.nlm.nih.gov/pubmed/24023913">Pochon et al 2017</a>)</td>
<td align="left">SILVA_132_LSUParc, GenBank</td>
<td align="left">5</td>
<td align="right">20180709</td>
<td align="left"><a href="https://www.dropbox.com/s/rmhh1g73jtipagu/classifier.rds?dl=1">RDS (11.8 MB)</a></td>
</tr>
<tr class="even">
<td align="left">18S</td>
<td align="left">Marine eukaryotes</td>
<td align="left">18S_V4F/18S_V4R (<a href="https://www.ncbi.nlm.nih.gov/pubmed/28947818">Stat et al 2017</a>)</td>
<td align="left">GenBank</td>
<td align="left">4</td>
<td align="right">20180525</td>
<td align="left"><a href="https://www.dropbox.com/s/s315gxuo4p24kx8/classifier.rds?dl=1">RDS (11.5 MB)</a></td>
</tr>
<tr class="odd">
<td align="left">23S</td>
<td align="left">Algae</td>
<td align="left">p23SrV_f1/p23SrV_r1 (<a href="https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1529-8817.2007.00341.x">Sherwood &amp; Presting 2007</a>)</td>
<td align="left">SILVA_132_LSUParc</td>
<td align="left">1</td>
<td align="right">20180715</td>
<td align="left"><a href="https://www.dropbox.com/s/6o8cauqrlgnmwp5/classifier.rds?dl=1">RDS (26.9MB)</a></td>
</tr>
<tr class="even">
<td align="left">COI</td>
<td align="left">Metazoans (amino)</td>
<td align="left">mlCOIintF/jgHCO2198 (<a href="https://frontiersinzoology.biomedcentral.com/articles/10.1186/1742-9994-10-34">Leray et al 2013</a>)</td>
<td align="left">Midori, GenBank</td>
<td align="left">4aa</td>
<td align="right">20181009</td>
<td align="left"><a href="https://www.dropbox.com/s/c987wohded37cxg/classifier.rds?dl=1">RDS (47 MB)</a></td>
</tr>
<tr class="odd">
<td align="left">COI</td>
<td align="left">Metazoans (marine only)</td>
<td align="left">mlCOIintF/jgHCO2198 (<a href="https://frontiersinzoology.biomedcentral.com/articles/10.1186/1742-9994-10-34">Leray et al 2013</a>)</td>
<td align="left">Midori, GenBank</td>
<td align="left">4mo</td>
<td align="right">20181009</td>
<td align="left"><a href="https://www.dropbox.com/s/vn1yit2wkug9f7p/classifier.rds?dl=1">RDS (34.1 MB)</a></td>
</tr>
<tr class="even">
<td align="left">COI</td>
<td align="left">Metazoans (no third codon positions)</td>
<td align="left">mlCOIintF/jgHCO2198 (<a href="https://frontiersinzoology.biomedcentral.com/articles/10.1186/1742-9994-10-34">Leray et al 2013</a>)</td>
<td align="left">Midori, GenBank</td>
<td align="left">4nt</td>
<td align="right">20181009</td>
<td align="left"><a href="https://www.dropbox.com/s/bfvqnggi4jt591i/classifier.rds?dl=1">RDS (51.9 MB)</a></td>
</tr>
<tr class="odd">
<td align="left">ITS2</td>
<td align="left">Cnidarians and sponges</td>
<td align="left">scl58SF/scl28SR (<a href="https://www.dropbox.com/s/6hcs1goju60wqi4/README.txt?dl=1">Wilkinson et al in prep</a>)</td>
<td align="left">GenBank</td>
<td align="left">5</td>
<td align="right">20180920</td>
<td align="left"><a href="https://www.dropbox.com/s/f07cka6308ebk2o/classifier.rds?dl=1">RDS (6.6 MB)</a></td>
</tr>
</tbody>
</table>

To classify a sequence or set of sequences, first read them into R as a
"DNAbin" list object. FASTA files can be parsed as follows:

    x <- readFASTA("<path-to-file>.fasta")

Alternatively users may wish to assign taxon IDs to the output from the
[DADA2](https://www.nature.com/articles/nmeth.3869) pipeline, in which
case the column names of the ouput table can be parsed as in the
following example:

    data("samoa") 
    x <- char2dna(colnames(samoa))
    ## name the sequences sequentially
    names(x) <- paste0("ASV", seq_along(x))

The next step is to download and read in the classifier. It is important
to ensure that the classifier was trained using the same primer set as
that used to generate the query data. In this example the data were
generated from autonomous reef monitoring structures in American Samoa
(ARMS) using the COI metabarcoding primers mlCOIintF and jgHCO2198
([Leray et al
2013](https://frontiersinzoology.biomedcentral.com/articles/10.1186/1742-9994-10-34)),
and de-noised, filtered and merged following the [DADA2
tutorial](https://benjjneb.github.io/dada2/tutorial.html).

There are currently three classifiers available for this primer set, a
[marine
only](https://www.dropbox.com/s/vn1yit2wkug9f7p/classifier.rds?dl=1)
version, one for DNA sequences with every third codon position removed
([nothirds](https://www.dropbox.com/s/bfvqnggi4jt591i/classifier.rds?dl=1)),
and one for translated amino acid sequences
([amino](https://www.dropbox.com/s/c987wohded37cxg/classifier.rds?dl=1)).

Here we'll use the amino acid version, which was created by translating
the [MIDORI UNIQUE 20180221](http://reference-midori.info/download.php)
training dataset using the
[EBI5](https://www.ebi.ac.uk/ena/browse/translation-tables) invertebrate
mitochondrial translation table.

The 47 MB classifier can be downloaded to the current working directory
and read into R as follows:

    download.file("https://www.dropbox.com/s/c987wohded37cxg/classifier.rds?dl=1", 
                  destfile = "classifier.rds", mode = "wb")
    classifier <- readRDS("classifier.rds")

Now we need to translate the amplicon sequence variants (ASVs) to amino
acid sequences using the same number 5 translation table. Before this,
any sequences whose length is not divisible by three should be
discarded. The sequences are then converted to character type for
translation with the `translate` function in the
[seqinr](https://cran.r-project.org/package=seqinr) package, and
converted back to binary form object using `ape::as.AAbin`.

    keeps <- sapply(x, length) %% 3 == 1L
    x <- x[keeps]
    x <- ape::as.character.DNAbin(x)
    x <- lapply(x, seqinr::translate, numcode = 5, frame = 1)
    x <- ape::as.AAbin(x)

Now we need to check that none of the translated sequences contain stop
codons:

    keeps <- sapply(x, function(v) !any(v == as.raw(42)))
    x <- x[keeps]

Finally, the amino acid sequences are passed to the classifier for taxon
ID assignment. There is an option to perform a nearest-neighbor search
prior to the computationally-expensive recursive model test procedure,
which can save time and improve resolution ('recall') at lower taxonomic
ranks. Note that this can be a double-edged sword; if multiple species
share an identical or near-identical sequence, and the true taxon of the
query sequence is missing from the trainingset, the algorithm may
over-classify the sequence and return a congeneric taxon. To perform a
nearest-neighbor search with a similarity threshold of say 0.99 (meaning
any sequence in the trainingset with a similarity greater than or equal
to 0.99 is considered a match), set `ping = 0.99`. To stay on the safe
side, we will set `ping = 1` (i.e. only sequences with 100% identity are
considered matches).

    out <- classify(x, classifier, cores = 2, ping = 1)

<!-- note newlines needed between html tags and code chunk -->
<table>
<thead>
<tr class="header">
<th align="left">representative</th>
<th align="right">taxID</th>
<th align="left">taxon</th>
<th align="left">rank</th>
<th align="right">score</th>
<th align="left">kingdom</th>
<th align="left">phylum</th>
<th align="left">class</th>
<th align="left">order</th>
<th align="left">family</th>
<th align="left">genus</th>
<th align="left">species</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ASV1</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9966</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV2</td>
<td align="right">6379</td>
<td align="left">Chaetopterus</td>
<td align="left">genus</td>
<td align="right">0.9881</td>
<td align="left">Metazoa</td>
<td align="left">Annelida</td>
<td align="left">Polychaeta</td>
<td align="left">Spionida</td>
<td align="left">Chaetopteridae</td>
<td align="left">Chaetopterus</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV3</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9769</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV4</td>
<td align="right">116569</td>
<td align="left">Neocopepoda</td>
<td align="left">infraclass</td>
<td align="right">0.9986</td>
<td align="left">Metazoa</td>
<td align="left">Arthropoda</td>
<td align="left">Hexanauplia</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV5</td>
<td align="right">33213</td>
<td align="left">Bilateria</td>
<td align="left">no rank</td>
<td align="right">0.9456</td>
<td align="left">Metazoa</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV6</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9973</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV7</td>
<td align="right">39820</td>
<td align="left">Nereididae</td>
<td align="left">family</td>
<td align="right">0.9110</td>
<td align="left">Metazoa</td>
<td align="left">Annelida</td>
<td align="left">Polychaeta</td>
<td align="left">Phyllodocida</td>
<td align="left">Nereididae</td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV8</td>
<td align="right">1</td>
<td align="left">root</td>
<td align="left">no rank</td>
<td align="right">1.0000</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV9</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9147</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV11</td>
<td align="right">2759</td>
<td align="left">Eukaryota</td>
<td align="left">superkingdom</td>
<td align="right">1.0000</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV12</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9424</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV13</td>
<td align="right">2759</td>
<td align="left">Eukaryota</td>
<td align="left">superkingdom</td>
<td align="right">0.9999</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV14</td>
<td align="right">33213</td>
<td align="left">Bilateria</td>
<td align="left">no rank</td>
<td align="right">0.9456</td>
<td align="left">Metazoa</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">ASV15</td>
<td align="right">2806</td>
<td align="left">Florideophyceae</td>
<td align="left">class</td>
<td align="right">0.9530</td>
<td align="left"></td>
<td align="left"></td>
<td align="left">Florideophyceae</td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">ASV16</td>
<td align="right">39820</td>
<td align="left">Nereididae</td>
<td align="left">family</td>
<td align="right">NA</td>
<td align="left">Metazoa</td>
<td align="left">Annelida</td>
<td align="left">Polychaeta</td>
<td align="left">Phyllodocida</td>
<td align="left">Nereididae</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>

Any sequences that return exact hits (or near matches if `ping = 0.99`
or similar) with at least one training sequence are assigned a score of
`NA`, as in the final row of the table above. Here, the multiple
matching sequences have a Nereid polychaete common ancestor, and the
query sequence was therefore assigned to the family Nereididae.

### Further reading

A more detailed overview of the package and its functions can be found
[here](https://rpubs.com/shaunpwilkinson/insect) or by running

    vignette("insect-vignette")

### Issues

If you experience a problem using this software please feel free to
raise it as an issue on
[GitHub](http://github.com/shaunpwilkinson/insect/issues).

### Acknowledgements

This software was developed at [Victoria University of
Wellington](http://www.victoria.ac.nz/) with funding from a Rutherford
Foundation Postdoctoral Research Fellowship award from the Royal Society
of New Zealand.
