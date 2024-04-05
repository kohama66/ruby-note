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
Stringに穴を開ける
`#{name}`
これは、文字列に何かを挿入する際の Rubyでのやり方なのです。

例)
```
puts "Hello #{name}!"
```

### chomp
chompメソッドは文字列オブジェクトの末尾についた改行を取り除き、新しい文字列を返してくれるメソッドです。

### to_iメソッド
to_iメソッドは文字列オブジェクトに対して使用すると数値オブジェクトに変換してくれるメソッドです。
数値以外の文字列オブジェクトに対し、to_iメソッドを使うとどうなるのでしょうか？　
この時数値以外の文字列オブジェクトは全て「0」に変換されます。

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