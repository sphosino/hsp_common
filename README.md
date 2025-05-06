# 🧩 common - 共通HSPモジュール集

このフォルダは、複数のHSPプロジェクトで再利用できる共通モジュールを集めたリポジトリです。

---

## 🚀 使い方

  プロジェクト側から、必要なモジュールを個別に `#include` して利用してください。
  
  例：
  
  ```hsp
  #include "../common/basic_mod1.hsp"
  #include "../common/basic_mod3.hsp"
  ```

⚠ 重要な注意点
✅ 各モジュールファイル内では、他のファイルを #include ではなく #addition を使って読み込んでください！

❌ #include を使うと、  呼び出し側がどこから呼び出すか分からないため、正しいパスでインクルードできず、コンパイルが通りません。

✅ 正しくはこう！
```
// OK: 呼び出し側で順序を制御できるようにします（同時に依存関係の明示になる）
#addition "basic_mod1.hsp"
```
#addition を使うことで、呼び出し側（プロジェクト）からの明示的な制御が可能になり、依存関係の混乱や多重インクルードを避けることができます。
📚 モジュールの依存関係

一部のモジュール（例：basic_mod3.hsp）は他のモジュール（例：basic_mod1.hsp）に依存している場合があります。
その場合は、プロジェクト側の #include 順序で制御してください。

📂 想定ディレクトリ構成（例）
- root
  - project1/
    - ├── main.hsp //basic.hspをインクルード。
    - ├── basic.hsp 
    -  └── modules/
  - common/
    - ├── basic_mod1.hsp
    - ├── basic_mod2.hsp
    - └── basic_mod3.hsp　#addition "basic_mod1.hsp" //includeではなくadditionで依存関係を明示
   
basic.hspに相対パスでまとめて記述  
#include "../common/basic_mod1.hsp"  
#include "../common/basic_mod3.hsp"  


🛠 開発者向けメモ
    #include は使わないでください。（hspが最初のスクリプト基準の相対パスのため）
    新しいモジュールを追加する際は、依存関係を明記して #addition を使ってください。
    
