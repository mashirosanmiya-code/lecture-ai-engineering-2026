# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：素のLLMは、学習済みの知識をもとに直接回答する。一方、エージェントは質問に応じてツールを呼び出し、用語集などの情報を取得してから回答できる。
- `--trace` で見えたツール呼び出し（ツール名と引数）：make_quiz({'lecture': 2})
第2回の用語から確認問題を作るために、make_quizが呼び出された
- 1つの質問での LLM 呼び出し回数（`requests`）：2回
- 追加したツールと、docstring に書いた説明：make_quiz(lecture: int)
指定した回の用語から1つを選び、確認問題と答えを返す。第2回の確認問題を出して、のように復習問題を求められたときに使う。

## 宿題

- 取り組んだレベル：基礎
- やったこと：基礎レベルに取り組んだ。
  - app/agent.py の INSTRUCTIONS から「用語や講座に固有のことを答える前に、必ず search_glossary で用語集を確認する」という指示を削除した。
  - app/tools.py の search_glossary の docstring を変更し、「用語の意味や定義を詳しく知りたいときに使う」という説明にした。
  - それぞれ変更した後、同じ質問「SFTとは何？」を --trace 付きで実行した。
- 結果： - INSTRUCTIONS を変更する前も、変更した後も search_glossary が呼び出された。
  - docstring を変更した後も search_glossary が呼び出された。
  - どの場合も query は「SFT」で、LLM の呼び出し回数（requests）は2回だった。
  - 回答の内容は大きく変わらなかったが、文章の長さや表現に少し違いが見られた。
- 気づき・疑問： - INSTRUCTIONS から検索を必須にする指示を削除しても、AIは search_glossary を呼び出した。なぜINSTRUCTIONSから検索を必須にする指示を削除してもAIはsearch_glossaryを呼び出したのか。
