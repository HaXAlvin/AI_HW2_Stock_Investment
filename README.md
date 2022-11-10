# Requirements

**python=3.7.15**


torch==1.12.1

torchaudio==0.12.1

torchvision==0.13.1

gym==0.25.2

gym-anytrading==1.3.2

matplotlib>=3.2.2

numpy==1.21.6

tqdm==4.64.1

# Run

1. Prepare stock csv dataset (at least 2500 rows, otherwise change the `frame_bound` arg of gym env), and put the csv file at same project folder.
2. Rename the filename in code, default is `2330_stock.csv`.
3. Train => run `train.ipynb` file. When it's done, it will output a `model.ckpt` file for model state dict.
4. Test => run `test.py` file. When it's done, it will ouput a `action.txt` file as the result.

# Usage of test.py

usage: test.py [-h] [--start START] [--end END] [--output_action_file_pathname OUTPUT_ACTION_FILE_PATHNAME]

optional arguments:
  -h, --help
                        show this help message and exit
  --start START, -s START
                        stock investment start date index
  --end END, -e END
                        stock investment end date index
  --output_action_file_pathname OUTPUT_ACTION_FILE_PATHNAME, -f OUTPUT_ACTION_FILE_PATHNAME
                        output action file pathname
