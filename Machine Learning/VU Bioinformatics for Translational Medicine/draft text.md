\section{Materials and Methods}

\subsection{Multivariate Feature Selection and Non‐linear Classification}

\subsubsection{Multivariate Feature Selection using SPLSDA}  
Sparse partial least squares discriminant analysis (SPLSDA) enforces supervised dimension reduction by limiting both the number of latent components (\textit{ncomp}) and the number of features per component (\textit{keepX}). We optimized \textit{ncomp} (1; 1–2; 1–3) and \textit{keepX} (1–200; step 1 to 10, then 10 to 200) via an iterative grid search with 10‑fold cross‑validation repeated 10 times, minimizing the balanced error rate. For each candidate \textit{ncomp}, the optimal \textit{keepX} for component 1 was used when tuning component 1+2, and so on. The combination yielding lowest mean error (3 components; keepX = 190, 5, 190) was selected :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}.  

Features were further filtered by stability (selected in > 25\% of 10 × 10 CV iterations) and by loading magnitude (above the median absolute loading per component). This final SPLSDA filter retained 185 copy‑number segments for downstream classification :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}.

\subsubsection{Classification using XGBoost}  
To capture potential non‐linear relationships between copy‑number features and breast cancer subtypes, we applied eXtreme Gradient Boosting (XGBoost) with the “softprob” objective for multi‐class classification. The input consisted of the SPLSDA‐filtered feature matrix.  

Hyperparameters—learning rate (0.1, 0.3), maximum depth (8–10), subsample (0.9, 1.0), colsample\_bytree (0.9, 1.0)—were optimized via a 5 × 10 nested cross‐validation. In each outer fold, SPLSDA filtering was recomputed (10 × 10 CV), then an inner 10‑fold grid search with early stopping (10 rounds without multi‑class error improvement) identified the optimal parameter set (learning rate = 0.3, max\_depth = 9, subsample = 0.9, colsample\_bytree = 1.0) :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}.  

The final model was trained on the full training dataset using these parameters, and both classifier and SPLSDA filter were serialized for reproducibility and subsequent SHAP analysis :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}.

\section{Results}

\subsection{SPLSDA Hyperparameter Tuning and Feature Selection}

\subsubsection{Optimizing Component Number and Sparsity}  
Iterative grid search showed that error rate decreased continuously up to three components, with optimal keepX values of 190, 5, and 190 (Figure 1). The demo figure’s diamond markers indicate an illustrative keepX of 80 (parenthetical), highlighting variability in optimal feature counts for components 2 and 3 across CV splits :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}.

\begin{figure}[h]
\centering
\includegraphics[width=0.8\textwidth]{fig2_splsda_tuning.png}
\caption{Iterative SPLSDA hyperparameter tuning. Classification error rate (y‑axis) versus number of selected features per component (x‑axis) for one‑, two‑, and three‑component models. Error bars denote 95\% confidence intervals; diamonds mark the chosen keepX values (190, 5, 190; demo diamond at 80 in parentheses).}
\end{figure}

\subsubsection{Projection and Variance Explained}  
Prior to feature filtering, the optimized three‐component model explained only 16\% of variance, with substantial overlap between HR⁺ and Triple Neg clusters (Figure 1B) :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}. After applying the SPLSDA filter, variance explained rose to ~45\% and classification error dropped below 20\%, although HR⁺ and Triple Neg remained less well separated (Figure 1C).

\begin{figure}[h]
\centering
\includegraphics[width=0.8\textwidth]{fig1_splsda_projection.png}
\caption{SPLSDA sample projections. (A) Preliminary model (10 components, all features); (B) optimized model (3 components, all features); (C) optimized + filtered features (3 components, 185 features). Ellipses represent 95\% confidence. Variance explained is indicated for each plot.}
\end{figure}

\subsubsection{Loadings Structure and Feature Stability}  
The correlation circle for components 1 vs 2 confirms that component 2 is dominated by a single segment (17\_35076296\_35282086), whereas component 1 comprises many small‐loading features within the 0.5 radius (Figure 3) :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13}. Stability analysis (10 × 10 CV) revealed that fewer than 25\% of features were consistently selected; applying a 0.25 frequency threshold and median loading cutoff yielded the final 185‑segment filter (Figure 4) :contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15}.

\begin{figure}[h]
\centering
\includegraphics[width=0.6\textwidth]{fig3_correlation_circle.png}
\caption{Correlation circle of SPLSDA loadings (components 1 vs 2). Outer circle radius = 1; inner circle = 0.5. The dominant feature vector outside the inner circle corresponds to segment 17\_35076296\_35282086.}
\end{figure}

