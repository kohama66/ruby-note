# Ruby
まつもとゆきひろ氏により開発されたプログラミング言語の一つです。

オブジェクト指向の言語である
Rubyは全てのものをオブジェクトとして管理します。
オブジェクトとは何かというと「もの」です。
この「もの」を組み立ててコンピュータに指示を出す言語をオブジェクト指向プログラミング言語と言います。

Rubyはインタプリタ方式の言語であるため実行速度が遅いというデメリットがあります。
インタプリタ方式とはコードを1行ずつ機械語に翻訳して実行する方式のことです。
それに対してコンパイル方式は全てのコードを一度に翻訳してから実行する方式のことを言います。

# irb

Interactive Ruby の略
ターミナルにて ruby を起動できる

rbモードでは外部で定義したメソッドやクラスもそのファイルを読み込むことで使えるようになります。
`load("ruby.rb")`

これで外部で定義したCarクラスがirbモードの中で使用できるようになります。
```
irb(main):001:0> load("classCar.rb")
=> true
irb(main):002:0> car = Car.new("BMW")
=> #&lt;Car:0x00007f809da88020 @name="BMW">
```

irbモードの中でirbコマンドを実行するとサブirbモードになります。
サブirbモード内では通常のirbモードで定義した変数はスコープ外になるので呼び出すことができなくなります。

すでにirbモード内に定義した環境を残したまま、新たな環境でコードを実行したいときなどに便利です。

### getsメソッド
getsメソッドが実行されるとターミナルがコマンド入力待ちの状態に変わります。
ユーザーが何らかの値をキーボードから入力し、エンターを押すとその文字が文字列オブジェクトとしてコンピューターに返ってきます。
また必ず送られてきた文字列オブジェクトの後に改行が入ります。
getsメソッドを使用する時に注意すべき点は必ず文字列オブジエクトとして送られるということです。
つまり数値を入力しても数値オブジェクトにはならないということです。

### 文・式
Perl, PHP, Javaなどでは、式(文)はセミコロン(;)で区切りますが、Ruby では通常改行で区切ります。
```
puts "Hello\n"
puts "World\n"
```
ただし、セミコロン(;)を用いることで、複数の式を1行に記述することもできます。
```
puts "Hello\n"; puts "World\n"
```

式の途中で改行したい場合、バックスラッシュ(\)を用います。
```
ans = 1 + 2 + 3 + \
      4 + 5 + 6
```

# 出力

### puts
基本は `puts` nil を返す

### print
printメソッドはputsメソッド同様、オブジェクトをコンソールに文字列として出力します。
返り値はnilです。
putsメソッドとの違いは改行がつかないことです。

### p
putsメソッドなどに対し、pメソッドは値の型や構造なども確認したい時に使います。
文字列オブジェクトであれば""に囲まれて返ってきますし、数値オブジェクトであれば""に囲まれずに返ってくるので、どんな型のオブジェクトかも確認したい時に便利です。
返り値はオブジェクト自身になります。

# モジュール

`Math`
数学のためのビルトインモジュール(標準で組み込まれているモジュール)

# メソッド

基本形は以下

```
def name
  // 中身
end
```
メソッドが引数を持たない場合、メソッド名の後ろに空のカッコをつけることができますが、 省略しても構いません。


```
def hi(name = "World")
puts "Hello #{name.capitalize}!"
end

=> :hi
hi "chris"
Hello Chris!

=> nil
 hi
Hello World!
=> nil
```
一つはカッコなしでメソッド呼び出しが使われていることです。 何をやっているか明確であれば、カッコは省略できます。 それ以外のトリックは、デフォルト引数のWorldです。 これは、「もしnameが与えられなければ、nameのデフォルト値である"World"を 使う」という定義になります。


