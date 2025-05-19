Open-Schema NER with Segmentation Strategies
This repository contains the code and experiments for evaluating an open-schema Named Entity Recognition (NER) model under different segmentation strategies in a domain-specific, low-resource setting.

We focus on evaluating and fine-tuning an open-schema NER model on French-language articles related to a specialized domain. The study assesses the effect of different segmentation strategies on model performance, particularly for long and heterogeneous documents.

🧪 Segmentation Strategies
The notebook Segmentation_strategies.ipynb provided in this repository evaluate the following segmentation strategies:

1. Thematic Segmentation + Passage Retrieval

The document is first split into coherent thematic segments using a dynamic segmentation algorithm.

Then, a semantic search engine retrieves the most relevant segments based on a domain-specific query (e.g., the definition of a “producer store”).

This method aims to reduce noise and focus on the most informative parts of the document.

2. Thematic Segmentation Only

The document is segmented thematically, without any filtering.

This method preserves topic coherence while maintaining broader coverage.

3. Sliding Window

The text is split into fixed-size windows with 10% overlap.

This overlap allows the model to better capture entities that may span across segment boundaries.

4. Chunking

The text is divided into non-overlapping blocks of fixed length.

It is the fastest method but can miss boundary-crossing entities.

🔍 Evaluation Procedure
The evaluation function evaluate_gliner_with_segmentation():

Loads the GLiNER model.

Applies each segmentation strategy.

Runs the model on the segmented data.

Filters irrelevant types and computes key metrics: TP, FP, FN, precision, recall, F1-score.

📌 Open-Schema NER
The notebook Gliner_model.ipynb provided in this repository includes two main phases:

Zero-shot evaluation
The model (GLiNER) is first evaluated without any fine-tuning using a sliding window segmentation strategy with a 10% overlap. This allows us to assess its out-of-the-box performance on the annotated test set.

Supervised fine-tuning
The same model is then fine-tuned on the training portion of the dataset (after applying the same sliding window strategy), and re-evaluated on the test set. Only a subset of the model’s layers were updated during training, to avoid overfitting on limited annotated data.


Selects the best strategy by minimizing the sum of FP + FN.

The function returns all metrics and a recommendation for the optimal segmentation method for fine-tuning and deployment.
