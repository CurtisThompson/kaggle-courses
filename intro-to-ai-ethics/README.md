# Introduction To AI Ethics

Below are my notes for the [Intro to AI Ethics](https://www.kaggle.com/learn/intro-to-ai-ethics) course, which I completed on the [19th of October 2023](https://www.kaggle.com/learn/certification/cwthompson/intro-to-ai-ethics).

## Human-Centered Design For AI

Human-centered design (HCD) involves designing systems that serve people's needs. There are several steps to consider:

1. Understand people's needs
2. Ask whether AI is the simplest way to solve those needs
3. Consider harms that AI could cause
4. Prototype with non-AI systems first
5. Provide ways for people to challenge the system
6. Build in safety measures

To mitigate harms you should try to include humans in the different processes of developing the AI. For example, humans can check the data quality before a new build or review AI decisions before they are implemented in the real world.

There are several different ways that people can challenge an AI system. Can certain features be turned off? Can people reach out to the development teams? Is there an explanation of how the AI reached a decision?

## Identifying Bias

Bias is a negative result of poor AI applications where one group is disproportionately affected.

There are several different types of bias:

|Bias|Explanation|
|---|---|
|Historical Bias|Past bias in the real world influencing the AI. For example, if historical hiring practices discriminated against women then a model trained to perform similar hiring practices could discriminate similarly.|
|Representation Bias|When groups are not represented in the training dataset. For example, using smartphone data to plan city transportation links will be bias against older people who are less likely to use a smartphone.|
|Measurement Bias|The accuracy of the data varies across groups due to proxy variables. For example, although race can be removed from a training set, there might be other variables which closely correlate with race, causing discrimination in the model.|
|Aggregation Bias|Bias due to inappropriately combined groups. For example, Hispanics have a higher rate of diabetes than non-Hispanic white people. Grouping them together for diagnosis will negatively affect one group.|
|Evaluation Bias|Benchmark data not reflecting the real world population. For example, facial recognition cannot only be benchmarked on white faces or else it may fail in the real world on darker skin.|
|Deployment Bias|The model is being used in a different way than intended.|Tools to predict reconviction rates may not be suitable for when handing out original criminal sentences.|

These biases are based on [A Framework for Understanding Sources of Harm throughout the Machine Learning Life Cycle (Suresh and Guttag, 2021)](https://arxiv.org/pdf/1901.10002.pdf).

Note that these biases are similar and can overlap. One problem could result in several biases.

The Kaggle exercise has a great example of biases in models. A model was trained to detect toxic (or abusive) messages online; it works by giving coefficients to each word and then passing those coefficients into a logistic regression model. Every message was given a label or either "Toxic" or "Not Toxic". These are some of the real results of the model:

|Message|Classification|
|---|---|
|I have a christian friend|Not Toxic|
|I have a muslim friend|Toxic|
|I have a white friend|Not Toxic|
|I have a black friend|Toxic|

All of those messages are not toxic. There is a clear bias against certain identities. This could be due to historical bias where the online community is more likely to be Islamophobic or racist towards black people.

## Fairness

There are lots of ways to define whether an AI is fair. Kaggle offers four fairness criteria:

1. **Demographic Parity**. The composition of the selected sample (by the model) represents the overall prediction population.
2. **Equal Opportunity**. The proportion of positives is equal across groups. This refers to the true positive rate (TPR).
3. **Equal Accuracy**. The percentage of correct classifications is equal across all groups.
4. **Group Unawareness**. Removing all group membership from the dataset such as gender, age, and race.

## Model Card

A model card is a short document that provides key information about a machine learning model. This is useful for transparency around the processes of the model.

Model cards were introduced in a paper called [Model Cards for Model Reporting (Mitchell et al, 2019)](https://arxiv.org/abs/1810.03993). Google Cloud has also provided an example for [Face Detection](https://modelcards.withgoogle.com/face-detection) and [Object Detection](https://modelcards.withgoogle.com/object-detection).

There are nine main sections to a model card but you can add or remove sections as required based on your domain and target audience:

1. **Model Details**. This includes version number and developers.
2. **Intended Use**. Use cases and target users.
3. **Factors**. What factors/features/variables impact the model.
4. **Metrics**. How is performance measured for the model?
5. **Evaluation Data**. What datasets were used for evaluation. Provide them if possible. Why were those dataset used?
6. **Training Data**. What data was the model trained on?
7. **Quantitative Analyses**. How did the model perform in evaluation? Break this down into all important factors.
8. **Ethical Considerations**. Is there sensitive data? Is there an impact to safety? How have risks been mitigated?
9. **Caveats and Recommendations**. Any information not already covered.

When using the model cards in business it is particularly important to think about the target audience. There may be some information that cannot be revealed outside of the business, and there may be some terms that are too technical for stakeholders.