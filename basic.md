### 基礎問題
- Kotlin 檔案的副檔名為 ＿？
- `val` 和 `var` 的不同
- `print` 和 `println` 有什麼不同？
- `for (i in 1..10) print(i)` 會印出？
- `for (i in 1 until 10) print(i)` 會印出？
- `for (i in 1..10 step 2) print(i)` 會印出？
- `for (i in 10 downTo 1) print(i)` 會印出？

### 進階語法問題
- `typealias NodeSet = Set<Network.Node>` 這段程式要達成的效果是什麼？
- 


### 物件
- `data class` 是什麼？宣告之後在 Kotlin 內產生什麼作用
- `companion object` 是什麼意思？
- 宣告 singleton 時需要使用的關鍵字是什麼？

### 函數
- scope function 是哪五個
- `tailrec` 關鍵字是什麼意思？在 Kotlin 內如何使用？
- `inline fun` 關鍵字是什麼意思？在 Kotlin 內如何使用？

### lambda
- `var block: (Int) -> String` 宣告內 `block` 的型態是什麼？

### Collections

```kotlin
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
    .filter { it.startsWith("a") }
    .sortedBy { it }
    .map { it.uppercase() }
    .forEach { println(it) }
```

會印出什麼內容？

`listOf(3.14F, 2)` 的型態為？

`listOf("a", 2)` 的型態為？

### Coroutine
- launch 和 async 有什麼不同 

### 後端開發
- 舉出一個可用 Kotlin 寫後端的框架
- 

