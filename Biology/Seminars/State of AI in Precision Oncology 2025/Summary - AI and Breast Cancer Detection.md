# Fireside Chat: AI and Breast Cancer Detection

**Summit:** State of AI in Precision Oncology 2025

**Speakers:**
- **Doug Flora, MD** — Executive Medical Director, Yung Family Cancer Center, St. Elizabeth Healthcare; Editor-in-Chief, *AI in Precision Oncology*
- **Constance (Connie) Lehman, MD, PhD** — Professor of Radiology, Massachusetts General Hospital / Harvard Medical School; Founder, Clarity; Editor, *AI in Precision Oncology*

---

> **Relevant Link:** [Open Evidence AI](https://www.openevidence.com/) — a clinical AI tool widely used by physicians, referenced in this talk and throughout the summit as an example of rapid grassroots clinician adoption of AI tools.

---

## Overview

Dr. Connie Lehman discusses the evolution of AI in breast imaging, from the earliest rule-based computer-aided detection (CAD) tools of the 1990s to today's deep learning models capable of predicting a woman's future risk of breast cancer from a mammogram years before a cancer is detectable. She describes her founding of Clarity — which received the first FDA de novo authorization for an AI platform to predict future breast cancer risk directly from mammography — and lays out a vision for how mammography will shift from age-based mass screening to precision, risk-based screening and ultimately to cancer interception and prevention. The conversation with Flora is marked by both speakers' conviction that the tools now exist to make this transition, and that the medical community needs to accelerate its willingness to use them.

---

## A Historical Arc: Seeing What the Human Eye Cannot

Lehman traces breast cancer detection through three broad eras:

**The tactile era**: for most of recorded history, breast cancer was found by touch — often too late.

**The grayscale era**: mammography (from film-screen to digital to 3D tomosynthesis) moved detection into imaging, but the emphasis was on improving image quality and training radiologists to see subtle changes.

**The deep learning era**: AI reveals signals in digital mammogram images that are entirely invisible to the human eye — patterns in the breast tissue that predict future cancer risk with a precision no radiologist, no matter how skilled, can match.

The insight that opened this third era came from a collaboration with Regina Barzilay's lab at MIT. When Barzilay's graduate students were given large sets of de-identified mammograms (before outcome data was available), they discovered that computer vision could extract demographic information — a woman's age, race, parity, menopausal status — directly from the mammogram image. This meant the mammogram contained far more information than the visual features radiologists were trained to read. The logical next step was to train models to predict cancer outcomes from those latent features.

---

## Why Age-Based Screening Is Insufficient

One of the most pointed themes of the conversation is Lehman's critique of current age-based screening guidelines, which she calls "crude." Her evidence:

- Approximately 75% of women diagnosed with breast cancer have no family history.
- Traditional clinical risk models (Gail model, Tyrer-Cuzick) rely heavily on family history and reproductive history — variables that, it turns out, are largely capturable from the mammogram image itself by AI, making these models largely redundant once AI risk scores are available.
- Studies show these traditional clinical risk scores add essentially no predictive value on top of AI image-based risk scores.
- The debate over whether to screen at 40, 45, or 50 — which has dominated breast imaging conferences for years — is, Lehman argues, the wrong question. There are women in their 30s who are at high risk and need screening; there are women in their 70s who are at low risk and may not need it.

The density legislation — federal law requiring that women be told whether they have dense breast tissue — illustrates both the promise and the limitation of this paradigm. Dense breast tissue is associated with both a higher cancer risk and a higher rate of missed cancers on mammography, so informing women is well-intentioned. But 50% of women have dense breast tissue, and not all of them are at increased risk, nor do they all need supplemental MRI. The AI risk score, Lehman argues, does what the density legislation intended to do but couldn't: provide a precise, individualized risk estimate that actually tells the right women which additional imaging they need.

---

## Deep Learning: The Paradigm Shift

Lehman draws a careful distinction between two generations of AI in breast imaging:

**Rule-based CAD (1998 onward):** The first FDA-cleared CAD tools were engineered by radiologists who told computers what suspicious calcifications and distortions looked like. Performance was disappointing — large studies, including Lehman's own work with the Breast Cancer Surveillance Consortium, found that radiologists reading with early CAD were not more accurate than without it.

**Deep learning (current):** Rather than encoding human-defined rules, deep learning models are trained on the outcome: mammogram with cancer in five years vs. mammogram without cancer in five years. The model learns on its own what patterns in the pixel data — patterns humans have never conceived of and cannot see — predict future risk. This is the same paradigm shift that produced AlphaFold (the 2024 Nobel Prize for Demis Hassabis, John Jumper, and David Baker), which learned protein structure prediction rules from data rather than from human biochemical reasoning.

Clarity's model was trained on **over 400,000 mammograms** from women around the world. The use of a globally diverse training dataset was a deliberate choice to address the equity problem Lehman identifies with prior AI tools — many of which were trained predominantly on datasets of European women.

---

## Clarity and the FDA De Novo Authorization

Clarity was founded reluctantly — Lehman describes being pushed into entrepreneurship by Peter Slavin, then president of Mass General, who argued that commercial translation was the only way to achieve real-world impact at scale. She connected with a healthcare-focused venture capital group, trained the model, and pursued FDA authorization.

The resulting **FDA de novo authorization** is the first for an AI platform that predicts future breast cancer risk from mammography. This distinguishes it from the existing generation of AI tools in breast imaging, which primarily help detect cancer that is already present (current cancer detection). Clarity's tool operates in the **risk prediction** domain: it identifies women at elevated risk of developing cancer in the next five years, enabling more targeted screening interventions before the cancer appears.

This is the distinction Flora summarizes as: current AI tools augment radiologists in finding existing cancers; Clarity's tool finds women who will develop cancer and don't yet know it.

---

## Dynamic Risk Scores: The Next Frontier

In preliminary studies to be presented at a major radiology meeting, Lehman's group has shown that their AI risk scores are **dynamic**, not static. When they look back at historical mammograms from women who later developed breast cancer, the risk score shows a distinctive rising slope starting approximately five years before diagnosis — a trajectory entirely different from the flat score trajectory of women who remained cancer-free.

This dynamic risk tracking opens several clinical possibilities:
- Monitoring risk score trajectories over time to detect worrying changes before cancer is present
- Demonstrating objective, dose-dependent risk reduction in response to interventions (tamoxifen, weight loss, dietary changes) by watching scores fall
- Helping patients and providers make more informed decisions about chemoprevention, risk-reducing surgery, or enrollment in prevention trials

Lehman envisions this as the bridge to true cancer *prevention* rather than merely early detection. If a woman's risk score is rising, the clinical response should be to intervene — not just to screen more often. She sees radiologists moving from diagnosticians (detecting and staging disease) into a new role as risk predictors and prevention partners.

---

## The Future Radiologist's Role

Lehman addresses the fear, widespread a few years ago, that AI would eliminate the need for radiologists. She argues the opposite has happened: radiologists are already in short supply as cancer incidence rises and cancer survivors require ongoing surveillance imaging. AI is making them more productive, not obsolete.

More importantly, AI is giving radiologists **something they could never do before**: risk prediction from images. This expands the value of the specialty rather than contracting it.

Looking ahead, she sees a realistic near-term future in which:
- A subset of clearly negative screening mammograms (those with no marks from any detection AI and a very low risk score) is processed autonomously without requiring a radiologist read — similar to how automated CBC counts removed the need for hematologists to count red blood cells under a microscope.
- Radiologists focus their attention on flagged, higher-complexity, or high-risk exams.
- Risk scores from mammography are integrated with blood-based biomarkers (ctDNA, DNA methylation, fragmentomics) in a multi-modal risk assessment platform.

---

## Equity in Breast Cancer Screening

Lehman returns repeatedly to the equity dimension. Traditional clinical risk models were built on predominantly White, European datasets, systematically underestimating risk in Black, Hispanic, and other non-European populations. Clarity's global training set is a deliberate corrective. She also highlights that younger women — especially women under 40 — are the fastest-growing group being diagnosed with breast cancer at late stage, precisely because the current age-based guidelines tell clinicians not to worry about them. AI risk scores can identify the subset of women under 40 who genuinely need screening, without requiring universal screening of all 30-year-olds.

---

## Convergence with Broader Summit Themes

Lehman endorses the vision Flora has developed throughout the day's conversations: the shift from screening to risk management. She agrees with Betsy O'Donnell (morning session) that combining imaging-based risk scores with blood-based MCED tests — ctDNA, DNA methylation, immunophenotyping — is where the field is heading. The mammogram captures a record of how a woman's lifetime exposures (diet, exercise, BMI, inflammatory processes, hormonal history) have shaped her breast tissue. This biological record is now readable by AI in ways it never was before, and it can be combined with genomic and liquid biopsy data to create a comprehensive, dynamic risk portrait.

---

## Key Takeaways

**The mammogram contains far more information than human vision can access.** Deep learning unlocks this hidden signal, predicting future cancer risk with a precision no radiologist-based analysis can match.

**Age-based screening is an outdated proxy for risk.** AI risk scoring makes individualized, risk-based screening technically feasible right now. The barriers are adoption, guidelines, and reimbursement — not science.

**The FDA de novo authorization for Clarity's risk prediction tool is a milestone.** It is the first regulatory recognition of AI that predicts future breast cancer rather than detecting current cancer.

**Dynamic risk scores open the door to prevention.** Watching risk scores change over time in response to interventions transforms mammography from a detection tool into a prevention monitoring tool — potentially enabling clinicians to demonstrate, quantitatively, that an intervention is working.

**The role of the radiologist is expanding, not shrinking.** AI is adding capabilities (risk prediction, autonomous interpretation of clearly normal studies) that make the specialty more powerful and more important to the full cancer prevention ecosystem.