# 文字
文字列(String)は、ダブルクォート(")、またはシングルクォート(')で囲みます。
```
str = "Hello world"
str = 'Hello world'
```

"..." の中では ' を、'...' の中では " を使うことができます。"..." の中で " を、'...' の中で ' を使用するには、バックスラッシュ(\)を用いて引用符をエスケープ(無効化)します。

```
str = "He said \"I'll be back.\""
str = 'He said "I\'ll be back."'
```

### エスケープシーケンス(\x)
```
\t : タブ(TAB:0x09)
\v : 垂直タブ(VT:0x0b)
\n : 改行(ラインフィード:LF:0x0a)
\r : キャリッジリターン(CR:0x0d)
\f : フォームフィード(FF:0x0c)
\b : バックスペース(BS:0x08)
\a : ベル(BEL:0x07)
\e : エスケープ(ESC:0x1b)
\s : 空白(SPC:0x20)
\\ : バックスラッシュ(\)
\改行 : 改行(LF:0x0a)
\nnn : 8進表記文字(nは0～7)
\xnn : 16進表記文字(nは0～f)
\unnnn : ユニコード文字nnnn (Ruby 1.9～)
\u{nnnn} : ユニコード文字nnnn (Ruby 1.9～)
\cx : コントロール文字(xはASCII文字)
\C-x : コントロール文字(xはASCII文字)
\M-x : メタ文字(xはASCII文字)
\M-\C-x : メタコントロール
```

### 式展開(#{...})
Stringに穴を開ける
`#{name}`
これは、文字列に何かを挿入する際の Rubyでのやり方なのです。

例)
```
puts "Hello #{name}!"
```

式が変数で、@ や $ で始まる場合は、{ } を省略することができます。
```
puts "My name is #{@name}"
puts "My name is #@name"
```

式展開を抑止するには、# の前にバックスラッシュ(/)を書きます。
`puts "You can use \#{expression} notation in the ruby string."`

### chomp
chompメソッドは文字列オブジェクトの末尾についた改行を取り除き、新しい文字列を返してくれるメソッドです。

### to_iメソッド
to_iメソッドは文字列オブジェクトに対して使用すると数値オブジェクトに変換してくれるメソッドです。
数値以外の文字列オブジェクトに対し、to_iメソッドを使うとどうなるのでしょうか？　
この時数値以外の文字列オブジェクトは全て「0」に変換されます。

# 数値
数値の途中のアンダーバー(_)は無視されます。これは、桁数の多い数値をわかりやすく表現する際に利用されます。
`num = 1_230_000_000       // 1,230,000,000`

# 変数・定数
識別子
変数、定数、クラス名、モジュール名、メソッド名等はすべて 識別子 で識別されます。識別子には、アンダーバー(_)を含む半角英数字を使用できます。ただし、識別子の先頭は数値であってはなりません。大文字・小文字は区別されます。
```
ClassName	クラス名。大文字で始まる。
ModuleName	モジュール名。大文字で始まる。
local_var	ローカル変数。小文字で始まる。
@instans_var	インスタンス変数。@小文字で始まる。
@@instans_var	クラス変数。@@小文字で始まる。
$global_var	グローバル変数。$小文字で始まる。
Const_var	定数。$大文字で始まる。
LABEL	ラベル。先頭は大文字でも小文字でも可。ヒアドキュメントで使用。
```

### グローバル変数($var)
ドル記号($) で始まる変数は「グローバル変数」と呼ばれます。プログラムのどこからでも参照できます。

### 定数(CONST)
大文字で始まる識別子は「定数」と呼ばれます。一度代入すると、再度値を変更することはできません。
クラス内で定義された定数は、クラス名::定数名 で参照されます。

```
class MyClass
  PI = 3.14
end

puts MyClass::PI        # => 3.14
```

クラス外で定義された定数は、暗黙的に Object クラスの定数となります。Object::定数名は、::定数名 とすることもできます。
```
PI = 3.14
puts Object::PI         # => 3.14
puts ::PI               # => 3.14
```

# class
```
irb(main):024:0> class Greeter
irb(main):025:1>   def initialize(name = "World")
irb(main):026:2>     @name = name
irb(main):027:2>   end
irb(main):028:1>   def say_hi
irb(main):029:2>     puts "Hi #{@name}!"
irb(main):030:2>   end
irb(main):031:1>   def say_bye
irb(main):032:2>     puts "Bye #{@name}, come back soon."
irb(main):033:2>   end
irb(main):034:1> end
=> :say_bye
```
これはGreeterという新しいクラスと、 そのクラスのメソッドをいくつか定義しています。また、@nameにも 気づいたかもしれません。これはインスタンス変数で、このクラスにある 全てのメソッドで使うことができます。見ての通り、 say_hi と say_byeで使われています。

