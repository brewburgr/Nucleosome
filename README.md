# Nucleosome
Code collection for Nucleosome pattern project


In BA_functions.py, a number of functions are defined and used throughout the code. Here they are explained:
(The ones that are not so releveantat this point are put in brackets, i.e. they are not really relevant anymore but i still kept them for documenting reasons. I will probably sort them out at the end of this project, but right now it is not foreseeable if they will be needed again.)
A better ordering is on its way, up until now i only added them consecutively.

**reset_weights(model)**: Resets the weigths of the model
**binaryalldirections()**: Returns the (4001,) binary data of all directions directly from 'sujeetClassChr1_all'
**binaryalldirections8000()**: Returns the (8001,) binary data of all directions directly from 'chr1_ctcfbin'
**sparsealldirections(binaryalldirections)**: self-explanatory
**getsparse(df,readingdirection,numnuc)**: returns the sparserep for a reading direction (4,5,6 or 7) and the number of nucleosomes (numnuc) that should be taken into account

**sparserep(array,length)**: turns a binary representation in array into a sparse representation, accounting for the #length nearest nucleosomes around the center of the sample (which is for our data usually corresponding to a CTCF site)
**sparserepedges(array,length, treshold)**: same as sparserep, but we only take into account the area outside of +-#treshold bp around the center
**(removehighwidths(df,dfwidths,treshold))**: removes data (created by sparserep) where nucleosomes have a higher width than #treshold. Also returns the index of the parts of the original positions that are not removed for later reference
**Modelsparse(arraylen)**: returns an autoencoder (full model, encoder, decoder) who can be trained on sparserep data, where arraylen = length.
**Modelsparsevae(arraylen)**: same as modelsparse, but variationalautoencoder
**saveindices(arrays,description)**: saves an array with indices into google sheet in drive (which has to be created and set up beforehand) and adds the description aswell.
**getindices(column)**: reads and returns indices of the respective column (just counting through from left to right, starting at 1) of the mentioned google sheet.
**training(model, lra,bs,ep,dataset,reset,vb)**: trains an autoencoder model where input=output=dataset, lra:learningrate, bs: batch size, ep: epochs, reset: 0 or 1, vb=0,1,2; displays different amount of information
**traininglabels(model, lra,bs,ep,dataset,labels,reset,vb)**: same as training, but here output=labels is different to input=dataset
**latrep(encoder,Data,label)**: creates plot of latentrepresentation of an encoder. label will be shown as a description in the legend of the graph. Returns latent representations as arrays a,b.
**latrepmulti(encoder,Datas,labels)**: multiple latent representations, so Datas and labels have to be arrays with the separate datasets that should be shown. No data returned.
**latrepmulti3d(encoder,Datas,labels,elev,az)**: Same as above, but for 3d-latent representations. with elev and az you can set the viewing perspective of the parameters.
**latrepmultivae(encoder,Datas,labels)**: Same as laterepmulti, but for data from variational autoencoder that needs to be treated differently.
**(latreplengthindex(encoder,Data,lengthindex,lower,higher))**: Plots data of different lengths in different colours.
**latrepclustered(encoder,Data,clustercolumn)**: Plots data of different clusters in different colors. Clusters are loaded from the google sheet also used in saveindices and getindices; clustercolumn refers to respective column (just counting through from left to right, starting at 1)

**largestlengthdata(Data,len3,num)**: Returns only datas that have the maximum number of nucleosomes on each side.
**clusters(lrep,clusters)**: creates a number (#cluster) of clusters of a latent representation and returns the respective indices
**(lengthindex(len3,maxlen))**: returns an (#maxlen x #maxlen) list lengthind where the respective entries relate to the number of nucleosomes to the right and left side of the centre (e.g. lengthind[4][5] contains the indices for all data samples who have 4 nucleosomes to the left and 5 to the right in this dataset)
**hamm(a,b)**: Hamming Distance of two objects
**n_analysis(part)**: returns 27x27 matrices for an array of (4001,)-shaped binary samples(part), where the entries correspond to the hamming distances between different parts of the samples (window size 149bp)

**hamtopca(data0,n_components)**: returns PCA reduced representation (with n_components number of components) of an array of samples data0, the samples have to be 2D (as the matrices from n_analysis)

**directpca(data,n_components)**: basically n_analysis and hamtopca in one step
**hammodel(numbereigs)**: returns full model, encoder and decoder of an autoencoder which can be used for the pca data. numbereigs refers to the input dimension (should be the same as n_components if the data from the functions defined before is used).


**hammodel3(numbereigs)**: same as hammodel, but bottleneck has 3 nodes instead of 2.
**cnn(inputshape)**: fully convolutional autoencoder model suited for (2,2000) data
**cnn8k()**:fully convolutional autoencoder model suited for (2,4000) data

**sparsealldirections(binaryalldirections)**: self-explanatory

**fcndata(binarydata,treshold)**: prepares data for cnn from the binarydata. treshold should be set to zero.

**fcndata8k(binarydata,treshold)**: prepares data for cnn8k from the binarydata. treshold should be set to zero.
**similarity(model,hamdata,indexof)**: returns the similarity score (siamese network) of a model with all other hamming distance data
**similarityplot(model,hamdata,indexof)**: also similarity score but with a plot
****
