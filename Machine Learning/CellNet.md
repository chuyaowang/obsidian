# Network Biology Applied to Stem Cell Engineering

## Overview

CellNet is a method to use GRNs to assess the fidelity of cell engineering approaches, or in human words, compare engineered cells to their counterparts in vivo.

The authors compared [directed differentiation](Cell%20Engineering.md##Directed%20differentiation) and [direct conversion](Cell%20Engineering.md##Direct%20conversion) cell populations. They found that directed differentiation led to cells that more closely resemble the target cells. However, both approaches created unwanted GRN connections.

## Introduction

Cell state conversions between various cell types have been achieved by forced expression of [transcription factors](Transcription%20Factor.md), but there lacks a quantitative method to assess their fidelity. The current approach that uses DNA and RNA expression profiles to do clustering analysis cannot provide insights on how to improve the outcome.

The authors developed the CellNet platform to compare engineered mouse and human cells to their counterparts. They found that reprogramming to pluripotency achieved the highest GRN similarity, while in neurons and cardiomyocytes, directed differentiation performed better than direct conversion.

Furthermore, in situ growth provided selective and inductive signals that more completely establish heart GRNs. Also, unintended GRNs are present in all cell engineering protocols.