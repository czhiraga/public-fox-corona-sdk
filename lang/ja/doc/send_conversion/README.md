## sendConversionの詳細(Android)

sendConversionメソッドを利用することで、インストール計測を行うことができます。Cookie計測を利用する場合には、外部ブラウザが起動されます。この際、外部ブラウザの遷移先をsendConversionの引数にURL文字列を指定することができます。

**[Lua記述例]**

ベーシックな成果通知の実装
```lua
Fox.sendConversion(”default”);
```

広告主端末IDを第二引数に指定する記述例
```lua
FOX.sendConversionWithStartPageUrl("default", "")
```
第二引数に広告主端末IDを渡すことができます。例えば、アプリ起動時にUUIDを生成し、初回起動の成果と紐づけて管理したい場合等に利用できます。

> ※上記"default"に自身のURLスキームを設定することで、ブラウザ起動後すぐにアプリケーションに戻る動作とすることもできますが、URLスキームを指定した場合にはHTMLページを経由しないため、HTML計測タグに対応できず、タグによる計測が必要となった際にアプリの更新が必要となるデメリットがありますので、HTMLページをご用意いただくことを推奨します。


**インストール計測クラス仕様**

|Javaクラス名|Luaプラグインメソッド名|プラグインメソッド概要|
|:------:|:------:|:------|
|CoronaAdManager|sendConversion|**第一引数 :** アプリ起動後に表示するページのURL||CoronaAdManager.SendConversionWithStartPageUrl|sendConversionWithStartPageUrl|**第一引数 :** アプリ起動後に表示するページのURL<br>**第二引数 :** 広告主端末ID（指定しない場合は “” (空値)を指定してください。|
> ※sendConversionWithStartPageUrlは起動直後の処理として実装いただくため、ログインIDなどを引数として渡すことはできません。
## sendConversionの詳細(iOS)
**[Lua記述例]**

ベーシックな成果通知の実装
```lua
Fox.sendConversionWithStartPage(”default”);
```

sendConversionWithStartPageの代わりにsendConversionWithBuidメソッドを利用し、成果ログに広告主端末IDを付与することができます。例えば、アプリ起動時にUUIDを生成し、初回起動の成果と紐付けて管理したい場合等に、利用できます。
```lua
Fox.sendConversionWithBuid(”default”, ”your unique id”);
```

> ※sendConversionWithStartPageは起動直後の処理として実装いただくため、ログインIDなどを引数として渡すことはできません。※自身のURLスキームを設定することで、ブラウザ起動後すぐにアプリケーションに戻る動作とすることもできますが、URLスキームを指定した場合にはHTMLページを経由しないため、HTML計測タグに対応できず、タグによる計測が必要となった際にアプリの更新が必要となるデメリットがありますので、HTMLページをご用意いただくことを推奨します。