```
irb(main):035:0> greeter = Greeter.new("Pat")
=> #<Greeter:0x16cac @name="Pat">
irb(main):036:0> greeter.say_hi
Hi Pat!
=> nil
irb(main):037:0> greeter.say_bye
Bye Pat, come back soon.
=> nil
```
一度greeter オブジェクトを作ると、Patという名前をおぼえてくれます。 ふむ、名前を直接取得しようとするとどうなるでしょう？

```
irb(main):038:0> greeter.@name
SyntaxError: (irb):38: syntax error, unexpected tIVAR, expecting '('
```

おっと、これはできませんでした。

### Class.instance_methods
インスタンスメソッドを確認できる、親やその上の祖先のクラスで定義されたメソッドを含めた、 完全なリストになっている。
定義されたメソッドだけを一覧したいのなら、引数falseを渡します。
`Class.instance_methods(false)` 

```
irb(main):041:0> greeter.respond_to?("name")
=> false
irb(main):042:0> greeter.respond_to?("say_hi")
=> true
irb(main):043:0> greeter.respond_to?("to_s")
=> true
```
上記でインスタンスが持っているかどうかを確認できます。

名前を表示したり変えたりしたい場合はどうでしょう？ Rubyはオブジェクトの変数にアクセスできる簡単な方法を用意しています。
```
class Greeter
attr_accessor :name
end
```

```
irb(main):047:0> greeter = Greeter.new("Andy")
=> #<Greeter:0x3c9b0 @name="Andy">
irb(main):048:0> greeter.respond_to?("name")
=> true
irb(main):049:0> greeter.respond_to?("name=")
=> true
irb(main):050:0> greeter.say_hi
Hi Andy!
=> nil
irb(main):051:0> greeter.name="Betty"
=> "Betty"
irb(main):052:0> greeter
=> #<Greeter:0x3c9b0 @name="Betty">
irb(main):053:0> greeter.name
=> "Betty"
irb(main):054:0> greeter.say_hi
Hi Betty!
=> nil
```
attr_accessorを使うと2つの新しいメソッドが定義されます。 nameは値を参照するメソッドで、name=は値を設定するメソッドです。

### attr_accessor
attr_accessorとは、インスタンス変数の読み取り専用のメソッドと書き込み専用のメソッド(セッター/ゲッター)の両方を定義することが出来るメソッドのことです。
```
# シンボルの場合
attr_accessor :インスタンス変数名

# 文字列の場合
attr_accessor 'インスタンス変数名'

# @ageの読み取り専用メソッド(参照可能になる)
def age
  @age
end

# @ageの書き込み専用メソッド(変更可能になる)
def age=(age)
  @age = age
end
```

### attr_reader
ゲッターメソッド

### attr_writer
セッターメソッド

上記をまとめたものが attr_accessor

### Railsのアクセサメソッド
Railsを触っている人は、「確かアクセサメソッドを定義していなくてもクラスのインスタンス変数に外部からのアクセスが出来たよな？」と感じた方がいると思います。

Railsでは、AcriveRecodeを継承したクラスのインスタンスは、テーブルに定義したカラムに対応するアクセサメソッドが自動的に定義されます。その為、特に意識する事なくインスタンス変数にアクセス出来てしまいます。

しかし、テーブルに定義したカラム以外に値を持たせたい場合にattr_accessorメソッドを使用する事が多いです。

### クラスメソッドの定義
インスタンスメソッドは、インスタンスから呼び出すことが出来ましたが、その他にもクラスから呼び出すことが出来るクラスメソッドがあります。
クラスメソッドとは、インスタンスに依存せずにクラス本体に紐づけられるメソッドのことです。
```
# クラスメソッドの定義方法1
class クラス名
  def self.クラスメソッド名
  end
end

# クラスメソッドの定義方法2
class クラス名  
  # この中で定義するとクラスメソッドと認識される
  class << self
    # メソッド名にselfは必要ない
    def test
    end
  end
end
```

### クラス変数
インスタンス変数の他に、クラス変数という@が２つ付く変数があります。
インスタンス変数が作成された各インスタンスごとに共有される変数だったのに対して、クラス変数は、全てのインスタンスで共有される変数です。
```
# たい焼きの設計図を作成
class Taiyaki

  # 全てのインスタンスで共有されるクラス変数
   @@total_taiyaki_count = 0

  # インスタンス作成の時に実行される
  def initialize(taste, price)
    @taste = taste
    @price = price

    # インスタンスが作成(new)される毎にカウントアップ
    @@total_taiyaki_count += 1
  end

  # インスタンスメソッド
  def show_info
      puts "#{@taste}味のたい焼きは#{@price}円です。"
  end

  # クラスメソッド
   def self.show_all_count
     puts "たい焼きは全部で#{@@total_taiyaki_count}個作成されました。"
   end

end
```

