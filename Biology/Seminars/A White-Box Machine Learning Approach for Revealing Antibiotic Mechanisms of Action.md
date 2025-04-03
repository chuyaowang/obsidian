# A White-Box Machine Learning Approach for Revealing Antibiotic Mechanisms of Action

[Paper link](https://www.cell.com/cell/fulltext/S0092-8674(19)30402-7)
[Beyond the black box with biologically informed neural networks](Biology/Seminars/Beyond%20the%20black%20box%20with%20biologically%20informed%20neural%20networks.md)
#paper 

## Summary

- An integrated biochemical screening, network modeling, and ML approach for revealing _causal mechanisms_
- Apply this approach to understanding mechanisms underlying _antibiotic efficacy_
- Added metabolites to E. Coli. environment with antibiotics and tested how did efficacy of antibiotics change
- [Genome Scaled Metabolic Model](LCMS/Genome%20Scaled%20Metabolic%20Model.md) of E. Coli., which simulates metabolic [fluxes](Biology/VU%20Introduction%20to%20Systems%20Biology/4.%20VU%20ISB%20Stoichiometric%20Models%20of%20Metabolism.md#^5518bd) and reactions based on defined inputs, such as metabolite perturbations. 
- Parsimonious flux balance analysis: predict flux under certain constraints. Makes an assumption that cells optimize for an objective function (minimize energy or resource expense while maximizing growth)
- Elastic Net used to do regression of IC50 (drug efficacy) from flux predictions. The regression coefficients are used to select important pathways. -> traditional ML approach, not DL

## Methods

### Experimental biochemical screening

- Added metabolites to E. Coli. environment with antibiotics, recorded antibiotic efficacy in terms of IC50 values (half-maximal inhibitory concentrations)

### Network modeling

- Used genome scaled metabolic model to predict _flux_ under each screening condition (metabolite-antibiotic combination)

In this paper, **Parsimonious Flux Balance Analysis (pFBA)** is used as a key computational tool to simulate metabolic states of *E. coli* under various conditions. Specifically, the authors use pFBA to predict how the supplementation of different metabolites impacts metabolic fluxes in the bacterial genome-scale metabolic model, iJO1366. Here's a detailed breakdown of its role and application:

> [!note]- parsimonious FBA
> ### **What is pFBA?**
> Parsimonious Flux Balance Analysis is an extension of standard Flux Balance Analysis (FBA). FBA is a mathematical approach used to predict the flow of metabolites (fluxes) through metabolic networks under steady-state conditions, optimizing for a particular objective (e.g., growth rate).
> 
> pFBA goes a step further:
> - In addition to optimizing the objective (e.g., biomass production), pFBA minimizes the total flux activity in the network. This reflects the biological principle of **parsimony**, where cells are hypothesized to use the minimal amount of resources necessary to achieve their goals, such as growth.
> 
> ---
> 
> ### **How Is pFBA Used in the Paper?**
> 1. **Simulating Metabolic States**:
>    - The authors simulate the metabolic fluxes for each metabolite-antibiotic condition by applying pFBA to the iJO1366 model of *E. coli*.
>    - Inputs to the model include boundary conditions defined by the availability of specific metabolites (from experimental screens) and the standard growth medium (MOPS-defined minimal medium).
> 
> 1. **Modeling Antibiotic-Driven Metabolism**:
>    - For each antibiotic (ampicillin, ciprofloxacin, gentamicin), the model predicts changes in flux through metabolic pathways when different metabolites are supplemented.
>    - pFBA produces flux distributions for thousands of reactions in the network, creating a comprehensive picture of how cellular metabolism adapts under stress.
> 
> 1. **Providing Training Data for Machine Learning**:
>    - The simulated metabolic fluxes are used as **input data** for the multitask elastic net regression model. These flux data, combined with experimental IC50 measurements (outputs), allow the biologically informed neural network to learn which metabolic reactions influence antibiotic efficacy.
> 
> 1. **Generating Testable Hypotheses**:
>    - By using pFBA, the authors identify metabolic pathways that are highly active in specific conditions. For example:
>      - They predict that purine biosynthesis is upregulated in response to certain antibiotics.
>      - These predictions guide further experimental validations, such as genetic deletions and metabolite supplementation studies.
> 
> ---
> 
> ### **Why Is pFBA Critical to the Study?**
> - **Biological Relevance**: It ensures that the flux predictions align with realistic biological behavior, such as resource efficiency during growth.
> - **Mechanistic Insights**: The pFBA results form the mechanistic backbone of the "white-box" neural network, ensuring that the predictions are tied to meaningful biochemical processes.
> - **Hypothesis Generation**: By minimizing flux activity, pFBA pinpoints key pathways that are energetically costly or critical under antibiotic stress, enabling focused experimental validation.
> 
> In summary, pFBA is used in this paper to simulate metabolic fluxes that reflect real biological constraints, integrate experimental data into network modeling, and provide actionable insights into how antibiotics perturb bacterial metabolism. Let me know if you'd like me to expand further!

### Biologically informed machine learning

- Flux as input, IC50 values as output
- Elastic net architecture
- Using flux as input applies biological constraints
- Identifies metabolic pathways (e.g., glycolysis, purine biosynthesis) whose activity correlated with changes in antibiotic efficacy.

> [!note]- Elastic net and feature selection
> ### What is an Elastic Net?
> The **elastic net** is a regularized regression method that combines the penalties of two other techniques:
> 1. [L1 Regularization](Machine%20Learning/Concepts/L1%20Regularization.md): Encourages sparsity by shrinking some coefficients to zero, effectively selecting a subset of features.
> 2. [L2 Regularization](Machine%20Learning/Concepts/L2%20Regularization.md): Shrinks coefficients uniformly, reducing the impact of multicollinearity (correlated features).
> 
> The elastic net balances these two penalties using a parameter called **l1_ratio**, which determines the mix of L1 and L2 regularization. This makes it particularly useful when:
> - There are many correlated features.
> - You want to select important features while still accounting for all variables.
> 
> ---
> 
> ### How Does the Model Identify Pathways Correlated with Antibiotic Efficacy?
> In this study, the authors used a **multitask elastic net regression** to identify metabolic pathways whose activity correlates with changes in antibiotic efficacy. Here's how it works:
> 
> 1. **Input Data**:
>    - The input features were **simulated metabolic fluxes** for each reaction in the *E. coli* genome-scale metabolic model (iJO1366). These fluxes represent the activity of metabolic reactions under different metabolite and antibiotic conditions.
>    - The output data were the experimentally measured changes in antibiotic IC50 values (a measure of drug efficacy).
> 
> 1. **Regularization with Elastic Net**:
>    - The elastic net regression was applied to predict IC50 values from the metabolic flux data.
>    - The L1 penalty (lasso) helped select a sparse set of metabolic reactions that were most predictive of antibiotic efficacy.
>    - The L2 penalty (ridge) ensured that correlated reactions were not arbitrarily excluded, preserving biologically meaningful relationships.
> 
> 1. **Pathway Identification**:
>    - After fitting the model, the authors analyzed the regression coefficients assigned to each metabolic reaction. Reactions with large coefficients were considered important for predicting antibiotic efficacy.
>    - These reactions were grouped into pathways using curated metabolic pathway annotations (e.g., from EcoCyc). Pathways enriched with high-coefficient reactions were identified as key contributors to antibiotic efficacy.
> 
> 1. **Validation**:
>    - The identified pathways were validated experimentally. For example, the model predicted that purine biosynthesis plays a critical role in antibiotic lethality, which was confirmed through genetic and biochemical experiments.
> 
> ---
> 
> ### Key Insights
> - The elastic net allowed the model to focus on a small, interpretable set of metabolic reactions while accounting for the complex, interconnected nature of metabolic networks.
> - By linking predictive features (metabolic fluxes) to known pathways, the authors could uncover **causal mechanisms** underlying antibiotic efficacy, such as the role of purine biosynthesis in increasing ATP demand and central carbon metabolism activity.
> 
> Let me know if you'd like further clarification or details!

### Validation

- The authors validated their predictions using genetic and biochemical experiments, such as deleting genes in purine biosynthesis and measuring the effect on antibiotic lethality.

## Results

### Known and new mechanisms identified

- The model correctly identified **central carbon metabolism pathways** (e.g., the TCA cycle) as contributing to antibiotic lethality, consistent with previous studies.
- Importantly, it uncovered a new role for **purine biosynthesis** in antibiotic action, showing that antibiotic-induced adenine limitation increases ATP demand, elevates central carbon metabolism, and enhances lethality.

### Experimental Validation

- Deleting genes involved in purine biosynthesis reduced the lethality of ampicillin and ciprofloxacin but increased the lethality of gentamicin. This validated the model’s prediction that purine biosynthesis mediates antibiotic efficacy in a pathway-specific manner.

### White-Box Model Performance:

- The biologically informed approach achieved high accuracy in predicting IC50 values while providing interpretable insights into the underlying pathways.

## Implications

1. **Biological Interpretability**:
    
    - By embedding biological network models into the machine learning workflow, the authors demonstrate that it is possible to predict drug efficacy **and** uncover causal mechanisms, bridging the gap between computational models and experimental biology.
        
2. **Antibiotic Mechanisms**:
    
    - The study highlights the critical role of **metabolism** in antibiotic action, particularly how pathways like purine biosynthesis and central carbon metabolism mediate drug efficacy. These findings could inform the development of adjuvants to enhance antibiotic performance.
        
3. **Machine Learning in Biology**:
    
    - The "white-box" approach provides a generalizable framework for integrating network models with machine learning. This methodology could be applied to other biological systems to uncover mechanisms behind complex phenotypes, such as cancer drug resistance or metabolic disorders.
        
4. **Therapeutic Potential**:
    
    - The identification of metabolic pathways as mediators of antibiotic efficacy opens avenues for new treatment strategies, such as targeting purine metabolism or using metabolic adjuvants.