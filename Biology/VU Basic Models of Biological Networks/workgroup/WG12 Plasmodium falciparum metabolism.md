# Plasmodium falciparum metabolism

## Glycolysis Fluxes

[Model](https://jjj.bio.vu.nl/models/penkler1/)
![](Media/Pasted%20image%2020250314155952.png)

### Flux relations

$\text{vPFvGLCtr}$: 0.265248
$\text{vPFvLACtr}$: 0.487602
$\text{vPFvGLYtr}$: 0.0214467
$\text{vPFvPYRtr}$: 0.0214467

Glycerol flux = pyruvate flux
2 times glucose flux - glycerol flux = GAP flux
pyruvate flux + lactate flux = GAP flux

![[Media/WG12 Plasmodium falciparum metabolism 2025-03-25 18.18.56.excalidraw]]
### 3 largest flux control coefficients for vPFLACtr

$$
C^{J_{\text{vPFvLACtr}}}_{v}
$$
- vPFvGLCtr: 0.294528
- vPFvHK: 0.331002
- vPFvPFK: 0.297087

### increase vPFvGLCtr by 1%

- vPFvGLCtr: 0.0469 -> 0.04737
- vPFvLACtr: 0.0487602 -> 0.489033
- $$\begin{aligned}
C&=\frac{\text{relative change in flux}}{\text{relative change in activity}}\\
&=\frac{ (0.489033-0.487602)/0.487602}{\text{1\%}}\\
&=0.293477
\end{aligned}$$
- There is a small difference with the matrix determined control coefficients. This is because the matrix method calculates control coefficient for an infinitesimally small change. When the change is larger (1%), the control coefficient is the slope for a longer range and become underestimated.

![[Media/WG12 Plasmodium falciparum metabolism 2025-03-25 18.12.40.excalidraw]]

## Plasmodium

[model](https://jjj.biochem.sun.ac.za/models/dutoit1)
### Steady state fluxes

vPFvLACtr: 0.549868
vRBCivLACTRANSPORT: 0.556635

### Control coefficients

|                    | J_vRBCivLACTRANSPORT |
| ------------------ | -------------------- |
| vRBCivGLCTRANSPORT | 0.000309877          |
| vRBCivHK           | -0.0000883929        |
| vRBCivPFK          | -0.0000206959        |
| vPFvGLCtr          | 0.291311             |
| vPFvHK             | 0.328006             |
| vPFvPFK            | 0.294453             |

|                    | J_vPFvLACtr |
| ------------------ | ----------- |
| vPFvGLCtr          | 0.294661    |
| vPFvHK             | 0.331779    |
| vPFvPFK            | 0.29784     |
| vRBCivGLCTRANSPORT | 0.000313442 |
| vRBCivHK           | -3.16224e-7 |
| vRBCivPFK          | -7.36005e-8 |
Different control coefficients in RBC vs. in PF. The different control coefficients allows target manipulation of lactate production in PF.