# インスタンス
インスタンスは、以下のようにクラスから作成します。
`クラス名.new`

### initailzeメソッドとインスタンス変数
引数で渡された値は、インスタンス作成時に実行されるinitializeメソッドを利用して「@がついたインスタンス変数」に代入します。
```
class Taiyaki
  # インスタンス作成の時に実行される
  def initialize(taste, price)
    # インスタンス変数には@をつける
    @taste = taste
    @price = price
  end
end

# newした際にinitializeメソッドが実行され、引数の値がインスタンス変数に代入される
anko_taiyaki = Taiyaki.new("あんこ", 250)
#=> <Taiyaki:0x007fd9489cdb18 @taste="あんこ", @price=250>
```

### インスタンスメソッド
インスタンスメソッドとは、作成したインスタンスから実行出来るメソッドのことです。

# オブジェクト
Rubyのプログラミングで使用する文字や数字などのデータやメソッドはオブジェクトという形でデータ化されます。

Rubyのオブジェクトは必ず何らかのクラスのインスタンスです。
オブジェクトには様々な種類があります。
```
文字列	Stringクラス
整数	Integerクラス
時刻	Timeクラス
日付	Dateクラス
ハッシュ	Hashクラス
```

# サイクルとループ - 別名: イテレーション
```
@names.each do |name|
  puts "Hello #{name}!"
end
```

```
# Say bye to everybody
def say_bye
  if @names.nil?
    puts "..."
  elsif @names.respond_to?("join")
    # Join the list elements with commas
    puts "Goodbye #{@names.join(", ")}.  Come back soon!"
  else
    puts "Goodbye #{@names}.  Come back soon!"
  end
```
say_byeメソッドはeachを使いません。その代わり、@namesがjoinメソッドを 処理できるかをチェックしています。もし処理できることがわかれば、それを使います。 そうでなければ、変数の値を文字列として出力します。 このメソッドは実際の変数の型を意識せず、サポートしているメソッドに頼っています。 これは“Duck Typing”という名前で知られている、「もしアヒルのように歩き、 アヒルのように鳴くものは……」というものです。この方法の良いところは、 対応する変数の型に不要な制約を課さずにすむことです。 もし誰かが新たな種類のリストクラスを持ち出してくれば、 joinメソッドが他のリストと同様の意味を持っている限り、 すべては期待した通り動きます。

# スクリプトの実行
`if __FILE__ == $0`
__FILE__ は現在のファイル名を返す特別な変数です。 $0はプログラムを実行するときに使われるファイル名です。 このチェックは、「もしこれがメインファイルとして実行されているならば……」 という意味になります。 これは、ライブラリとして使われる場合には実行されないけれど、 実行ファイルとして使われる場合には実行されるコードを書くために 使われます。

例)
```
if __FILE__ == $0
  mg = MegaGreeter.new
  mg.say_hi
  mg.say_bye

  # Change name to be "Zeke"
  mg.names = "Zeke"
  mg.say_hi
  mg.say_bye

  # Change the name to an array of names
  mg.names = ["Albert", "Brenda", "Charles",
              "Dave", "Engelbert"]
  mg.say_hi
  mg.say_bye

  # Change to nil
  mg.names = nil
  mg.say_hi
  mg.say_bye
end
```

# Array
配列とは、複数のデータを格納することが出来るArrayクラスのオブジェクトのことです。

### 要素の取り出し方
配列の各要素を取得するには、下記のように[]と添字(インデックス)を指定します。
また、存在しない要素を指定しても、特にエラーは出ないでnilが返ります。

### 要素を追加する方法
配列に要素を追加するには、下記の様に<<演算子を使う事で、配列の末尾に要素を追加する事が出来ます。
一度に複数の要素を追加する時は、pushメソッドを使います。pushメソッドは、配列の末尾に引数で指定した要素を追加します。
`fruits.push("Peach", "Pear") # fruitsにPeachとPearを追加`

