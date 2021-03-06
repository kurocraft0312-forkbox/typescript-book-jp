# Barrel

バレル\(Barrel\)とは、複数のモジュールから1つの便利なモジュールにエクスポートをロールアップする方法です。バレル自体は、他のモジュールの選択されたエクスポートを再エクスポートするモジュールファイルです。

ライブラリ内の次のクラス構造を想像してみてください:

```typescript
// demo/foo.ts
export class Foo {}

// demo/bar.ts
export class Bar {}

// demo/baz.ts
export class Baz {}
```

バレルがなければ、ユーザーは3つのインポート文を必要とするでしょう：

```typescript
import { Foo } from '../demo/foo';
import { Bar } from '../demo/bar';
import { Baz } from '../demo/baz';
```

代わりに、以下を含む`demo/index.ts`バレルを追加することができます：

```typescript
// demo/index.ts
export * from './foo'; // re-export all of its exports
export * from './bar'; // re-export all of its exports
export * from './baz'; // re-export all of its exports
```

今、ユーザーは必要なものをバレルからインポートできます：

```typescript
import { Foo, Bar, Baz } from '../demo'; // demo/index.ts is implied
```

## 名前付きエクスポート

`*`をエクスポートする代わりに、モジュールを名前でエクスポートすることができます。たとえば、`baz.ts`に次のような機能があるとします。

```typescript
// demo/foo.ts
export class Foo {}

// demo/bar.ts
export class Bar {}

// demo/baz.ts
export function getBaz() {}
export function setBaz() {}
```

`getBaz`/`setBaz`をdemoからエクスポートしたくない場合、代わりに別名でそれらをインポートし、その別名でエクスポートすることで変数に入れることができます：

```typescript
// demo/index.ts
export * from './foo'; // re-export all of its exports
export * from './bar'; // re-export all of its exports

import * as baz from './baz'; // import as a name
export { baz }; // export the name
```

そして今、ユーザーは次のようになります：

```typescript
import { Foo, Bar, baz } from '../demo'; // demo/index.ts is implied

// usage
baz.getBaz();
baz.setBaz();
// etc. ...
```

