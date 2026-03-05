# Skill Drill - Project Guide

## プロジェクト概要

NLP研究者志望のAIエンジニアによる学習・競技・研究の統合リポジトリ。
Kaggle NLPコンペへの参戦、LLM実装の実験、PhD出願準備を一箇所で管理する。

## ディレクトリ構成

```
skill_drill/
├── kaggle/            # Kaggleコンペ関連（コンペ名ごとにサブディレクトリ）
│   └── <comp_name>/   # EDA, feature engineering, モデル, submission
├── learning_log/      # 論文読みメモ、学習ノート、振り返り
├── llm_engineering/   # LLM・Transformer実装実験、再現実装
├── phd_prep/          # PhD出願用の研究計画書、SoP下書き、志望校リスト
└── tools_practice/    # PyTorch, HuggingFace, wandb等のツール練習
```

## よく使うコマンド

```bash
# Git操作
git status
git add -p                       # 変更を確認しながらステージング
git commit -m "内容"
git log --oneline -10

# Python実行
python <script>.py
jupyter notebook                 # ノートブック起動
pytest tests/                    # テスト実行

# 仮想環境
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## ML/NLP コーディング規約

1. **シード固定**: 再現性のため、実験コードでは必ず乱数シードを固定する
   ```python
   import random, numpy as np, torch
   def seed_everything(seed=42):
       random.seed(seed)
       np.random.seed(seed)
       torch.manual_seed(seed)
       torch.cuda.manual_seed_all(seed)
   ```

2. **Data Leakage 防止**: train/validation/test分割は前処理・特徴量生成より先に行う。テストデータの統計量を学習に使わない

3. **実験ログ必須**: 実験の条件（ハイパーパラメータ、データバージョン、モデル構成）と結果（スコア、学習曲線）を必ず記録する。wandb, MLflow, またはMarkdownメモのいずれかで管理

4. **型ヒント推奨**: 関数の引数・戻り値には型ヒントをつける

5. **マジックナンバー禁止**: ハイパーパラメータや定数は変数・設定ファイルで管理する

6. **GPU対応の書き方**: `device = torch.device("cuda" if torch.cuda.is_available() else "cpu")` でデバイスを統一管理する

## ルール

- **コードの説明を求められたら必ず日本語で答えること**
