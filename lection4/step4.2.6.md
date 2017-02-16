**Problem:**

В одном из прошлых заданий мы встречали тип `Result` и функцию `doSomeWork`:

```haskell
data Result = Fail | Success

doSomeWork :: SomeData -> (Result,Int)
```

Функция `doSomeWork` возвращала результат своей работы и либо код ошибки в случае неудачи, либо `0` в случае успеха. Такое определение функции не является наилучшим, так как в случае успеха мы вынуждены возвращать некоторое значение, которое не несет никакой смысловой нагрузки.

Используя функцию `doSomeWork`, определите функцию doSomeWork' так, чтобы она возвращала код ошибки только в случае неудачи. Для этого необходимо определить тип `Result'`. Кроме того, определите instance `Show` для `Result'` так, чтобы show возвращал `"Success"` в случае успеха и `"Fail: N"` в случае неудачи, где `N` — код ошибки.



**Answer:**


```haskell
data Result' = Fail' Int | Success'

instance Show Result' where
    show Success' = "Success"
    show (Fail' errNum) = "Fail: " ++ show errNum

doSomeWork' :: SomeData -> Result'
doSomeWork' d = case doSomeWork d of
    (Success, _) -> Success'
    (_, errNum) -> Fail' errNum
```