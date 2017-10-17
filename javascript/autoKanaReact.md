# 自動ルビ生成をReactjsに実装
npmにてそれらしいパッケージを見つけたがコンポーネントをもっており、MaterialUIを利用したかったために別途作成。
historykanaを利用し、入力履歴からルビを抜き出せた。

- https://github.com/inuscript/react-auto-kana
- https://www.npmjs.com/package/historykana

## サンプル

```
import React, { Component } from 'react';
import HistoryKana from 'historykana';
import TextField from 'material-ui/TextField';

export default class SampleKana extends Component {
  constructor(props, context) {
    super(props, context);
    this.state = {
      name: '',
      nameKana: '',
      nameHistory: [],
    };
  }
  handleInputName(value) {
    const { nameHistory } = this.state;

    nameHistory.push(value);
    this.setState({
      name: value,
      nameKana: HistoryKana(nameHistory),
      nameHistory: (value) ? nameHistory : [],
    });
  }
  render() {
    const { nameKana } = this.state;

    return (
      <div>
        <TextField
          floatingLabelText="名前"
          type="text"
          value={name || ''}
          onChange={e => this.handleInputName(e.target.value)}
        />
        <TextField
          floatingLabelText="名前（カナ）"
          type="text"
          value={nameKana || ''}
          onChange={e => this.setState({ nameKana: e.target.value })}
        />
      </div>
    );
  }
}
```

## TODO
- autoCompleteによって履歴に残らない入力がなされるとルビが取れない。
- 入力削除時にルビ削除を間違うことがあるので、今後改修予定。
