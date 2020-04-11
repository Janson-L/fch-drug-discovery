# Covid-19 Drug Discovery using Genetic Algorithm and Deep Learning
## Forkwell Coronavirus Hack: Drug Discovery
This is an submission to the Forkwell Coronavirus Hack Competition hosted by Forkwell under category Drug Discovery. 

The goal of this category is to create a novel small molecule or find existing drug on market which able to stop of interfere with the coronavirus lifecyle. Therefore, one of the approaches to this is to find out drugs or ligands which able to bind with the coronavirus main protease [6LU7](https://www.rcsb.org/structure/6lu7). 

Several research and experiment had been conducted and recorded in [DrugBank](https://drugbank.s3-us-west-2.amazonaws.com/assets/blog/COVID-19_Web.pdf) paper which leads to our evaluation target.  

Below are the samples of existing drugs that had been experiment with the coronavirus binding: 

| Drugs/Ligands        | Binding Score           |
| ------------- |:-------------:|
|   Remdesivir    | -7.4 |
|   Umifenovir    | -6.1     |
|   Favipiravir | -5.6     |
|   Lopinavir | -6.6     |
|   Ritonavir | -6.2     |
|   Galidesivir | -5.6     |
|   Favipiravir | -5.6     |
|   Triazavirin | -5.9     |
|   Chloroquine | -5.6     |
|   Darunavir | -7.2     |
|   TMC-310911 | -8.9     |


# Acknowledgement
Our team would like to thanks all the mentors from forkwell corona-virus for giving us the chances in working on this project and contributing to the corona-virus outbreak. 

This work is continuous progress from the repository [Deep_Learning_Coronavirus_Cure](https://github.com/mattroconnor/deep_learning_coronavirus_cure) created by Matt O Connor which is also one of our mentors in this hackathon. 

Next, we would like to thanks jhjensen2 with his repository Graph-based genetic algorithm[GB-GA](https://github.com/jensengroup/GB-GA). The details of his work can be find under his paper entitled "A graph-based genetic algorithm and generative model/Monte Carlo tree search for the exploration of chemical space" [link](https://pubs.rsc.org/en/content/articlelanding/2019/SC/C8SC05372C#!divAbstract) 

# Team Details
Team Name: TaoFuFa
1) Quek Yao Jing [Skyquek-github](https://github.com/Skyquek)
2) (Janson) Liew Kok Foo [Janson-L-github](https://github.com/Janson-L)
3) Tang Li Ho [Skyquek-github](https://github.com/Skyquek) ------------------ Li Ho
4) Kwong Tung Nan [Skyquek-github](https://github.com/Skyquek) -------------Kwong

# Requirements
The requirements are identical to the original repository [Deep_Learning_Coronavirus_Cure](https://github.com/mattroconnor/deep_learning_coronavirus_cure)


# Changes to Original files
In this repository, we introduced a new concept which we name it as local Genetic Algorithm (local-GA), which is an optimization method in evolutionary computing. In our method, we plan to keep changes to a minimum as the repository by Matt is well-maintained and can act as a good starting point.  

Our local-GA utilizes the cross-over and mutation to search for the molecule based on the fitness function.

We implement local-GA in 2 parts, which are before the Transfer Learning and before we export the generated molecule to sdf file.

In our approaches, this is overview of our local GA:
- **Population: The number of original molecule**

The initial population depends on the molecule we compute before passing it to the local GA. There are 2 part that we called the local-GA which is before the transfer learning and before exporting the sdf files. So, the first population is the 70 molecule selected based on score, similarity, logP and also random generated. In second local-GA, number of validated molecule from 5000 molecule generated after transfer learning is used.

- **Mating Pool: The number we want to pass generation by generation**

We select the number of molecule we need from the population to the mating pool. The selection criteria is based on the fitness function. This number is also the number of molecule returned after every generation. 

- **Cross-Over: Explain how the chemical cross-over work...................TANG LI HO**

LI HO, update here. 


- **Mutation: Explain how the chemical mutation work.......................TANG LI HO**

LI HO, update here. 

- **Fitness Fucntion: The fitness function of the molecule is based on the logP value. From this [article](https://www.acdlabs.com/download/app/physchem/making_sense.pdf), the oral administration of drug should be lower than 5 and best in the range of 1.35 - 1.8.**

The fitness function is the evaluation criteria in every single generation. 

LogP is used in the pharmaceutical/biotech industries to understand the behavior of drug molecules in the body. Drug candidates are often screened according to logP, among other criteria, to help guide drug selection and analog optimization. This is because lipophilicity is a major determining factor in a compound’s absorption, distribution in the body, penetration across vital membranes and biological barriers, metabolism and excretion (ADME properties). According to ‘Lipinski’s Rule of 5’ (developed at Pfizer) the logP of a compound intended for oral administration should be <5. A more lipophilic compound:

• Will have low aqueous solubility, compromising bioavailability. If an adequate concentration of a drug cannot be reached or maintained, even the most potent in-vitro substance cannot be an effective drug.

• May be sequestered by fatty tissue and therefore difficult to excrete; in turn leading to accumulation that will impact the systemic toxicity of the substance.

• May not be ideal for penetration through certain barriers. A drug targeting the central nervous system (CNS) should ideally have a logP value around 2;2 for oral and intestinal absorption the idea value is 1.35–1.8, while a drug intended for sub-lingual absorption should have a logP value >5.


Not only does logP help predict the likely transport of a compound around the body. It also affects formulation, dosing, drug clearance, and toxicity. Though it is not the only determining factor in these issues, it plays a critical role in helping scientists limit the liabilities of new drug candidates.

# Approaches
## Original Approaches: 

Global-Generation 0:

1) LSTM-CHEM to train ChEMBL Database
2) From LSTM CHEM, we predict 10k of data
3) Check the validation
4) Compute Tanimoto similarity, select 1000 only
5) Give ID to the 1000 smile, add the HIV, and other drugs SMILE manually…. 
6) Save all in master table and manually check from PyRX to get the affinity

