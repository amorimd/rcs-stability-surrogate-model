# Surrogate model for the Muon collider RCS stability studies

This repository contains a notebook that explores the output of a simulation run of the transverse and longitudinal beam stability of a chain of Rapid Cycling Synchrotrons that make the acceleration chain of the Muon Collider study.
The resulting output are used as a train and validation set for a Multi Regressor model that uses Gradient Boosted trees from scikit learn or from xgboost package

## Purpose

The stability simulations using Xsuite and PyHEADTAIL enable to estimate the emittance (i.e the transverse and longitudinal size of the muon bunches) after acceleration in the RCS chain.
However many parameters are free and can influence the outcome, by mitigating or amplifying the instabilities: chromaticity, offset of the bunch, damper strength, wakefield strength.
Wide parameter scans on these variables can take days to complete, with thousands of jobs.

This surrogate model used gradient boosted trees to provide a regression model that estimates the output emittance for any parameter in the simulation range.
The model training is quick (few seconds), and the hyperparameter scan takes ~20 minutes using RandomizedSearchCrossValidation with 100 candidates.

Once the model is stored, predicting a value only takes milliseconds.

## Parameters (5)

The model parameters are the one that were scanned in simulations:
- chromaticity
- damper strength
- initial transverse offset in each RCS
- wakefield scaling
- numbers of turns for the wakefield


## Outputs (12)

The goal of the simulations and of the model is

- Horizontal emittance in RCS 1, RCS 2, RCS 3 and RCS 4
- Vertical emittance in RCS 1, RCS 2, RCS 3 and RCS 4
- Longitudinal emittance in RCS 1, RCS 2, RCS 3 and RCS 4
