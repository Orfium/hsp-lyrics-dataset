# hsp-lyrics-dataset

## Description

This dataset is based on the [Hit Song Prediction (Million Song Dataset and Audio Features)](https://zenodo.org/record/3258042), which contains 95,067 songs that are representative of hits and non-hits based on their entrance or not to the Billboard Hot 100 charts. The dataset comprises release year information, high- and low-level audio features, the highest Billboard rank, if it is featured in the chart, and metadata for each song. Please refer to https://zenodo.org/record/3258042 for further information on the Hit Song Prediction dataset.

We extend the aforementioned dataset with features derived from the lyrics of each sound recording. We use the [Genius](https://genius.com) database, which contains a collection of approximately 25 million songs and lyrics, from which we retrieve 11,634 song lyrics. We use multilingual BERT in order to extract the text embedding from the lyrics of each song.

In Particular our dataset contains the following files:
* **lyrics_embeddings.json** which contains the [MSD](http://millionsongdataset.com) id, that is a unique identifier for every track, the Genius id, that can be used to query the Genius API for the lyrics retrieval, and the textual embeddings that were computed from the last layer of the multilingual BERT model. 
* **hsp_hits.csv** which is a subset of the msd_bb_matches.csv file from the Hit Song Prediction dataset and contains information about the MSD tracks that were also featured in the Billboard Hot 100 charts, i.e. the MSD id, Echo Nest id, artist name, track title, release year, peak position in Billboard charts and the number of weeks in the charts.
* **hsp_non_hits.csv** which is a subset of the msd_bb_non_matches.csv file from the Hit Song Prediction dataset and contains meta-information about the tracks of the MSD that were not featured in the Billboard Hot 100 and hence were used as negative samples, i.e. the MSD id, Echo Nest id, artist name, track title and the release year.
* **low_level_hits.json** contains a subset of the low-level audio features computed in the Hit Song Prediction for the hits class, organized by the MSD id of evey track.
* **low_level_non_hits.json** contains a subset of the low-level audio features computed in the Hit Song Prediction for the non hits class, organized by the MSD id of evey track.
* **high_level_hits.csv** contains a subset of the high-level audio features computed in the Hit Song Prediction for the hits class, organized by the MSD id of evey track.
* **high_level_non_hits.csv** contains a subset of the high-level audio features computed in the Hit Song Prediction for the non hits class, organized by the MSD id of evey track.

## Download
In order to download the zipped data use the following instructions
```
aws s3 cp s3://audio-video-datasets/internal/hit-song-prediction/data/hsp_lyrics_dataset/ ./ --recursive
```

## Reproducibility
In order to reproduce our results stated in the paper seed everything with the number 42. In order to balance the hits/non_hits classes use
```
hsp_non_hits = msb_non_hits.sample(n=hsp_hits.shape[0], random_state=42)
```
in Pandas Python library

