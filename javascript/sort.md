# sort
https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

## 構文
array.sort(compareFunction);

- コールバックは整数を返す。
- 戻り値が正の整数であれば後に、負の整数であれば前にソートされる。

```
function compare(a, b) {
  if (ある順序の基準において a が b より小)
     return -1;
  if (その順序の基準において a が b より大)
     return 1;
  // a は b と等しいはず
  return 0;
}
```

## オブジェクトのソート
オブジェクト内のidによってソートをおこなうサンプル。

```
list = [
  { id: 2, name: 'taro' },
  { id: 1, name: 'jiro' },
  { id: 3, name: 'kojiro' },
]
list.sort((a, b) => (a.id - b.id)));
```
