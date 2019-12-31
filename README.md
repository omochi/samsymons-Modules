# 更新履歴

## 構成の単純化と変な挙動の解消

- 少し変更してからリビルドするとコケる問題を解消。
- ヘッダーのコピーを削除。
- `Defines Module`を`NO`、`Module Map File`の設定を削除。
- `module.modulemap`が複雑でよくわからなかったので単純化。
  ミソとして、`StaticLibraryModule.Model`などのサブモジュールの中に`export *`が無いと、
  ソース側の`#import`がコンパイラにモジュールインポートに差し替えられたところで、
  `Foundation`のシンボルが見えなくてうまくいかない、という問題があった。
- ユーザ側の`Import Paths`にディレクトリを追加。
  これは何が起きてるかわかりやすい構成だと思う。
  ただ、Xcode的にはここが自動解決する構成が可能なはずだ・・・。
- `Enable Modules`が`YES`になるだけで振る舞いが変わるので、
  コンパイラが`module.modulemap`をアグレッシブに発見してると思われる。

# Modules

An example of Objective-C static library & framework modules.

### StaticLibraryModule

The static library module includes a customize module map, with multiple submodules.

This is used by the `StaticLibraryModuleConsumer` target, to demonstrate importing and using of the static library's API.

### FrameworkModule

The framework target does not customize its module support in any way. Instead, this is a demo of how and why frameworks can get module support for free.
