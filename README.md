# MedCS: Medicare Code Similarity software (for Windows 7 or above) 

This software allows you to train word2vec model on the medical claims data and to explore the similarities between the codes. 

  

After you open the folder medicare_code_similarity, you will see: 

- code_explorer	% this is a folder that will enable you to explore medical codes 

   - css directory	% needed for display on browser 

   - js directory	% needed for display on browser 

   - index.html    % the html file is used to run in browser 

  

Three executable files to train the word2vec model: 

- pre_processing.exe	% this file loads synthetic_claim_data.csv file (your input file) and produces “document” file 

- word2vec_train.exe	% this file loads “document” file and produces code2rawcode_file.csv, code_vectors_file.csv  and “model” files. 

- post_procesing.exe	% this file loads “model” file and produces code_index.csv, code_pmi.csv,                                                                              code_vectors_file.csv files. 

  

Other files: 

- d.csv	% this is ICD9 diagnosis code description file, we need it to show the code description. You can replace it with the icd9 diagnosis codes that correspond to your data. 

- p.csv	% this is ICD9 procedure code description file, we need it to show the code description. You can replace it with the icd9 procedure codes that correspond to your data. 

- hcpcsdict.csv	% this is procedure code description in Healthcare Common Procedure Coding System (HCPCS) format, we need it to show the code description. You can replace it with the hcpcs codes that correspond to your data. 

- synthetic_claim_data.csv	% this is the claims data set in a desired csv format. You would need to replace this data set with your own data set written in the same tabular format. 

 

STEP 1 (pre-processing synthetic_claim_data.csv file): 

------------------------------------  

The goal of this step is to convert the original csv file (synthetic_claim_data.csv) into the format needed for model training.  

Click the pre_processing.exe file. It will ask to input the name of the csv file (synthetic_claim_data.csv). 

Then you need to input the names of the columns which contain patient id, claim time, icd 9 diagnosis codes, icd 9 procedure codes and hcpcs codes. 

Then, it will start to process the data. It may take several minutes depending on the size of your data.  

After it is finished, it will ask you to press any button to finish. 

At this time, a file "document” is generated in the same folder.  

  

STEP 2 (train a model):  

------------------------------------  

The goal of this step is to learn from the data how to represent codes as vectors using the word2vec algorithm.  

Click the word2vec_train.exe file. It may take a minute to load this file.  

After it finished loading, you will be prompted to proceed.  

If you input "Y", then it will ask you how much iteration you want to train word2vec. We recommend 10.  

Then it will ask you to set a threshold to filter out rare codes. We recommend 15 (codes occurring less than 15 times in your data will be ignored). 

Then it will start to train the model. After training is finished, code_vectors_file.csv, code2rawcode_file.csv and "model" files are generated in the folder.  

After it is finished, it will ask you to press any button to finish. 

  

STEP 3 (post-processing):  

------------------------------------  

The goal of this step is to generate three csv files from the trained word2vec model that store cosine similarity, pmi value and code dictionary index.  

Click the post_process.exe file, the program may take up to 30 minutes depending on the size of your dataset.  

Do not close the terminal while it is running. After it is finished, it will ask you to press any button to finish. 

  

This step creates 2 files: 

- code_index.csv 

- code_pmi.csv 

  

If you finished STEP 2 and STEP 3 before, you can directly do STEP 4 and 5 to load your trained model. 

  

STEP 4 (activate the code_explorer):  

------------------------------------  

The goal of this step is to set up a local-server on your computer that would enable browser to show code similarity results. The following are the instructions to install a local-sever on your computer. 

  

Although there are many ways you can install the server (e.g., R, XAMPP, WAMP), in the following we explain how to install the R.  

 

Download and install R for Windows from this link: https://cran.r-project.org/bin/windows/ 

After installing R, you will run R from the start menu of your computer.  

After running R, you will see a command console. Now, you will run the following line in your command console to add ‘servr’ package.  

install.packages(‘servr’) 

To run a server using R, write the following lines in your command console where the httd function will point to medicare_code_similarity folder in your computer. 

library(servr) 

httd("C:\\medicare_code_similarity") 

In this example, the medicare_code_similarity folder is in ‘C’ drive. After running the above lines, a browser window will open that will show medicare_code_similarity folder. Now, you will copy the files created in STEPS 1-3 into code_explorer folder. In particular, the “code_explorer” folder will contain the following files: 

- code_index.csv 

- code_pmi.csv 

- code_vectors_file.csv 

- index.html 

- css directory 

- js directory 

  

STEP 5 (explore the codes from a browser):  

------------------------------------  

In this step, you will click on the “code_explorer” folder in your opened browser. You will see an interface where you can give a medical code in the text field and press the "search code" button to see results. 

There are two options in the interface, (Cosine similarity and PMI value). You can select any one option to see results. 

 

You only need to do STEPS 1-4 once to prepare the model. Then, you can start using STEP 5 at any time to explore the relationships between the codes. 

------------------------------------  

Thanks! 

 
