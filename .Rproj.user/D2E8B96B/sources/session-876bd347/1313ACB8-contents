# Installing and Loading the rentrez Package:
if (!requireNamespace("rentrez", quietly = TRUE)) {
  install.packages("rentrez")
}

# Loading the rentrez package for interacting with GenBank:
library(rentrez)

# Fetching Sequences from GenBank

# Define the GenBank IDs for Borrelia burgdorferi 16S gene sequences
ncbi_ids <- c("HQ433692.1", "HQ433694.1", "HQ433691.1")

Bburg<-entrez_fetch(db = "nuccore", id = ncbi_ids, rettype = "fasta")
# This code creates a vector of IDs and then uses entrez_fetch() to retrieve the corresponding sequences.

# The object Bburg is one long character string containing three FASTA-formatted sequences so we need to split this string into individual elements:
# Split the fetched FASTA data into separate sequences.
# The lookahead regex (?=>) ensures we split before each header starting with ">"
Sequences <- strsplit(Bburg, "\n\n")
print(Sequences)

# Extracting Headers and Sequences:
Sequences<-unlist(Sequences)
header<-gsub("(^>.*sequence)\\n[ATCG].*","\\1",Sequences)
seq<-gsub("^>.*sequence\\n([ATCG].*)","\\1",Sequences)
Sequences<-data.frame(Name=header,Sequence=seq)

# Writing the processed sequences to a CSV file:
write.csv(Sequences, file = "Sequences.csv", row.names = FALSE)