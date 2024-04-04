# irb

Interactive Ruby の略
ターミナルにて ruby を起動できる

# 出力

基本は `puts` nil を返す

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