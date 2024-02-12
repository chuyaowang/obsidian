# INCA Analysis Steps

> Summary of the [official help document](file:///Users/wangchuyao/Documents/seminars/mfa/model/INCAhelp.pdf)
> Also [reference](file:///Users/wangchuyao/Documents/seminars/mfa/model/A%20guide%20to%2013C%20metabolic%20flux%20analysis%20for%20the%20cancer%20biologist.pdf)

## 1. Enter experiments

- Take care to not write arrows and compound names wrong.
- Must use \* sign after stoichiometric coefficients/
- The order of the atom transition letters is important.

## 2. Edit reactions

- Edit entered reactions here, not the first page.
- Pathway information can be entered here.
- Bidirectional reactions: `<->`
- One-way reactions: `->`
- Known net and exchange flux of each reaction can be entered.

> [!note] Net and Exchange Flux
> - The net flux is defined as the difference between the forward flux and the backward flux of a reversible reaction, or simply as the forward flux of an irreversible reaction. 
> - The exchange flux is the minimum of the forward and backward fluxes of a reversible reaction, or is zero for an irreversible reaction.
> - i.e. for a reaction with forward flux $v_F$ and reverse flux $v_B$, the net and exchange fluxes are defined as: $$\begin{array}{c}v_{net}=v_F-v_B\\v_{exch}=\min(v_F,v_B)\end{array}$$

- Checking the select box will open the forward and reverse flux of each reaction in the lower left panel to edit.
- Fluxes can be fixed if it is a reference flux or a specific initial flux distribution is desired.
- If a reaction is deactivated here, the corresponding MS data must also be deactivated.

## 3. Edit network nodes

- There are 3 types of metabolites: source, sink, and internal.
- O2, CO2, ATP, NADP, NADPH should not be in **mass balance** since they can either enter or exit the system freely or be used by other reactions not in the system.
- Source and sink should not be in **mass balance**.
- It is assumed compounds not in mass balance are not labelled, but this can be changed in `blank`(TODO).
- Labeled source nodes are not included in **isotopomer balance**, but labeled sink nodes are.
- Unbalanced internal nodes are also assumed to be unlabeled unless specified in blank; this is tantamount to giving an infinite pool size to the node, since its labeling is independent from the rest of the network.
- Did not read INST-MFA stuff.

## 4. Edit metabolite properties

- Clicking each metabolite opens it in the *Edit atom properties* panel; ID denotes each atom; Element should include all the atoms that can be potentially labeled.
- Rotationally symmetric compounds need to be labeled accordingly in the *Edit symmetric atoms* panel. Basically if going on the backbone from left or right makes no difference, the compound is rotationally symmetric.
- Biochemically indistinguishable atoms need to be labeled in the *Edit equivalent atoms* panel; but typically not required for carbon.
- Although uncommon, more than one symmetry operation or equivalent groups can be entered for one compound.
- Rotationally symmetric compounds found:
  1. Citrate (maybe not)
  2. Fumarate
  3. Glycerol (maybe not)
  4. Succinate
- Citrate has an odd symmetry mapping: 123456 should map to 543216

## 5. Enter experimental dataset

- Three sets of data need to be entered:
  1. Flux measurements
  2. Isotope labeling measurements
  3. Isotope tracers
- Pool size can be added for INST-MFA.

### 5.1. Add new experiment

- Add a new experiment dataset by clicking new in the *Edit experiments* panel
- Why need multiple: replicate experiments or parallel labeling experiments with multiple tracers.
- When multiple experiments are checked, INCA will find a **flux map** that best fits all of them.
  
### 5.2. Enter flux or pool size measurements

- Enter growth rate, substrate uptake, and product formation data here.
- The standard error cannot be zero!
- The example provided standard deviation, but standard error = sd/sqrt of sample size.

### 5.3. Enter MS measurements

- Data needs to be entered manually.
- Click new to add a new isotopomer measurement entry.
- Use the drop down menu to add data for M0, M1, M2...
- Multiple samples can be entered.
- Enter MS abundance scaled to 1 for each metabolite.
- Need to correct for [natural isotope abundance](Natural%20Abundance%20Correction.md) by yourself or have INCA do it in the options.
- Also need standard error here, not standard deviation.
- Do it for each experiment.

### 5.4. Enter tracer data

- [Tracer](tracers) is the isotope of which you know the exact purity.
- Click new to generate a new tracer entry for the selected experiment. Tracer node should be the source node, and tracer abundance should not be entered in MS data part.
- Fractional abundance refers to how many one type of atoms out of the total number of that type of atoms are labeled in the tracer. For example, a U13C labeled glucose has a fractional abundance of 1.
- Then use the drop down menu to edit information for this tracer; Isotopic purity for each atom can be entered here.

## Constraint-based Analysis

- Does not need experimental data; analyzes network based on the stoichiometric matrix.
- Solve the S · v = 0 system of equations as a constraint optimization problem.
- Useful for identifying blocked pathways (net flux becomes 0 by **mass balance** constraints) or locations where material can enter/leave the network via unbalanced nodes.