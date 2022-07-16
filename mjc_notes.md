# 2022-07-16 15:14:59 make a new conda env for volt 

```sh
export PROJ=volt
mamba create -y --name $PROJ python=3.7 -c pytorch -c conda-forge

# now I want to install pytorch with conda to avoid cuda issues, make sure we get the right version by looking at nvidia-smi to get cuda version. pick the closest
mamba install -y  pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
mamba install botorch -c pytorch -c gpytorch -c conda-forge

# install kernel
mamba install -y ipykernel pip ipywidgets
python -m ipykernel install --user --name $PROJ --display-name $PROJ

# install this
pip install -e .
```


# data

instead of using robinhood (US only) we will use tingo

```py
import datetime
import pandas_datareader as pdr
# restricting to 1996-01-04 00:00:00 2019-06-28 00:00:00
api_key = os.environ["TIINGO_API_KEY"]
start = datetime.datetime(1996, 1, 4)
end = datetime.datetime(2019, 6, 28)
tickers = ["MSFT", "AAPL", "XOM"] #, "TUR", "RSX", "EWY", "EWS", "VTIP", "TLT", "BWX", "PDBC", "IAU", "VNQI"]

symbols = pdr.get_data_tiingo(tickers, api_key=api_key, start=start, end=end)
symbols
```