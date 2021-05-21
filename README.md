# childes-tagging
reformatting soon
Current steps require running notebooks in Jupyter, but I'm planning to add command-line functionality
https://docs.google.com/document/d/1nDBty5LLoRhuC5l6h0QlKRcKQ6hKNCfNIEenbQm8u1I/edit

## Steps to run analysis:
### 1. Sample token IDs with `sampling.ipynb` → `sampled_full.csv` with full token information of sampled IDs join-merged with the corresponding utterance gloss for each token
`analyzable_results/sampled_full_english_v4.csv` is an example result of running `sampling.ipynb`.
Adjust parameters in code block 2. 
### 2. Hand-annotate the sampled tokens for part-of-speech
Add the correct part of speech tags to `sampled_full.csv` in a new column called `correct_pos`.
### 3. Add the model's tags
Input your updated `sampled_full.csv` into `tagging.ipynb` to produce `sampled_tagged.csv`.
By default, `tagging.ipynb` uses spacy, but it can easily be adjusted for any model using the third code block. The adjustments for CoreNLP and Stanza are currently in block 3 but commented out.
Adjust parameters in code block 2.
### 4. Create part-of-speech mappings
a. One mapping from CHILDES part of speech category to a compatible-set category. `remappings/childes_pos_remapping_full - childes_simplified_pos_full.csv` is an example.
b. A second mapping from the model's POS and morphology categories to a compatible-set category. `remappings/spacy_childes_pos_mapping_full - spacy_childes_pos_mapping_full.csv` is an example.
`spacy_pos_morph_pairs.ipynb` generates all possible spaCy POS-morphology combinations, which may be helpful in creating the mapping for other models.
The mappings should have specific column names like `spacy_part_of_speech`, `spacy_morphology`, `spacy_pos_converted` and `childes_simplified_pos`, `childes_remapped_pos`. Replace "spacy" above with the name of the model you are using, which is the same name provided as a parameter to `tagging.ipynb`.
### 5. Using these two mappings, use `scoring.ipynb` to generate precision, recall, and F1 score for the models, and view the confusion matrix.
Currently, the notebook does some maneuvering to handle incomplete annotations, which may create strange results.
