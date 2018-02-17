# nlp-bible
A quirky bible passage generator using the powerful character-level RNN from https://github.com/jcjohnson/torch-rnn

### Use - Preprocessing

1. Run `python proccess.csv` to process the King James CSV into the following format:

BOOK X, CHAPTER XX:
asdfaasdfsdf
asdfasdfsadfasd
asdfasdfsadfasdasdfdsffd
asdsdasd


### Usage - Running, Preprocessing, Training, and Sampling

1. Run the docker container - we used docker because we had trouble installing hdf5 on mac - if you want to give it a shot, check out the instructions from the original
    * `docker run --rm -ti crisbal/torch-rnn:base bash`

2. Change the docker image name to `nlp-bible` (This will be for ease of copying to the docker container in the next step)

3. Copy the processed text into the data/ folder of the docker container:



2. Preprocess the sample data - this converts our generated `bible-text.txt` file into the required formats of `HDF5` (.h5) and `JSON` (.json)

    ```
    python scripts/preprocess.py \
    --input_txt data/bible-text.txt \
    --output_h5 data/bible-text.h5 \
    --output_json data/bible-text.json
    ```

3. Train the model! With some testing and time at NLP champs, we found some of the best results using NNNN layers with MMM neurons each:

    ```
    th train.lua \
    -input_h5 data/bible-text.h5 \
    -input_json data/bible-text.json \
    -gpu -1
    ```

So, sit back, maybe grab a :beer: and relax until the training is done... Depending on your hardware, this could take up to a few hours

4. Sample from the model!
    * `th sample.lua -checkpoint cv/checkpoint_10000.t7 -length 2000 -gpu -1`