pushメソッドは要素を追加していましたが、別の配列の要素を追加したい場合は、「+=演算子」を使います。
`fruits += %w(Peach Pear)`
上記の%w()は、要素が文字列の配列を作成します。
先頭に追加したい場合はunshiftメソッドを使います。

### 要素を削除する方法
配列の特定の要素を削除するには、下記の様に「delete_atメソッド」を使います。delete_atメソッドの戻り値は、削除した値になります。
また、存在しない添字を指定するとnilが返ってきます。

### 二次元配列とは？
以下のように、配列の中に要素として配列が格納された形を二次元配列(多次元)と言います。先ほどまでの要素が特に配列などで入れ子になっていない配列が一次元配列です。
```
irb(main):016:0> foods = ["Strawberry", ["Carrot", "Onion"], "Meat"]
=> ["Strawberry", ["Carrot", "Onion"], "Meat"]
```

### 多重代入と配列
多重代入とは、下記の様に変数の代入を複数にまとめることでしたが、配列を使っても多重代入をする事が出来ます。

```
irb | 多重代入の使用例
irb(main):001:0> a, b = 6, 10
=> [6, 10]
irb(main):002:0> a
=> 6
irb(main):003:0> b
=> 10
```

配列を使って多重代入をしてみよう
先ほどのa,bに対して6,10を代入していましたが、これを配列を使って多重代入すると下記の様になります。

```
irb | 配列を使った多重代入
irb(main):004:0> a, b = [6, 10]
=> [6, 10]
irb(main):005:0> a
=> 6
irb(main):006:0> b
=> 10
```

# Hash
ハッシュとは、キーと値の組み合わせをセットにして複数のデータを管理することが出来る便利なオブジェクトのことです。
他の言語では連想配列やマップと呼ばれる場合があります

例)
```
fruits = { "Apple" => "150円", "Orange" => "100円", "Melon" => "600円", "Grape" => "700円" }
=> {"Apple"=>"150円", "Orange"=>"100円", "Melon"=>"600円", "Grape"=>"700円"}

fruits["Apple"] = "180円"
```

ハッシュは、{}を使って定義します。
```
# 空のハッシュを定義
 {}

# キーと値の組み合わせを３つの格納するハッシュ
{ "キー1" => "値１", "キー2" => "値2", "キー3" => "値3" }

# 変数aに３つのキーと値の組み合わせが格納されたハッシュを代入する
a = { "キー1" => "値１", "キー2" => "値2", "キー3" => "値3" }
```

メソッドの第一引数がハッシュかつ、()を省略してメソッドを呼び出す場合、Rubyがハッシュの{}ではなく、ブロックの{}と解釈してエラーが出てしまいます。
```
# サンプルコードでエラーを検証
def buy_ice(options={}, menu)
  puts options
end

# ()を省略してbuy_iceメソッドを呼び出すと、ハッシュの{}がブロックの{}と解釈されるのでエラーが起こる
buy_ice {'Strawberry' => true, 'Chocolate' => true}, 'ice'

SyntaxError (syntax error, unexpected =>, expecting '}')
```

メソッド引数の第一引数がハッシュの場合は、()をつけてメソッドを呼び出す事でブロックの{}だと解釈されずにメソッドを呼び出す事ができます。
()を省略せずにメソッドを呼び出すとエラーは起こらない
```
buy_ice( { 'Strawberry' => true, 'Chocolate' => true }, 'ice')
{"Strawberry"=>true, "Chocolate"=>true}
=> nil
```

メソッドの第二引数がハッシュの場合は、()を省略してメソッドを呼び出す事ができます。その際、下記のコードの様にハッシュの{}も 省略する事が出来ます。
```
# 第二引数がハッシュの場合
def buy_ice(menu, options={})
  puts options
end

# メソッド呼び出し時に{}も省略する事が出来る
buy_ice 'ice', 'Strawberry' => true, 'Chocolate' => true 
{"Strawberry"=>true, "Chocolate"=>true}
=> nil
```

### 要素の取得方法
要素を取得するには、下記の様な構文になります。
ハッシュは、大量のキーと値が格納されていてもハッシュの内部構造によって高速に指定したキーの値を取得する事が可能です。

### ハッシュの要素数を調べる方法
ハッシュの要素数を調べるには、sizeメソッドを使います。(エイリアスはlengthメソッド)

