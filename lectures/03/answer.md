# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：第1回の素のLLMは学習済みの知識だけで回答するが、 第3回のエージェントは用語集を検索してから回答できる。
- `--trace` で見えたツール呼び出し（ツール名と引数）：search_glossary({"query":"LoRA"}) search_glossary({"query":"QLoRA"})
- 1つの質問での LLM 呼び出し回数（`requests`）： 2回
- 追加したツールと、docstring に書いた説明：make_quiz ツールを追加した。 「指定した回の講義内容から確認問題を1問作成するためのツール」 と説明を記載した。

## 宿題

- 取り組んだレベル：基礎
- やったこと：app/agent.py の INSTRUCTIONS から 「用語や講座に固有のことを答える前に、必ず search_glossary で用語集を確認する」 という行を削除した。
- 結果：変更前は search_glossary が LoRA と QLoRA に対して呼ばれた。
変更後も search_glossary が呼ばれた。tool_calls は 2 回、 requests は 2 回だった。
- 気づき・疑問： INSTRUCTIONS の指示を削除しても search_glossary は利用された。
そのため、ツール利用の判断には INSTRUCTIONS だけでなく app/tools.py の docstring の説明も影響している可能性があると考えた。エージェントの挙動はシステムプロンプトだけでなく、 ツールの説明文にも影響されることが分かった。