\begin{figure}[h]
\centering
\includegraphics[width=\textwidth]{fig4_stability_loading.png}
\caption{Feature stability and loading distributions. (A–C) Selection frequency across 10 × 10 CV for components 1–3. (D–F) Horizontal barplots of absolute loadings, colored by subtype with highest mean copy‐number.}
\end{figure}

\subsection{XGBoost Classification Performance}

\subsubsection{Error Rates across Nested CV}  
The optimal XGBoost model (lr = 0.3, depth = 9, subsample = 0.9, colsample = 1.0) achieved a median error rate of 0.13 across 50 validation folds (Supplementary Figure 1) :contentReference[oaicite:16]{index=16}:contentReference[oaicite:17]{index=17}.

\begin{figure}[h]
\centering
\includegraphics[width=0.6\textwidth]{supp_fig1_error_hist.png}
\caption{Histogram of overall classification error rates across 50 validation folds. Dashed line marks the median (≈ 0.13).}
\end{figure}

\subsubsection{Confusion Matrix and AUC}  
Aggregated over outer folds, the model attained 100\% accuracy for HER2+, 85.8\% for HR+, and 75.3\% for Triple Neg (Table 1). One‑vs‑all AUCs were 1.00, 0.90, and 0.89, respectively (Supplementary Figure 2) :contentReference[oaicite:18]{index=18}.

\begin{table}[h]
\centering
\begin{tabular}{lccc}
\toprule
               & Predicted HER2⁺ & Predicted HR⁺ & Predicted Triple Neg \\
\midrule
True HER2⁺     & 100\%           & 0\%           & 0\%                  \\
True HR⁺       & 0\%             & 85.8\%        & 14.2\%               \\
True Triple Neg & 0\%             & 24.7\%        & 75.3\%               \\
\bottomrule
\end{tabular}
\caption{Average confusion matrix from 5 × 10 nested CV for XGBoost classification.}
\end{table}

\begin{figure}[h]
\centering
\includegraphics[width=0.8\textwidth]{supp_fig2_roc.png}
\caption{ROC curves for HER2⁺, HR⁺, and Triple Neg classification across nested CV folds. Light gray: individual folds; bold: mean ROC; diagonal: chance.}
\end{figure}

\subsection{SHAP Analysis of Feature Contributions}

\subsubsection{Global Importance Profiles}  
SHAP summary plots of the top 15 features per class show that segment 17\_35076296\_35282086 dominates HER2⁺ predictions, whereas HR⁺ and Triple Neg rely on a broader set of features with more distributed contributions (Figure 5A–C) :contentReference[oaicite:19]{index=19}:contentReference[oaicite:20]{index=20}.

\begin{figure}[h]
\centering
\includegraphics[width=\textwidth]{fig5_shap_summary.png}
\caption{Class‑specific SHAP summary plots of top 15 features. (A) HER2⁺; (B) HR⁺; (C) Triple Neg. Features ordered by mean absolute SHAP value.}
\end{figure}

\subsubsection{Dependence on Copy‑Number State}  
Dependence plots for 17\_35076296\_35282086 reveal that amplification (2) strongly increases SHAP values for HER2⁺, while its effect on HR⁺ and Triple Neg is weaker and more variable (Figure 6A–C) :contentReference[oaicite:21]{index=21}:contentReference[oaicite:22]{index=22}.

\begin{figure}[h]
\centering
\includegraphics[width=\textwidth]{fig6_shap_dependence.png}
\caption{SHAP dependence plots for segment 17\_35076296\_35282086. (A) HER2⁺; (B) HR⁺; (C) Triple Neg. X‑axis: raw copy‑number call (–1: loss; 0: normal; 1: gain; 2: amplification); Y‑axis: SHAP value.}
\end{figure}

\subsubsection{Individual Prediction Explanations}  
Force plots for one representative sample of each subtype illustrate how features collectively push model outputs away from the baseline expectation (Supplementary Figure 3), with 17\_35076296\_35282086 driving the HER2⁺ case and a multi‐feature interplay for HR⁺ and Triple Neg predictions :contentReference[oaicite:23]{index=23}:contentReference[oaicite:24]{index=24}.

\begin{figure}[h]
\centering
\includegraphics[width=\textwidth]{supp_fig3_force_plots.png}
\caption{SHAP force plots for three representative samples. (A–C) True HER2⁺; (D–F) True HR⁺; (G–I) True Triple Neg. Yellow arrows: positive contributions; magenta: negative.}
\end{figure}
