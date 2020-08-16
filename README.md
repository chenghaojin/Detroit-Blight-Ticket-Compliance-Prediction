# Detroit Blight Tickets Compliance Classification

## Dataset

The data consists of information regarding over 250,000 blight tickets issued by the city of Detroit over the last couple of decades. Blight tickets are issued to property owners when their properties are not maintained according to Detroit’s property maintenance code. Each year, the city issues millions of dollars in fines but many remained unpaid. The enforcing of unpaid tickets is a costly process so being able to predict the outcome of a ticket and understand the factors behind non-compliance become important. 

The data can be assessed through [Detroit Open Data Portal](https://data.detroitmi.gov/).

## Feature Selection & Engineering

During feature selection phase, columns containing information that would not be available when making predictions were first dropped. These include payment dates, collection status, etc. Longitudes and latitudes of violation locations were cut into 1.5km by 1.5km blocks to better represent geographical data in a ML algorithm. A new feature ``time_diff`` was created by calculating the number of days between issuing and hearing dates. The ``violator_name`` column contains over 1000 unique names but many of them are different spellings of the same entity (such as Investment co, acorn and INVESTMENT, ACORN, etc.). Versions of names for the top 4 violators were replace with common names. Among numeric features, ``admin_fee``, ``state_fee`` and ``clean_up_cost`` have 0 variances so there were dropped from the model.

## Model Fitting, Tuning & Performance Evaluation

An XGBoost model was tuned using randomized search over possible values of parameters. The final model had a 0.87 AUC score on training set. After fitting the model on the hold-out validation set, an AUC of 0.82 was achieved. The most important feature in terms of contribution to the accuracy of the model is <i> responsible by default (disposition) </i>. Two numerical features, <i>discount amount</i> and <i>late fee</i> also contribute significantly. In fact, 4 out of the top 6 features are levels of ``disposition``. 