### 要素を削除する方法
ハッシュの要素を削除するには、deleteメソッドを使います。指定したキーに対応する要素を削除します。
指定したキーがない場合はnilが返ります。

### ハッシュを使った繰り返し処理
ハッシュはeachメソッドを使うと、キーと値を順番に取得する事が出来ます。配列の時とは違いブロック引数がキーと値の２種類になっているので注意してください。
```
# fruitsに格納されている順番にkey, valueにそれぞれキーと値を渡してブロック内の処理を実行させている
fruits.each do | key, value |
  puts "#{key}は、#{value}"
end

Orangeは、100円
Melonは、600円
Grapeは、700円
Strawberryは、600円
=> {"Orange"=>"100円", "Melon"=>"600円", "Grape"=>"700円", "Strawberry"=>"600円"}
```

ブロックに渡した引数は「key, value」の2個でしたが、引数を1個だけにすると、キーと値が配列に格納されます。
```
# ブロックに渡す引数を１つにすると配列に格納される
fruits.each do | key_value |
  puts "#{key_value}"
end

# キーと値はそれぞれ添字0,1に格納される
["Orange", "100円"]
["Melon", "600円"]
["Grape", "700円"]
["Strawberry", "600円"]
=> {"Orange"=>"100円", "Melon"=>"600円", "Grape"=>"700円", "Strawberry"=>"600円"}

# キーと値をブロック内で使うには、配列から取り出す処理を追加
fruits.each do | key_value |
  key = key_value[0]
  value = key_value[1]
  puts "#{key}は#{value}"
end

Orangeは100円
Melonは600円
Grapeは700円
Strawberryは600円
=> {"Orange"=>"100円", "Melon"=>"600円", "Grape"=>"700円", "Strawberry"=>"600円"}
```

ハッシュの各要素について処理を繰り返すには、each_key, each_value, each_pair を使用します。処理される順番は不同となります。

### ハッシュとシンボル
現在ハッシュのキーには文字列を使っていますが、シンボルを使うことが推奨されています。まずは文字列とシンボルの違いについて理解していきましょう。

### シンボルとは？
シンボルとは、コロン(:)を使って任意の名前を定義します。シンボルは、シンボルクラスのオブジェクトです。

```
:シンボルの名前

# シンボルの例
:name

# シンボルクラスのオブジェクト
:name.class
=> Symbol
```

シンボルと文字列の違いとは？
シンボルはSymbolクラスのオブジェクトで、文字列はStringクラスのオブジェクトです。

シンボルは表面的には文字列と似ていますが、シンボルの中身は文字列とは違い整数で管理されています。その為、文字列よりも高速に処理出来ます。

シンボルは、「同じシンボルであれば同じオブジェクト」という特徴があります。実際に、オブジェクトのidを調べる「object_idメソッド」を使って見ていきましょう。
```
# 文字列は、同じ文字列でもオブジェクトidが違う
'pikawaka'.object_id => 70151245202480
'pikawaka'.object_id => 70151245128760
'pikawaka'.object_id => 70151248681680

# シンボルは同じシンボルであればオブジェクトidが同じ
:pikawaka.object_id => 1310428
:pikawaka.object_id => 1310428
:pikawaka.object_id => 1310428
```

同じシンボルが同じオブジェクトである事は、メモリの使用率などが良くなり文字列よりも処理の速度が上がります。これはハッシュのキーにも当てはまります。
また、シンボルの特徴にイミュータブルで文字列の様に破壊的な変更は出来ない為、変更されては困るものに使う事が出来ます。

### ハッシュのキーにシンボルを使う
シンボルをハッシュのキーに使うことによって、文字列よりも高速に値を取り出したり、イミュータブルで破壊的な変更がされないのでハッシュのキーを勝手に変更される事がありません。

ハッシュのキーには文字列ではなく、シンボルを使う様にしましょう。
```
# 文字列をハッシュのキーにした場合
fruits = { "Apple" => "150円", "Orange" => "100円", "Melon" => "600円", "Grape" => "700円" }

# 文字列でハッシュを取り出す
fruits[ "Apple"]

# シンボルをハッシュのキーにする場合
fruits = { :Apple => "150円", :Orange => "100円", :Melon => "600円", :Grape => "700円" }

# シンボルでハッシュを取り出す
fruits[:Apple]
=> "150円"
```

