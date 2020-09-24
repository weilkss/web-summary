# web 前端面试题

想进大厂？首先基础得扎实，技术面试得过，你才能有机会和 hr 小姐姐谈工资

## 算法篇

### 1. 验证一个数是否是素数

> 如果这个数是 2 或 3，一定是素数;如果是偶数，一定不是素数;如果这个数不能被 3~它的平方根中的任一数整除，m 必定是素数。而且除数可以每次递增 2(排除偶数)

```js
function isPrime(num) {
  if (num === 2 || num === 3) {
    return true;
  }

  if (num % 2 === 0) {
    return false;
  }

  let divisor = 3,
    limit = Math.sqrt(num);

  while (limit >= divisor) {
    if (num % divisor === 0) {
      return false;
    } else {
      divisor += 2;
    }
  }

  return true;
}

isPrime(30); // false
```

### 2. 斐波那契

- 用递归做

```js
function fibonacci(n) {
  if (n <= 0) {
    return 0;
  }

  if (n == 0) {
    return 1;
  }

  return fibonacci(n - 1) + fibonacci(n - 2);
}
console.log(fibonacci(10));
```

- 用循环做

```js
function fibonacci(n) {
  var n1 = 1,
    n2 = 1,
    sum;
  for (let i = 2; i < n; i++) {
    sum = n1 + n2;
    n1 = n2;
    n2 = sum;
  }
  return sum;
}
console.log(fibonacci(10));
```

### 3. 求最大公约数

```js
function greatestCommonDivisor(a, b) {
  if (b === 0) {
    return a;
  } else {
    let c = a % b;
    a = b;
    b = c;
    return greatestCommonDivisor(a, b);
  }
}
```

### 4. 数组去重

```js
function removeDuplicate(arr) {
  if (arr === null || arr.length < 2) {
    return arr;
  }

  let res = [],
    exits = [];

  for (let i = 0; i < arr.length; i++) {
    let j = arr[i];

    while (!exits[j]) {
      res.push(arr[i]);

      exits[j] = true;
    }
  }

  return res;
}
```

### 5. 冒泡排序

```js
function arrSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

### 6. 删除重复的字符

```js
function dropRepeat(str) {
  let result = [];
  let hash = {};
  for (let i = 0, elem; i < str.length; i++) {
    elem = str[i];
    if (!hash[elem]) {
      hash[elem] = true;
      result = result + elem;
    }
  }
  return result;
}
```

### 7. 排序两个已经排好序的数组

```js
function mergeSortedArr(a, b) {
  if (!a || !b) {
    return;
  }

  let aEle = a[0],
    bEle = b[0],
    i = 1,
    j = 1,
    res = [];

  while (aEle || bEle) {
    if ((aEle && !bEle) || aEle <= bEle) {
      res.push(aEle);

      aEle = a[i++];
    } else {
      res.push(bEle);

      bEle = b[j++];
    }
  }

  return res;
}
```

### 8. 字符串反向

```js
function reverse(str) {
  let resStr = '';

  for (let i = str.length - 1; i >= 0; i--) {
    resStr += str[i];
  }

  return resStr;
}
```

### 9. 字符串原位反转

```js
function reverseInPlace(str) {
  return str.split(' ').reverse().join(' ').split('').reverse().join('');
}
```

### 10. 判断是否是回文

```js
function isPalindrome(str) {
  if (!str || str.length < 2) {
    return;
  }

  for (let i = 0; i < str.length / 2; i++) {
    if (str[i] !== str[str.length - 1 - i]) {
      return false;
    }
  }

  return true;
}
```

### 11. 判断数组中是否有两数之和

```js
function sumFind(arr, num) {
  if (!arr || arr.length < 2) {
    return;
  }

  let differ = {};

  for (let i = 0; i < arr.length; i++) {
    let subStract = num - arr[i];

    if (differ[subStract]) {
      return true;
    } else {
      differ[arr[i]] = true;
    }
  }

  return false;
}
```

### 12. 连字符转成驼峰

```js
function transHump(str, sym) {
  if (!sym) {
    sym = '-';
  }

  let arr = str.split(sym);

  for (let i = 1; i < arr.length; i++) {
    arr[i] = arr[i].charAt(0).toUpperCase() + arr[i].substring(1);
  }

  return arr.join('');
}
```

### 13. 用正则实现 trim() 清除字符串两端空格

```js
String.prototype.myTrim = function () {
  // return this.replace(/\s*/g,""); // 清除所有空格
  return this.replace(/(^\s*)|(\s*$)/g, ''); // 清除字符串前后的空格
};
```

### 14. 将数字 12345678 转化成 RMB 形式：12,345,678

- 正则处理

```js
function formatCash(str) {
  if (typeof str === 'number') {
    str = String(str);
  }
  return str.replace(/\B(?=(\d{3})+(?!\d))/g, ',');
}
```

- js 实现

```js
function formatCash(str) {
  if (typeof str === 'number') {
    str = String(str);
  }
  return str
    .split('')
    .reverse()
    .reduce((prev, next, index) => {
      return (index % 3 ? next : next + ',') + prev;
    });
}
```

### 15. 删除相邻相同的字符串

```js
function delSrt(str) {
  let res = [],
    nowStr;

  for (let i = 0; i < str.length; i++) {
    if (str.charAt(i) != nowStr) {
      res.push(str.charAt(i));
      nowStr = str.charAt(i);
    }
  }

  return res.join('');
}
```

## 更多面试题

- [常见 css 的面试题](./css.md)
- [常见 html 的面试题](./html.md)
- [常见 javascript 的面试题](./javascript.md)
- [常见 typescript 的面试题](./typescript.md)
- [常见 vue 的面试题](./vue.md)
- [常见 react 的面试题](./react.md)
- [常见 webpack 的面试题](./webpack.md)
- [常见 node 的面试题](./node.md)
- [前端工程化](./eng.md)
- [优化相关](./optimize.md)
