# 排序

## 快速排序

### 解法一
单独开辟两个存储空间 left 和 right 来存储每次递归比 target 小和大的序列，每次递归直接返回 left、target、right 拼接后的数组。
浪费大量存储空间，写法简单
```js
function quickSort (array) {
  if (array.length < 2) return array
  const target = array[0]
  const left = []
  const right = []
  for (let i = 1; i <array.length;i++) {
    if (array[i] < target) {
      left.push(array[i])
    } else {
      right.push(array[i])
    }
  }

  return quickSort(left).concat([target], quickSort(right))
}
```

### 解法二
记录一个索引 l 从数组最左侧开始，记录一个索引 r 从数组右侧开始
在 l < r 的条件下，找到右侧小于 target 的值 array[r]，并将其赋值到 array[l]
在 l < r 的条件下，找到左侧大于 target 的值 array[l],并将其赋值到 array[r]
这样让 l = r 时，左侧的值全部小于 target ，右侧的值全部小于 target , 将 target 放到 该位置
```js
function quickSort (array, start, end) {
  if (end - start <1) return
  const target = array[start]
  let l = start
  let r = end

  while (l < r) {
    while (l < r && array[r] >= target) {
      r--
    }
    array[l] = array[r]
    while (l < r && array[l] < target) {
      l++
    }
    array[r] = array[l]
  }
  array[l] = target
  quickSort(array, start, l - 1)
  quickSort(array, l + 1, end)
  return array
}
```