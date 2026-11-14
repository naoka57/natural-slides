# natural-slides

AIが作る日本語スライドにありがちな「細い線・余白だらけ・均等3カラム・箇条書きの羅列・ですます調の説明文」を避けるための、Claude 向けスキル。図とイラスト、太い線、言い切る文で、人が手で作ったように見える資料を作る。営業資料、提案書、会社紹介、サービス説明、セミナー資料、テンプレートを想定している。

特定の会社や業種に縛られないよう作ってある。メインカラー1色・ロゴ・社名を「ブランド設定」で差し替えれば、そのまま自分の資料に使える。色や線の太さ、図解の型（工程フロー、ピラミッド、マトリクス、ベン図など）、余白の取り方まで具体的な数値で指示しているのが中身の大半。

## 何をするスキルか

Claude にスライドを作らせると、どうしても「それっぽいけど中身の薄い」仕上がりになりやすい。このスキルは、その「AIっぽさ」の出どころを一つずつ潰していく。たとえば枠線は6〜9pxと太くする、要点は「・」ではなく円で囲んだ番号で並べる、段階を見せるときはピラミッド図を使う、タイトルに句読点を入れない、本文をです・ます調にしない、といった具合に、判断に迷いやすいところを数値とルールで固定する。

出力形式を指定しなければ、その環境で使えるスライドの仕組み（スライド型のアーティファクト、`.pptx`、HTML など）で作る。比率は16:9、1920×1080基準。

PowerPoint・Canva・Googleスライドに持っていっても崩れにくいよう、組み方も決めてある。文字は見出しと段落の2種類だけで書き、円は図形、矢印はコネクタとして置く。ピルは幅と高さを数値で決めた箱の中に文字を置き、マーカーは独立した一行にする。書き出したあとでも、文字の打ち替えや図形の移動ができる。見せるだけで編集しないなら PDF が一番崩れない。詳しくは SKILL.md の「書き出しやすい構成」にある。

## 使い方

Claude Code や Claude のスキル対応環境で、`skills/natural-slides/SKILL.md` を読み込める場所に置く。

### claude.ai（Claude のアプリ）で使う

`skills/natural-slides` フォルダを丸ごと zip にする。zip の中身は `natural-slides/SKILL.md` と `natural-slides/brand.example.md` の形になっていればいい。

```bash
git clone https://github.com/yoshitakagiii/natural-slides.git
cd natural-slides/skills && zip -r ../../natural-slides.zip natural-slides
```

claude.ai の「カスタマイズ」から「Skills」を開き、「+追加」→「Skills をアップロード」で zip を選ぶ。新しい版に入れ替えるときも同じ手順で、「アップロードして置き換え」を選ぶ。前の版はバージョン履歴に残る。

### Claude Code で使う

Claude Code の場合、ユーザー全体のスキルとして使うなら、このリポジトリを clone して中の `skills/natural-slides` を `~/.claude/skills/` にコピーする。

```bash
git clone https://github.com/yoshitakagiii/natural-slides.git
cp -r natural-slides/skills/natural-slides ~/.claude/skills/
```

プロジェクト単位で使うなら、同じものをそのリポジトリの `.claude/skills/` 以下に置く。

置いたあとは「このサービスの営業資料を作って」「提案書のテンプレートを作って」のように頼めば、スキルの説明文にある条件に合ったときに Claude が自動で読み込む。明示的に呼びたいときは `/natural-slides` のように指定する環境もある。

## 最初に使うとき

初めて資料を頼むと、Claude は作り始める前に、いまの既定値を見せてブランド設定を一度だけ尋ねる。尋ねるのはメインカラー、書体、ロゴ、会社名・サービス名、主な出力先（PDF・PowerPoint・Googleスライド・Canva）の5つ。「このままでいい」と答えれば、既定値（メインカラー #2F3237、Montserrat ＋ Noto Sans JP）で作る。

決まった設定は、Claude Code ならスキルのフォルダに `brand.md` として保存され、次からは尋ねずにその設定で作る。claude.ai のようにスキルのフォルダに書き込めない環境では、Claude が設定の中身を渡すので、プロジェクトの指示に貼っておく。

質問を飛ばしたいなら、先に `skills/natural-slides/brand.example.md` を `brand.md` という名前でコピーし、値を書き換えておけばいい。

## 文章の自然さを上げたいとき

スライドに載せる文の自然さをさらに詰めたいときは、日本語の文章スキルと併用するとよい。相性がいいのは [coji/natural-japanese](https://github.com/coji/natural-japanese)（MIT）。natural-slides 単体でも動くので、必須ではない。

## ライセンス

MIT License. 詳しくは [LICENSE](LICENSE) を参照。

スキルが生成するイラストや書体（Montserrat / Noto Sans JP）そのもののライセンスは、それぞれの提供元の条件に従うこと。詳しくは [NOTES.md](NOTES.md) にまとめた。
