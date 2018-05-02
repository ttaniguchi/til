# 概要
JSでカメラデバイス操作をおこなう方法とその知見。

## 基本構文
```html
<html>
<body>
  <video id="video" width="640" />
</body>
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>
<script>
  navigator.getUserMedia({ audio: true, video: { width: 1280, height: 720 } },
    (stream) => {
      const video = document.querySelector('#video');
      // 廃止予定 video.src = URL.createObjectURL(stream);
      video.srcObject = stream;
      video.onloadedmetadata = (e => video.play());
    },
    err => console.log("The following error occurred: " + err.name),
  );
</script>
</html>
```

## ローカルでのテスト
ssl環境を構築できない場合はChromeを以下のモードで起動する。

```sh
open -a "/Applications/Google Chrome.app" --args --unsafely-treat-insecure-origin-as-secure="http://0.0.0.0:3000/"
```

※ http://0.0.0.0:3000/ が対象URL

## デバイス一覧の取得

```js
// デバイス一覧の取得
navigator.mediaDevices.enumerateDevices()
  .then(devices => console.log(devices))
  .catch(error => console.log(error));

// devices の内容
[
  {
    deviceId: "default",
    groupId: "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff", // (16進数コード)
    groupId: "6358795a402060b0164502d6ddebe9e898e06f473b41785e0acf0c2f9853a6af",
    kind: "audioinput",
    label: "既定 - 内蔵マイク",
  },
]
```
