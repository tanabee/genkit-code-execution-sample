# Genkit が Code Execution に対応したので試してみた

## はじめに

Genkit の version 0.5.8 で Google AI の Code Execution 機能が追加されました。これにより Python コードを実行して返すことができるようになりました。

## Genkit プロジェクトの初期化

Genkit プロジェクトの初期化を行います。Genkit のバージョンを 0.5.8 以上にする必要があるので、genkit のインストールから行います。

```sh
% npm i -g genkit
% mkdir genkit-code-execution-sample
% cd genkit-code-execution-sample

% genkit init
? Select a runtime to initialize a Genkit project:
❯ Node.js
? Select a model provider:
❯ Google AI
? Select a model provider: Google AI

? Would you like to generate a sample flow? Yes
✔ Successfully generated sample file (src/index.ts)
Genkit successfully initialized.
```

## Code Execution の有効化

generate メソッドの引数に `codeExecution: true` を足すだけで有効化できます。合わせて `prompt` は入力テキストをそのまま渡すように変更します。

```typescript
const llmResponse = await generate({
  model: gemini15Flash,
  prompt,
  config: {
    temperature: 1,
    codeExecution: true, // この行を追加
  },
});
```

## 挙動の確認

以下を実行して Developer Tool を起動します。

```
% genkit start -o
```

Flow メニューから実装した Flow を選択します。

まず、以下のプロンプトをリクエストしてみます。
「10万回コインを投げて、表が出た回数の割合をシミュレートしてください。」

[img]()

View Trace を選択すると実際にコードが実行されたことがわかります。

次に、より直接的なリクエストをしてみます。
「Python で以下のコードを実行してください: print('Hello World') 」

[img]()

先ほどと同様、View Trace を選択すると実際にコードが実行されたことがわかります。

最後に、コードとは関係のない一般的なリクエストをしてみます。

[img]()

すると、コードの実行がされていないことがわかります。これは、Code Execution が tools の 1 つの選択肢として指定されているためです。生成 AI は必要な場合にしか Code Execution を実行しません。

## まとめ

1 行追加するだけで簡単に Code Execution を試すことができました。これによって Genkit でできることの幅が広がったのではないかと思います。も是非試してみてください。

https://github.com/tanabee/genkit-code-execution-sample

## 参考資料

- Code Execution: https://ai.google.dev/gemini-api/docs/code-execution?lang=node