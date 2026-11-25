# Dataset setup: LAV-DF

The LAV-DF dataset is **not redistributed** in this repository.

1. Obtain the dataset from its official project/source and follow its access and usage terms.
2. Attach or download it into your environment.
3. In Kaggle, add the dataset as notebook input. The notebooks include dataset-discovery/path logic and expect read-only inputs under `/kaggle/input/`.
4. Confirm that the metadata and video files are present before running preprocessing.

The notebooks use a balanced 1,000-video experiment subset (500 real and 500 fake) with a 600/200/200 train/validation/test allocation. Follow the split-generation or split-loading logic in each notebook; do not assume that separately generated splits contain identical video IDs unless the saved split metadata confirms it.
