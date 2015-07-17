## sendLtvConversionの詳細

sendLtvConversionメソッドを利用することで、広告流入別の課金金額や入会数などを計測することができます。計測のために、任意の地点にLTV成果通信を行うコードを追加します。

ソースの編集は、成果が上がった後に実行されるスクリプトに処理を記述します。例えば、会員登録やアプリ内課金後の課金計測では、登録・課金処理実行後のコールバック内にLTV計測処理を記述します。

### Androidへの組み込み

成果がアプリ内部で発生する場合、成果処理部に以下のように記述してください。

LTV成果通知のコードを追加

```lua
Fox.sendLtvConversion(成果地点ID);
```

アプリ内部の成果に、広告主端末ID（会員IDなど）を含める事ができ、これを基準とした成果計測が行えます。LTV成果に広告主端末IDを付与したい場合は以下のように記述してください。```lua
Fox.sendLtvConversion(成果地点ID, "広告主端末ID");
```

> 成果地点ID(必須)：管理者より連絡します。その値を入力してください。広告主端末ID(オプション)：広告主様が管理しているユニークな識別子（会員IDなど）です。指定できる値は64文字以内の半角英数字です。
アプリ内計測時には、パラメータをオプションとして設定する事が可能です。
```lua
Fox.addLtvParam("パラメータ名", "値");
```

### iOSへの組み込み

```lua
Fox.sendLtv(“成果地点ID”);```

アプリ内部の成果に、広告主端末ID（会員IDなど）を含める事ができ、これを基準とした成果計測が行えます。LTV成果に広告主端末IDを付与したい場合は以下のように記述してください。

```lua
Fox.sendLtvWithBuid(成果地点ID, "広告主端末ID");
```
> 成果地点ID(必須)：管理者より連絡します。その値を入力してください。広告主端末ID(オプション)：広告主様が管理しているユニークな識別子（会員IDなど）です。指定できる値は64文字以内の半角英数字です。アプリ内計測時には、パラメータをオプションとして設定する事が可能です。

```lua
Fox.addParameter("パラメータ名", ”任意の値”);
```


### (共通)パラメータ詳細

指定できるパラメータは次の通りです。

|パラメータ名|概要|
|:------|:------|
|"_sku"|Stock Keeping Unit(商品管理コード)<br>（半角英数字32文字まで）<br>商品の在庫管理する際に使用してください|
|"_price"|Price<br>（整数値　日本円）<br>売上額を管理する際に使用してください。|
|"_currency"|Currency<br>（半角英字3文字の通貨コード）<br>通貨別で課金額を集計する際に使用してください。<br>通貨が設定されていない場合、PriceをJPY(日本円)として扱います。|
|任意でパラメータを加える事も可能です。|FoxPlugin::addParameter(“パラメータ名”, “値”);<br>※1 同一パラメータ名を記述した場合は、後者が有効となります。<br>※2 アンダースコア（"_"）をパラメータ名の先頭に記述しないでください。<br>※3 半角英数字以外は使用できません。|

CC_LTV_PARAM_CURRENCYには[ISO 4217](http://ja.wikipedia.org/wiki/ISO_4217)で定義された通貨コードを指定してください。

**[Lua記述例]**
```lua
// Android
Fox.addLtvParam("_sku", "ABC1234")Fox.addLtvParam("_price”, 2000)Fox.addLtvParam("_out", 1)Fox.addLtvParam("my_param", "ABC")Fox.sendLtvConversion(70, "Taro")
// iOS
Fox.addParameter(“_sku”, “ABC1234”)Fox.addParameter(“_price”, 2000)Fox.addParameter(“_out”, 1)Fox.addParameter(“_currency”, USD)Fox.addParameter(“my_param”, “ABC”)Fox.sendLtv(70, “Taro”)
```
