# Swift2.0まとめ

#### 日本の現地時間の表示

ソース

```swift
let dateFormatter = NSDateFormatter()                       // フォーマットの取得
dateFormatter.locale = NSLocale(localeIdentifier: "ja_JP")  // JPロケール
dateFormatter.dateFormat = "yyyy/MM/dd HH:mm:ss"            // フォーマットの指定
print(dateFormatter.stringFromDate(NSDate()))               // 現在日時
```

実行結果
>2015/10/04 11:53:40
>Program ended with exit code: 0

#### 関数返却関数
```swift
func priceFunc(age age:Int) -> (Int) -> Int {
    //for child function
    func kidsPrice(kosu kosu: Int) -> Int {
        return 400 * kosu
    }
    //for adult function
    func adultPrice(kosu kosu:Int) -> Int {
        return 600 * kosu
    }
    if age < 12 {
        return kidsPrice
    } else {
        return adultPrice
    }
}
let age10Func = priceFunc(age: 10)
let price = age10Func(2)
print(price)
let age20Func = priceFunc(age: 20)
let price2 = age20Func(2)
print(price2)
```

#### クロージャ

* __Mapメソッド (写像関数)__
```swift
let numbers = [4,7,2,9]
let array1 = numbers.map({ (v:Int) -> Int in
    return v*2
})
//こうもかける
let array2 = numbers.map({ v in return v*2 }) //推論で、型を省略
let array3 = numbers.map{ v in return v*2 } //クロージャが１つの場合、外だしできる
let array4 = numbers.map{ return $0*2 } //クロージャの引数は$0,$1,$2...で参照
print(array1,array2,array3,array4)
```
実行結果
>[8, 14, 4, 18] [8, 14, 4, 18] [8, 14, 4, 18] [8, 14, 4, 18]
>Program ended with exit code: 0

* __sortメソッド__
```swift
let stringArray = ["orange", "Apple", "lemon", "Peach"]
let sortedStringArray = stringArray.sort{ $0.uppercaseString < $1.uppercaseString }
print(sortedStringArray)
```
実行結果
>["Apple", "lemon", "orange", "Peach"]
>Program ended with exit code: 0

* __クロージャを引数にする自作関数の例__
```swift
//自作クロージャを引数に持つ関数
func show(a:Int,b:Int,c:Int, execfunc :(Int,Int,Int) -> Int){
    print(execfunc(a,b,c))
}
func calc(a:Int, b:Int, c:Int) -> Int {
    return a + b + c
}
//関数をそのまま渡す
show(1, b: 2, c: 3, execfunc: calc)
//クロージャを渡す
show(1, b: 2, c: 3, execfunc: {(a:Int, b:Int, c:Int) -> Int in
    return a + b + c
})
//返却値を推論して省略
show(1, b: 2, c: 3, execfunc: {(a:Int, b:Int, c:Int)  in
    return a + b + c
})
//引数型も推論して省略
show(1, b: 2, c: 3, execfunc: {(a,b,c)  in
    return a + b + c
})
//クロージャが一つのため、外だしできる
show(1, b: 2, c: 3){(a,b,c) in
    return a + b + c
}
//引数は$0,$1,$2...で取得できる
show(1, b: 2, c: 3){ $0 + $1 + $2 }
```
実行結果
>6
>6
>6
>6
>6
>6
>Program ended with exit code: 0

* __引数なし、Void返却型のクロージャの書き方__
```swift
//void argument and void return value type closure
//case1
var voidFunc = { () -> Void in
    print("void: case1")
}
voidFunc()
//case2
voidFunc = {() -> () in
    print("void: case2")
}
voidFunc()
//case3
voidFunc = {print("void: case3")}
voidFunc()
```
実行結果
>void: case1
>void: case2
>void: case3
>Program ended with exit code: 0
