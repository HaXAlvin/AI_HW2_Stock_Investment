利用強化學習 (Reinforcement Learning) 進行股票投資決策
必須在 AnyTrading 這個環境進行股票投資
允許同學以範例程式碼為基礎進行修改
Training code example: https://colab.research.google.com/drive/1zmx4lNeyBV24krXjmW-h8O7cPDD-VFOS
Testing code example: https://colab.research.google.com/drive/1ZhWZkx5N77QWrfZ2MUa4s9Wt9dIFPFGC
繳交格式請參考作業說明簡報
若有問題請來信至 ncu-ai-2022fall-ta@googlegroups.com，請勿私訊助教

以下為 Homework2 第三點補充說明：
有鑑於說明不清楚導致部分同學誤解說明的意思，在這邊補充說明。
補充說明第三點所提到的，禁止修改的環境參數及環境功能是指覆寫原先 AnyTrading 環境的參數 (class parameter) 及功能 (class function)。
如參數 (window_size、手續費大小等) 以及功能 (_calculate_reward、_update_profit等) 修改 (其中連結為 AnyTrading 環境 github 程式碼)。
至於 AnyTrading 環境回傳的 reward 要如何使用及更新模型，則不在此限制中。故不影響作業第1.2題的回答內容。


以下為 Homework2 補充說明：
AnyTrading 環境在計算 profit 時會計算買入以及賣出時股票價值的手續費 (可參考原始環境套件 github)，所以並不是單純的 (初始本金 - total_reward = 最終本金)。
RL 方法模型可使用套件。
AnyTrading 環境的參數修改僅限資料集 feature 欄位的使用 (_process_data 功能)  以及 frame_bound 範圍 (可參考以下 training 程式範例)。其餘參數 (class parameter: window_size、手續費等) 修改以及功能 (class function: _calculate_reward、_update_profit等) 覆寫，將會視為程式無法正確執行 (程式執行成績 <=25%)。
def my_process_data(env):
    start = env.frame_bound[0] - env.window_size
    end = env.frame_bound[1]
    prices = env.df.loc[:, 'Low'].to_numpy()[start:end]
    # 這邊可修改想要使用的 feature
    signal_features = env.df.loc[:, ['Close', 'Open']].to_numpy()[start:end]
    return prices, signal_features
 
 
class MyStocksEnv(StocksEnv):
    # 除 _process_data 外，其餘功能 (class function) 禁止覆寫
    _process_data = my_process_data
 
# window_size: 能夠看到幾天的資料當作輸入, frame_bound: 想要使用的資料日期區間
# 可修改 frame_bound 來學習不同的環境資料
# 不可修改此處 window_size 參數
env = MyStocksEnv(df=STOCKS_TSMC, window_size=10, frame_bound=(1000, 1500))