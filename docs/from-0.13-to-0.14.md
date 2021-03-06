# 从 0.13 升级到 0.14

## 简化导入入口

ali-react-table 原来提供了过多的 import 入口，记忆成本过大。v0.14 移除了 `ali-react-table/biz` 这个导入入口，原先从该入口导出的 API 现在都已经合并到 `ali-react-table` 中。

```diff
- import { applyTransforms, proto } from 'ali-react-table/biz'
+ import { applyTransforms, proto } from 'ali-react-table'
```

1.0 之前 `ali-react-table/biz` 仍然可用，但在使用时会进行警告。

## 移除 `commonTransforms` 对象

commonTransforms 被拆分了为了多个独立的函数，包括 makeSortTransform、makeTreeModeTransform、makeColumnHoverTransform 等。 v0.14 移除了 commonTransforms，commonTransforms.XX 改名为 makeXXTransform。

```diff
- import { applyTransforms, commonTransforms } from 'ali-reac-table/biz'
+ import { applyTransforms, makeTreeModeTransform } from 'ali-react-table'

const renderData = applyTransforms(
  input,
-  commonTransforms.treeMode({ primaryKey: 'name', openKeys, onChangeOpenKeys }),
+  makeTreeModeTransform({ primaryKey: 'name', openKeys, onChangeOpenKeys }),
)
```

1.0 之前 commonTransforms 在 `ali-react-table/biz` 中仍然可用，但在使用时会进行警告。

## 移除 `useOperationBar` 和 `CustomColumnsDialog`

这两个 API 和 ali-react-table 的定位有些不符，由 ali-react-table 进行提供并不合适。v0.14 移除了这两个 API。

1.0 之前这两个 API 在 `ali-react-table/biz` 中仍然可用，但在使用时会进行警告。

## 移除 dvt-aggregation 依赖

移除 dvt-aggregation 依赖，如果原先有使用 createAggregateFunction 函数的情况，请手动安装 [dvt-aggregation](https://github.com/shinima/dvt-aggregation/)。
