# 株価分析アプリケーション - インストール手順書

## システム要件

### 必須環境
- **Python**: 3.8以上（推奨: 3.9-3.11）
- **OS**: Windows 10/11, macOS 10.14+, Linux（Ubuntu 18.04+）
- **メモリ**: 最低4GB（推奨: 8GB以上）
- **ストレージ**: 2GB以上の空き容量

### 注意事項
- TensorFlow使用時は追加で500MB以上の容量が必要
- GPU使用時はCUDA対応のNVIDIA GPUとCUDAドライバが必要

## インストール手順

### 1. リポジトリのクローン
```bash
git clone <repository-url>
cd My-Claude-Code-Communication
```

### 2. 仮想環境の作成（推奨）
```bash
# Python venv使用の場合
python -m venv stock_analysis_env
source stock_analysis_env/bin/activate  # Linux/macOS
# または
stock_analysis_env\Scripts\activate     # Windows

# conda使用の場合
conda create -n stock_analysis python=3.9
conda activate stock_analysis
```

### 3. 基本ライブラリのインストール
```bash
pip install -r requirements.txt
```

### 4. オプションライブラリのインストール（必要に応じて）

#### TensorFlow（LSTM予測機能用）
```bash
# CPU版（軽量）
pip install tensorflow-cpu>=2.13.0

# GPU版（高性能、CUDA必須）
pip install tensorflow>=2.13.0

# または個別にインストール
pip install -r OPTIONAL_REQUIREMENTS.txt
```

## アプリケーションの起動

```bash
# メインディレクトリから
streamlit run ProjectWorkspace/Project-5/Stock_analysis/stock-prediction-app.py

# または直接ディレクトリに移動して実行
cd ProjectWorkspace/Project-5/Stock_analysis
streamlit run stock-prediction-app.py
```

ブラウザで `http://localhost:8501` にアクセス

## 機能別要件

### 基本機能（全て必須）
- ✅ 株価データ取得・表示
- ✅ テクニカル分析（移動平均、RSI、MACD等）
- ✅ インタラクティブチャート
- ✅ ニュース取得・感情分析

**必要ライブラリ**: streamlit, pandas, numpy, matplotlib, plotly, requests, scikit-learn, statsmodels, textblob, vaderSentiment, joblib

### 高度な予測機能（オプション）
- 🔶 LSTM神経網による価格予測
- 🔶 深層学習モデルによる予測精度向上

**追加ライブラリ**: tensorflow

## トラブルシューティング

### よくある問題と解決法

#### 1. TensorFlowインストールエラー
```bash
# 古いバージョンの削除
pip uninstall tensorflow tensorflow-gpu tensorflow-cpu

# 最新版の再インストール
pip install tensorflow>=2.13.0
```

#### 2. メモリ不足エラー
- 仮想メモリを増やす
- TensorFlowを使用しない設定に変更
- より軽量なデータセットを使用

#### 3. ポート使用エラー
```bash
# 異なるポートで起動
streamlit run stock-prediction-app.py --server.port 8502
```

#### 4. API制限エラー
- アプリ内の設定で取得間隔を調整
- 複数のAPIキーを設定（該当する場合）

## 依存関係の詳細

### コアライブラリ
| ライブラリ | バージョン | 用途 |
|-----------|-----------|------|
| streamlit | >=1.28.0 | Webアプリフレームワーク |
| pandas | >=2.0.0 | データ分析・操作 |
| numpy | >=1.24.0 | 数値計算 |
| matplotlib | >=3.7.0 | 基本的な可視化 |
| plotly | >=5.15.0 | インタラクティブ可視化 |

### 機械学習・統計
| ライブラリ | バージョン | 用途 |
|-----------|-----------|------|
| scikit-learn | >=1.3.0 | 機械学習アルゴリズム |
| statsmodels | >=0.14.0 | 統計モデル（ARIMA等） |
| joblib | >=1.3.0 | モデル保存・読込 |

### 自然言語処理
| ライブラリ | バージョン | 用途 |
|-----------|-----------|------|
| textblob | >=0.17.1 | 基本的な感情分析 |
| vaderSentiment | >=3.3.2 | 高度な感情分析 |

### オプション（深層学習）
| ライブラリ | バージョン | 用途 |
|-----------|-----------|------|
| tensorflow | >=2.13.0 | LSTM神経網予測 |

## パフォーマンス最適化

### 推奨設定
1. **キャッシュ設定**: アプリ内で1時間のデータキャッシュが有効
2. **メモリ使用量**: 基本機能のみで約500MB、TensorFlow使用時は1-2GB
3. **CPU使用率**: シングルコア使用、マルチコア環境では並列処理が効率的

### 高速化のヒント
- 初回起動時はライブラリの読み込みに時間がかかります
- TensorFlowモデルのトレーニングは時間がかかるため、事前トレーニング済みモデルの使用を推奨
- 大量データ分析時は仮想メモリの設定を確認

## サポート・問い合わせ

技術的な問題や追加の機能要求については、プロジェクトのIssueページまたは管理者まで連絡してください。

---
**注意**: このアプリケーションは教育・研究目的で開発されており、投資判断には十分な注意と追加の分析が必要です。