現在ハッシュロケット(=>)を使っていますが、キーをシンボルにした場合は、ハッシュロケットを省略する事ができます。

シンボルのコロンの位置が左から右に変わるので注意してください。
ハッシュロケット(=>)は、Ruby1.8以前でハッシュを生成する際に使われていた記法なので、シンボルを使う際は上記の様な書き方にしましょう。
```
# ハッシュロケットがある場合
fruits = { :Apple => "150円", :Orange => "100円", :Melon => "600円", :Grape => "700円" }

# ハッシュロケットを省略する場合、コロンの位置を左から右に変更する
fruits = { Apple: "150円", Orange: "100円", Melon: "600円", Grape: "700 円" }
=> {:Apple=>"150円", :Orange=>"100円", :Melon=>"600円", :Grape=>"700円"}
```

シンボルは、ハイフンが入ってるとsyntax errorになる場合があります。ハイフンを使う場合は、下記の様に指定してあげる事でハッシュロケットを省略しながらシンボルを使う事が出来ます。

```
# ハイフンが入っていると下記の指定だとエラーが起こる
{ hoge-hoge: 1 }
syntax error, unexpected ':', expecting =>

# Ruby2.2ではシングルクォートかダブルクォートで囲って使う事が出来る
{ 'hoge-hoge': 1 }
=> {:"hoge-hoge"=>1}
```

# もし～ならば(if, then, else, elsif)
```
if expr [then]
  expression...
[elsif expr [then]
  expression...]...
[else
  expression...]
end
```

then は省略可能です。
PHP などでは数値の 0 や空文字列も偽とみなされますが、Ruby では false および nil のみが偽と判断され、0 や空文字を含むその他の値は真とみなされます。

# もし～でなければ(unless, then)
unless は「もし～でなければ」を意味します。下記の例では、num が 10 より小さくなければ、BIG を表示します。then は省略可能です。
```
unless num < 10 then
  puts "BIG"
end
```

# ～のあいだ(while, do)
```
while expr [do]
  expression...
end
```
while は「～のあいだ」を意味します。下記の例では、i の値が 10よりも小さい間 i の値を表示します。do は省略可能です。
```
i = 0
while i < 10 do
  puts i
  i += 1
end
```

# ～になるまでのあいだ(until, do)
until は「～になるまでのあいだ」を意味します。下記の例では、i の値が 10よりも大きくなるまでの間 i の値を表示します。do は省略可能です
```
i = 0
until i > 10 do
  puts i
  i += 1
end
```

# ～のあいだ(for, in, do)
```
for var[, var]... in expr [do]
  expression...
end
```
for は配列の各要素に対して処理を繰り返します。do は省略可能です。

```
for i in [1, 2, 3] do
  puts i                  #=> 1, 2, 3
end

for i in 1..10 do
  puts i                  #=> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
end
```

ただし、Ruby では for 文を使用することはあまりなく、下記の様なイテレータを使用するのが一般的です。
```
10.times do |i|
  puts i
end
```

# ～の場合(case, when)
case, when, else は、値によって処理を振り分けます。次の例では、num の値が 1～3 の場合は SMALL、4～6 の場合は NORMAL、その他の場合は BIG を表示します。then は省略可能です。
```
num = 4
case num
when 1..3 then
  puts "SMALL"
when 4..6 then
  puts "NORMAL"
else
  puts "BIG"
end
```

# ループを抜ける(break)
break は最も内側の while, until, for などのループ処理を抜けます。下記の例では、i が 5の時に forループを抜けます。
```
for i in 1..10
  if i == 5 then
    break
  end
  puts i                 #=> 1, 2, 3, 4
end
```

# ループを繰り返す(next)
next は while, until, for などのループ処理において、残りの処理をスキップして次のループを始めます。次の例では、i が 5の時のみ、puts を実行しません。
```
for i in 1..10
  if i == 5 then
    next
  end
  puts i              #=> 1, 2, 3, 4, 6, 7, 8, 9, 10
end
```

# ループを繰り返す(redo)
redo も next と同様、ループを繰り返しますが、next がループの終了判断を行ってから処理を行うのに対し、redo は終了判断無しで処理を繰り返します。

```
i = 0
while i < 5 do
  i += 1
  if i == 5 then
    redo
  end
  puts i              #=> 1, 2, 3, 4, 6
end
```