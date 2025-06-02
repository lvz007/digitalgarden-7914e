---
{"dg-publish":true,"permalink":"/ToLearn/test/"}
---


| Just                               | a   | normal       | table |
| ---------------------------------- | --- | ------------ | ----- |
| Use `<` to merge cells to the left | <   | Merged cell! | <     |
| Use `^` to merge cells up          | <   | ^            | ^     |


```sheet
| Just                               | a   | normal       | table |
| ---------------------------------- | --- | ------------ | ----- |
| Use `<` to merge cells to the left | <   | Merged cell! | <     |
| Use `^` to merge cells up          | <   | ^            | ^     |
[**test**]
```


```sheet
{
    classes: { 
        class1: { 
            "color": "cyan",
        },
        class2: {
            backgroundColor: "#555",
        }
    },
}
---
| I                 | -   | have | meta                  | data        | too! |
| ----------------- | --- | ---- | --------------------- | ----------- | ---- |
| group 1           | -   | foo  | bar ~ .class1 .class2 | baz         | test |
| group 2 ~ .class1 | -   | 1    | ^                     | 3 ~ .class2 | 4    |

```

```sheet

{
    classes: {
        c1: {
            "color": "cyan",
        },
        c2: {
            backgroundColor: "#555",
        }
    },
}

--- ~ { color: 'red' }

| I           | ----   | have     | meta                  | data        | too! |
| ------------| ------ | -: ~ .c2 | --------------------- | ----------- | ---- |
| group 1     | ----   | ~~foo~~  | bar ~ .c1 .c2         | $baz$       | test |
| group 2     | - ~.c1 | 1\. test | ^                     | 3 ~ .c2     | 4    |
```

```tx
First Header | Second Header | Third Header |
:----------: | :-----------: | :----------- | 
Content      |   *Long Cell* || 
Content      |    **Cell**   |     Cell     | 
```

```tx
|--|--|--|--|--|--|--|--|
|♜|  |♝|♛|♚|♝|♞|♜|
|  |♟|♟|♟|  |♟|♟|♟|
|♟|  |♞|  |  |  |  |  |
|  |♗|  |  |♟|  |  |  |
|  |  |  |  |♙|  |  |  |
|  |  |  |  |  |♘|  |  |
|♙|♙|♙|♙|  |♙|♙|♙|
|♖|♘|♗|♕|♔|  |  |♖|
```

> [!NOTE]- 标题
> content

>[!info]+ information
>	这里是关于`info`的测试

>[!example] 例子
>例子例子

