# SNPacTF
Discrimination tool for rSNPs

## Author
Ahmed Karam

## Requirements

#### Python3
- Download and install any version of python from the main website (https://www.python.org/)
- NOTE: make sure that your processor architecture (32-bit or 64-bit) in your device is compatible with python

#### Biopython
- On the official biopython website (https://biopython.org/) you will find details on downloading and installation.
- We recommend that you use pip to install biopython. *pip install biopython*

## Run

Example command:
#### **python3 SNPacTF.py --snp_table '/path/to/snp_table.csv' --snp_fasta '/path/to/snp_fasta.fasta' --comparison_table '/path/to/comparison.tsv' --motif_db '/path/to/motif_databases' --output '/path/to/output/folder' --prefix 'prefix'**

##### Arguments:
- -h = show this help message and exit
- --snp_table = Input SNP Table (Full Path)
- --snp_fasta = Input SNP Fasta (Full Path)
- --comparison_table = Input Comparison Table (Full Path)
- --motif_db = Input Folder/Directory Name (Full Path)
- --output = Output Folder/Directory Name (Full Path)
- --prefix = File Name Prefix

## Input Files Description
### Input SNP Table Example
#### How to get the table?
Enter the Ensembl homepage, then in the search field in the middle of the page, enter **ENSG00000139618** and press Go.
Choose the search result that contains **ENSG00000139618**, it will appear with a page with information about the gene, in the list on the left of the page there is an option **variant table**, click on it, the table will appear with you. You can filter the SNPs according to their locations through the **Consequences** option located directly above the table.
The table can be downloaded from an icon similar to an Excel file located at the top right of the table.
Download the table, open the file in Excel, and copy the **variant_ID column** to get a FASTA file containing the sequences of SNPs.
### - If you are going to use another source, make sure the SNP information is in the same order as the table that comes from Ensembl.

#### This is an example from the Ensembl Plants database for the TraesCS7D02G364900 gene and the table has been filtered to get the upstream gene variant.
```
"Variant ID",vf,Location,"Chr: bp",vf_allele,Alleles,Class,Source,Evidence,"Clin. Sig.","Conseq. Type",AA,"AA coord","AA coord",sift_sort,sift_class,SIFT,Transcript
Cadenza1015.chr7D.471217381,43266487,7D:471217381,7D:471217381,A,G/A,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza1184.chr7D.471217437,43266488,7D:471217437,7D:471217437,A,G/A,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza1734.chr7D.471217461,43266489,7D:471217461,7D:471217461,A,G/A,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza0917.chr7D.471217478,43266490,7D:471217478,7D:471217478,T,C/T,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza1567.chr7D.471217483,43266491,7D:471217483,7D:471217483,T,C/T,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza1726.chr7D.471217528,43266492,7D:471217528,7D:471217528,A,G/A,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza0951.chr7D.471217538,43266493,7D:471217538,7D:471217538,G,C/G,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
Cadenza2056.chr7D.471217538,43266494,7D:471217538,7D:471217538,G,C/G,SNP,"EMS-induced mutation",,,"upstream gene variant",,,,,-,,TraesCS7D02G364900.1
```

### Input SNP Fasta Example

On the Ensembl homepage, you will find **Biomart at the top**, then select the Ensembl variation database and choose the organism you are dealing with, then left click on **Filters**, then from **GENERAL VARIANT FILTERS** enter the **variant_ID list in the Filter by Variant name option**.
Then click on **Attributes**, then **Flanking Sequences**, then enter an **equal number of upstreams and downstreams**, such as 50 and 50.
Then in the top left, click on **Results**.
And download the file by clicking on the word **Go** at the top right.
### - NOTE: If you are going to use another source, make sure that the SNP is in the middle of the sequence and is an underscore (_).

#### In this example the list of variant_IDs is searched in the table of SNPs extracted above. The database used in this example was Ensembl Plants, the Ensembl variations database, and Triticum aestivum was the organism used.
```
>7D|471217381|471217381|Cadenza1015.chr7D.471217381|EMS-induced mutation|G/A
TCGGAGCTCGCGGCAGCGAAGCAGGGTCTGAGAAGACGGTAATGGGGTATTGCTCGGCTC
TGCTCTGCAGGAGGCAAATCGCGAGCGGTATTTATAGGAG_GCCGAGGGGGGAGGGGCCC
AGGCGTCAGCGAGTGGTGGTTGGGGTGAGGGAGATGGCAACGGAGGCCGAGGGGGATGGA
GGAGCCGAAGAGTAAAACGTG
>7D|471217528|471217528|Cadenza1726.chr7D.471217528|EMS-induced mutation|G/A
AGGGAGATGGCAACGGAGGCCGAGGGGGATGGAGGAGCCGAAGAGTAAAACGTGACGGCG
TGTTGATGGCGCTACCCTGCGGATTTTGGATTTATTAAAG_GGTCGGTGACTCAGCCATG
GCGTGGAGCTACGCCTGTGGATGACAGCAACAGCTCATGCCGTCTGTTTTCTGCCTTTTT
GCTAGGGCCTATTTTCATTTC
>7D|471217538|471217538|Cadenza0951.chr7D.471217538|EMS-induced mutation|C/G
CAACGGAGGCCGAGGGGGATGGAGGAGCCGAAGAGTAAAACGTGACGGCGTGTTGATGGC
GCTACCCTGCGGATTTTGGATTTATTAAAGGGGTCGGTGA_TCAGCCATGGCGTGGAGCT
ACGCCTGTGGATGACAGCAACAGCTCATGCCGTCTGTTTTCTGCCTTTTTGCTAGGGCCT
ATTTTCATTTCCTTCCTCATC
>7D|471217478|471217478|Cadenza0917.chr7D.471217478|EMS-induced mutation|C/T
GAGGGCCGAGGGGGGAGGGGCCCAGGCGTCAGCGAGTGGTGGTTGGGGTGAGGGAGATGG
CAACGGAGGCCGAGGGGGATGGAGGAGCCGAAGAGTAAAA_GTGACGGCGTGTTGATGGC
GCTACCCTGCGGATTTTGGATTTATTAAAGGGGTCGGTGACTCAGCCATGGCGTGGAGCT
ACGCCTGTGGATGACAGCAAC
>7D|471217483|471217483|Cadenza1567.chr7D.471217483|EMS-induced mutation|C/T
CCGAGGGGGGAGGGGCCCAGGCGTCAGCGAGTGGTGGTTGGGGTGAGGGAGATGGCAACG
GAGGCCGAGGGGGATGGAGGAGCCGAAGAGTAAAACGTGA_GGCGTGTTGATGGCGCTAC
CCTGCGGATTTTGGATTTATTAAAGGGGTCGGTGACTCAGCCATGGCGTGGAGCTACGCC
TGTGGATGACAGCAACAGCTC
>7D|471217437|471217437|Cadenza1184.chr7D.471217437|EMS-induced mutation|G/A
GCTCTGCTCTGCAGGAGGCAAATCGCGAGCGGTATTTATAGGAGGGCCGAGGGGGGAGGG
GCCCAGGCGTCAGCGAGTGGTGGTTGGGGTGAGGGAGATG_CAACGGAGGCCGAGGGGGA
TGGAGGAGCCGAAGAGTAAAACGTGACGGCGTGTTGATGGCGCTACCCTGCGGATTTTGG
ATTTATTAAAGGGGTCGGTGA
>7D|471217461|471217461|Cadenza1734.chr7D.471217461|EMS-induced mutation|G/A
GCGAGCGGTATTTATAGGAGGGCCGAGGGGGGAGGGGCCCAGGCGTCAGCGAGTGGTGGT
TGGGGTGAGGGAGATGGCAACGGAGGCCGAGGGGGATGGA_GAGCCGAAGAGTAAAACGT
GACGGCGTGTTGATGGCGCTACCCTGCGGATTTTGGATTTATTAAAGGGGTCGGTGACTC
AGCCATGGCGTGGAGCTACGC
```

### Input Comparison Table Example

We get the orthologous sequences from several methods, and the easiest way is BLASTn.
We use MEME online tool to get the predicted motif from orthologous sequences. Then we make a submission for the predicted motifs to be compared with the known motifs using Tomtom.
The result is a tab separated table. It contains an important line at the end, which is the command line with which the program was run.
If you use another source, make sure that the information is as it is formatted in the Tomtom table and contains the last line, as we will explain shortly.

```
Query_ID	Target_ID	Optimal_offset	p-value	E-value	q-value	Overlap	Query_consensus	Target_consensus	Orientation
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0936.1	-12	0.00609338	3.99726	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TTGCGTGT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1697.1	-8	0.00653619	4.28774	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TTCTTGTCGTGT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1417.1	-10	0.00835446	5.48053	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GATGACGTGGCAC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0986.1	-38	0.0113636	7.45451	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CACCGACA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0992.2	-33	0.0116765	7.65976	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TATGACGGCGGC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1007.1	-38	0.014394	9.44245	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CACCGACA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1023.1	-38	0.014394	9.44245	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CACCGACA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1831.1	-35	0.0149483	9.80609	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGACGGCGACGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0589.1	0	0.020544	13.4769	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TTGACCGAGCC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1331.1	-23	0.0218971	14.3645	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCACGTGTGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1346.1	-33	0.023526	15.433	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GATGATGACGTCACT	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2022.1	-17	0.0275823	18.094	1	17	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGCGGCGGCGGCGGCGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1815.1	-18	0.0333898	21.9037	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCAGCTGCTGCTG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0097.1	-10	0.0357096	23.4255	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GATGACGTGGCC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0579.1	-13	0.0358444	23.5139	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCGCTGAGCC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1817.1	-21	0.0371913	24.3975	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCGGCGGCGGCGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2021.1	-24	0.0392323	25.7364	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GAGACGGTGGAGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1332.1	-23	0.0403371	26.4611	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCACGTGTGA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2029.1	-17	0.0413717	27.1398	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGGAGGAGCGTGT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1669.1	-31	0.0414539	27.1938	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGATGTCGGCAAA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1333.1	-23	0.0427594	28.0502	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCACGTGTGA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1070.2	-34	0.0429775	28.1932	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGATGACGTCATCA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0587.1	-16	0.0433854	28.4608	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GTGGACCCGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0096.1	-11	0.0436285	28.6203	1	7	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGACGT	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1047.2	-34	0.0451168	29.5966	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGATGACGTCATCA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1805.1	-14	0.0479924	31.483	1	9	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCGTTGACT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1826.1	-15	0.048253	31.654	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCGCACGTGCGCG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0571.1	-23	0.049192	32.27	1	21	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TTCACCTCGGGAACTGTGCCA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1664.2	-26	0.0497817	32.6568	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCTTCTGGAAGC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1748.1	-34	0.0511612	33.5618	1	9	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGTCGGCA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1068.2	-34	0.0546559	35.8543	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGATGACGTCATCA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1218.1	-32	0.0594299	38.986	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGATGTCGGCGAA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1424.1	-21	0.0600698	39.4058	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCTGTGTCGGTGGCG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1075.1	-15	0.0610917	40.0761	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGTTGACC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1086.1	-14	0.0623514	40.9025	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GTGTTGACTT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1226.1	-20	0.0629524	41.2968	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGTGGAGGCGGTGGA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1084.1	-15	0.0656998	43.0991	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGTTGACC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0971.1	-34	0.0662217	43.4414	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGTCGGCAA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1021.1	-26	0.070668	46.3582	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCACGTGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1083.2	-11	0.0714141	46.8477	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TAAGCGTTGACTTT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1231.2	-20	0.0714141	46.8477	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGCGGCGGCTAAGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1069.2	-32	0.0723529	47.4635	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGATGACGTCATCAT	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0998.1	-11	0.0746012	48.9384	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGGCGGCGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2013.1	-21	0.0757509	49.6926	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCTGCGGCGGCGACG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0978.1	-34	0.0759827	49.8447	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGTCGGC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2017.1	-8	0.078529	51.515	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATCACGGCGAGTAT	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1220.1	-21	0.0792879	52.0129	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATTTTGTCGGTGGAG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1819.1	-36	0.0803641	52.7188	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGCGGCGGCGGC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1828.1	-15	0.0803641	52.7188	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGTGGACCACGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1004.1	-12	0.0816271	53.5474	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGGCGGCG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1312.1	-10	0.08231	53.9953	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ACCGGCGTTGACTT	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1225.1	-19	0.0829681	54.427	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGGCGGCGGCGGTGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1793.1	-29	0.0838649	55.0154	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TATGGATAAG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1335.1	-32	0.0874327	57.3559	1	11	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGATGACGTCA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1693.1	-32	0.0881532	57.8285	1	13	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	AACAGACAGCAAG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA2011.1	-36	0.0889997	58.3838	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ACCACCGACACC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1345.1	-2	0.0903421	59.2645	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GATGCTGACGTGGC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0962.1	-26	0.0938898	61.5917	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCACGTGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1074.1	-26	0.0938898	61.5917	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCACGTGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1240.1	-17	0.0986382	64.7066	1	21	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGCGGCGGCGGAGGCGGTGGA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1221.1	-22	0.0992001	65.0753	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGGCGGCGGCGGAGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1228.1	-21	0.10025	65.7643	1	17	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GCGGCGGCGGCGGCGGC	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0128.1	-12	0.100514	65.9369	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ACACGTGG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA0567.1	-4	0.100514	65.9369	1	8	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CGCCGCCA	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1246.1	-17	0.102344	67.1376	1	21	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GGCGGCGGTGGCGGCGGCGGA	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1305.1	-13	0.103398	67.8293	1	12	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	AGCGTTGACTTT	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1336.1	-34	0.103636	67.9849	1	14	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	ATGATGACGTCATC	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1685.1	-27	0.103656	67.9987	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	CTAATGGGAGACACG	+
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1753.1	-19	0.103656	67.9987	1	15	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	TGGCGGCGGCGGTGG	-
GTGACTCAGCCATGGCGTGGAGCTRCGCCTGTGGATGACAGCRACASCTC	MA1405.1	-32	0.10518	68.9981	1	10	GTGACTCAGCCATGGCGTGGAGCTACGCCTGTGGATGACAGCGACAGCTC	GACTGACAGT	+

# Tomtom (Motif Comparison Tool): Version 5.4.1 compiled on Aug 25 2021 at 17:37:53
# The format of this file is described at https://meme-suite.org/meme/doc/tomtom-output-format.html.
# tomtom -no-ssc -oc . -verbosity 1 -min-overlap 5 -mi 1 -dist pearson -evalue -thresh 70.0 -time 300 query_motifs db/JASPAR/JASPAR2022_CORE_plants_non-redundant_v2.meme
```
This line ```# query_motifs db/database_name/database_branch.meme``` will be essential if you are using a program other than **Tomtom**. You will put the main part which is ```# query_motifs db/``` , and then write the name of the database file in meme format and the name of the folder in which the file is located. Put the line at the comparison file (following the comparison table).

### Input Folder/Directory Name

Basically, SNPacTF works with the database in the MEME website. You must download it and enter the motif_databases folder path as the main entry for SNPacTF.
If you want an alternative source, do the following:

Enter the path of the folder containing the folders containing the meme files.
Example:
```/home/SNPacTF/motif_databases``` contains JASPAR folder and ARABD which are database folders.
```/home/SNPacTF/motif_databases/JASPAR/``` contains meme files for different sections.
So the required path is ```/home/SNPacTF/motif_databases```