While each Global-Generation < n, 

7) From the master table (load from Global-Generation before this), 
- 35 based on score
- 5 based on the similarity
- 5 based on the weight
- 5 based on the random mutation
  
1) From 55, we do Transfer Learning. We then  generate 5k of data and then perform validation and similarity and generate master table. 

## Modified Approaches:
Global-Generation 0:
1) LSTM-CHEM to train ChEMBL Database
2) From LSTM CHEM, we predict 10k of data
3) Check the validation
4) Compute Tanimoto similarity, select 1000 only
5) Give ID to the 1000 smile, add the HIV, and others drugs SMILE manually…. 
6) Save all in master table and manually check from PyRX to get the affinity

While each Global-Generation < n, 

7) From the master table (load from Global-Generation before this), 
- Select the 35 based on score
- 10 based on the similarity
- 10 based on logP
- 10 based on weights
- 5 based on the random generation

    7.1) From the number of molecule we select at 7, we pass to Local GA to obtain 10 molecule which contains logP 1.35 - 1.8

    7.2) Combined all the molecule from 7 and 7.1 and pass to 8
8) By using 90 molecule, we perform Transfer Learning and generate 5k of data.
9) From the 5k of data, we do validation to make sure it is  valid molecule. 
10) After that, we generate another 50 molecule using local-GA which has logP 1.35-1.8. 
11) Validate the 50 molecule generated using local-GA and combined with molecule from 9.
12) Export to sdf and evaluate with PyRX. Note

There are few ideas we think of improving: 
1) Change the LSTM network to Generative Adversarial Network (GAN), but after discussion we found out that its is not necessary as LSTM is good enough for this project. GAN is computing expensive and requires much more training time. 

2) From the evaluation, we plan to use neural network to perform prediction, but after we think twice we found out that the neural network is just the estimation of the affirnity which is dangerous as its contains errors in the prediction. 

# Challenge
The first challenge we faced is computation power limitation. VINA is a tool that utilizes CPU only without the option to utilize GPU for accelerating the docking process. 1500 ligands require roughly 18 hours to calculate binding affinity to every ligands with exhaustiveness of 8. This operation is performed on a Windows machine with Core i7-6700K. This severely limits the things we can do to our algorithm design as we need to reserve a lot of time to calculating the binding affinity of each ligand with the main protease of coronavirus.  ...JANSON & KWONG

# Future work
Evaluation: 
1) Cloud Computing: ...................KWONG
2) .....JANSON or KWONG (add what method which can speed up the progress)

# Reference
1) https://drugbank.s3-us-west-2.amazonaws.com/assets/blog/COVID-19_Web.pdf
2) https://www.acdlabs.com/download/app/physchem/making_sense.pdf
3) https://github.com/mattroconnor/deep_learning_coronavirus_cure
4) https://github.com/isayev/ReLeaSE
5) https://github.com/sirimullalab/dlscore
6) https://gitlab.com/cheminfIBB/pafnucy
7) https://github.com/jensengroup/GB-GA
8) https://github.com/jensengroup/GB-GM
9) https://chemrxiv.org/articles/Graph-based_Genetic_Algorithm_and_Generative_Model_Monte_Carlo_Tree_Search_for_the_Exploration_of_Chemical_Space/7240751
10) https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6198856/
11) https://arxiv.org/abs/1703.10603


