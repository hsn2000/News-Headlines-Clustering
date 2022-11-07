# Document Clustering by extracting sequences from Word of Graph

### Introduction:<br>
Document Clustering is a data clustering problem that focuses on objects that are in the form of documents. The major focus of this procedure is to arrange similar documents into a single group (cluster) that are related in some way, such as document type, content, and so on. The difficult element is determining which features are relevant for clustering and how many classes of such groupings (cluster) exist in the data set. Document Clustering seeks to group documents in such a way that documents within a cluster are comparable (i.e. high intra cluster similarity) while remaining are in other clusters (low inter cluster similarity). It is an unsupervised strategy in which the primary priority of the document clustering method is to identify and classify the unknown aspects of data in a document. 
All traditional approaches, which rely on attributes such as terms and phrases, ignore the context in which the text was used. These methods concentrate solely on clustering, regardless of the context. We presented a new document clustering method that more effectively represents the context of text than earlier methods. Although document representation in terms of word-of-graph, in which each unique word represents the edges and directed vertices among them, is an effective technique that preserves the order in which the words were initially used, comparing graphs is a time-consuming job. We extract word sequences from this directed graph in this technique, which not only minimizes the number of words utilized in document representation but also relieves the tedious task of document comparison. Finally, the clustering on the new headlines dataset is done using Hierarchical agglomerative clustering. The motivation or goal of clustering textual documents is to automatically group textual documents into clusters based on their content similarity which can be further used for browsing, searching, document organization, topic extraction and fast information retrieval or filtering.

### Methods and Materials:<br>
Python was used to create the algorithm, which was then run on Google Colab, nx.digraph is used to generate the graph. A dataset of 1 million news headlines is being used. Each headline is treated as its own document. Before being used, all of the documents in the specified datasets are preprocessed. Stop words are deleted, and Porter stemmer is used to stem each word.

### Creating word of graph:<br>
The document is represented as a word graph, which is connected to an un-weighted directed graph with vertices representing unique words and edges representing the relationship between the words inside the adjustable window size. The order in which the words were employed determines the orientation of the edges. The basic premise is that all of the words in the text have relationships with each other within the window size, beyond which the relationship is ignored. This method links all co-occurring keywords without considering their meanings.


<img height="300px" src="https://cdn.wccftech.com/wp-content/uploads/2021/07/Spotify.jpg">

                The Word-of-Graph of the document containing news headline "act fire witnesses must be aware of defamation"

An ordered sequence of two or more words is called a word sequence. The document treated as input to the word-sequence is the graph-of-word. We are using two word pairs as a sequence in this approach. The algorithm starts with the first word present in the graph and traverses the entire graph word by word and extracts the two adjacent words that have an edge between them. So we obtain sequences like w1 = {information, retrieval}, w2 = {information, resources} etc. The list of entire sequences present in the document is the final representation of the document and they maintain the correlation between the terms as well the context of the text is intact. 

### Generating Similarity Matrix:<br>
Documents that have similar contextual features should be placed inside same cluster and those having dissimilarity should be part of a different cluster. To find the similarity following formula is used: 

                Similarity = d1∩d2/d1Ud2
 
Where d1 and d2 are documents which belong to the dataset D. Documents that have more sequences in common would have higher similarity measure.

### Clustering:<br>
To cluster the word-sequences extracted from word-of graph, we perform hierarchical clustering on the candidate clusters to obtain the final result. Documents that have similar word-sequences extracted from graph-of-word display similarity and are merged together into one cluster. The same process is repeated again and again until we have all the documents belonging to at least one cluster.

### Data and Results:<br>
As we have mention we have used hierarchal clustering (agglomerative). We’ve implemented its four types to compare the accuracy of the clustering.
1.	Single-Linkage clustering: 
It is based on grouping clusters in bottom-up fashion (agglomerative clustering), at each step combining two clusters that contain the closest pair of elements not yet belonging to the same cluster as each other.
2.	Complete-Linkage clustering:
It is one of several methods of agglomerative hierarchical clustering. Complete-Link clusters at step are maximal sets of points that are completely linked with each other via links of similarity. The method is also known as farthest neighbor clustering.
3.	Average-Linkage clustering:
In Average linkage clustering, the distance between two clusters is defined as the average of distances between all pairs of objects, where each pair is made up of one object from each group.
4.	Ward-Linkage clustering:
Ward suggested a general agglomerative hierarchical clustering procedure, where the criterion for choosing the pair of clusters to merge at each step is based on the optimal value of an objective function.

By comparing different hierarchal linkage method we’ve concluded on the basis of Silhouette Score that Average-Linkage clustering performs better than others although the single-linkage cluster is fast but not perform well on cleanly separated globular clusters. 

### Conclusion:<br>
After analyzing the results, we can safely say that based on the datasets used, the proposed approach of Word Sequence From Word-of-Graph (WSFWS) performs quite well. This approach reduces the size of document as the document is represented in terms of word sequences that are extracted from bag-of-words. This refined document still retains the semantics present in the actual document hence the results keep improving as the documents are increased.

Future work might involve refining our graph-of-word model with weighted edges or proposing a scoring function that challenges the document independence assumption to other applications such as document summarization and phrasal indexing.
