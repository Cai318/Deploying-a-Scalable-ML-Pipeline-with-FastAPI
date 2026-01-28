# Model Card

For additional information see the Model Card paper: https://arxiv.org/pdf/1810.03993.pdf

## Model Details

This income prediction model is a Random Forest Classifier built with scikit-learn to predict whether an individual earns more or less than $50K annually. It uses 100 estimators, a fixed random state of 42, and no limit on tree depth, enabling it to capture complex patterns in the data. It was trained on the UCI Census Income Dataset (Adult Dataset), a subset from the 1994 Census that contains demographic and employment information. After preprocessing, which included one-hot encoding of categorical features and binarization of the target variable, the dataset was split into 80% for training and 20% for testing. The model incorporates 14 features, including eight categorical variables (workclass, education, marital status, and race) and six numerical variables (age, fnlgt, education level, capital gain/loss, and hours worked per week).

## Intended Use

The primary use case of this model is to predict income from demographic and employment characteristics. It is intended for researchers studying income inequality and demographic factors, policymakers analyzing socioeconomic patterns, and educational institutions conducting academic research. The model is not designed for high-stakes or commercial applications and should not be used for direct employment decisions, credit scoring, insurance underwriting, or any other commercial purposes without proper validation.

## Training Data

The training data set utilized for this model is titled "Census Income" and can be found at: https://archive.ics.uci.edu/dataset/20/census+income

This UCI Census Income Dataset is derived from the 1994 Census database and includes detailed demographic and employment information, with the target variable indicating whether an individual’s annual income exceeds $50K. This dataset was chosen because it includes several features that can be investigated and because the income requirements are already separated.

The data preprocessing steps include one-hot encoding for all categorical features, label binarization of the target, and handling missing values using a OneHotEncoder configured with handle_unknown="ignore". No scaling was applied to numerical features because the Random Forest algorithm is inherently scaleinvariant. The training dataset comprised 80% of the original dataset, totaling about 26,048 samples with 14 features each. It is structured as a binary classification task, with approximately 76% of individuals earning ≤$50K and about 24% earning >$50K.

## Evaluation Data

The evaluation process used a test set comprising 20% of the original dataset, totaling about 6,512 samples. Cross-validation was not included in this implementation but could be incorporated in future iterations to provide a more robust assessment of model performance.

## Metrics

The model’s primary evaluation metrics include **precision**, which measures the proportion of predicted positives that are correctly identified; **recall**, which measures the proportion of actual positives that are correctly identified; and the **F1-score**, the harmonic mean of precision and recall. The overall model performance shows a precision of **0.7419**, a recall of **0.6384**, and an F1-score of **0.6863**.

Performance varies across demographic slices; for example, for individuals with an education level of “Prof-school”, the model performs well, with a precision of 0.8182, a recall of 0.9643, and an F1-score of 0 8852. The model underperforms for individuals with an education level of “10th”, yielding a precision of 0.4000, a recall of 0.1667, and an F1-score of 0.2353.

Overall, the model demonstrates moderate effectiveness, offering relatively high precision with fewer false positives, though lower recall indicates it misses some higher-income individuals. The F1-score provides a balanced view of these trade-offs.

## Ethical Considerations

The model raises several important ethical considerations, including potential biases stemming from historical patterns in the 1994 Census data, as well as the risk that demographic features such as race, sex, and native country may introduce unfair bias and perpetuate existing socioeconomic inequalities. Its performance also varies across demographic groups, underscoring fairness concerns and reinforcing that the model should not be used for discriminatory purposes and should undergo regular fairness audits. In addition, the dataset includes sensitive demographic information, making responsible use of predictions and adherence to data protection regulations essential.

To address these concerns, recommended mitigation strategies include continuous monitoring of performance across demographic slices, implementing fairness constraints during training, maintaining transparent documentation of model limitations, and regularly retraining the model with updated, more representative data.

## Caveats and Recommendations

The model has several limitations, including reliance on 1994 data that may not reflect current economic conditions and a restriction to U.S. Census data, which limits generalizability to other countries. Its binary classification framework can oversimplify income distribution, and the model does not account for temporal dynamics. Given these limitations, the model should be used only for research and educational purposes, with results validated against more current data. 

Users should consider ensemble methods for improved performance, conduct feature importance analyses for interpretability, and regularly retrain the model with updated data. When deploying the model, it is important to monitor model drift, apply A/B testing for updates, implement automated retraining pipelines, and establish clear governance policies.

Future improvements could include incorporating more recent datasets, adding cross- validation to improve robustness, applying feature engineering techniques, exploring alternative algorithms such as XGBoost or neural networks, and integrating explainable AI methods to enhance interpretability.
