前两天项目上碰到了一个让人头疼的问题，需求是把data的数据赋值给dataCopy，修改dataCopy的时候保证data不变。

但是不论我怎么操作，data都会跟随着dataCopy的变化而变化，自己怎么折腾都解决不了，最后搜索了下，发现是浅拷贝导致的问题。

```javascript
export default {
    data() {
        return {
            data:{},
            dataCopy:{}
        };
    },
    mounted() {
        let obj = {
            name: "张三",
            sex: "男",
            age: 20,
        }
        this.data = obj
        this.dataCopy = this.data
        this.dataCopy.name = "李四"
        console.log(data, dataCopy)
    },
};
```

## 关于浅拷贝和深拷贝

浅拷贝：将A对象赋值给B对象，修改B对象的属性和方法会影响到A对象的属性和方法。

深拷贝：将A对象赋值给B对象，修改B对象的属性和方法不会影响到A对象的属性和方法。

那么为何会有深拷贝和浅拷贝的出现呢？原因就是为了节省内存空间，浅拷贝就是我们的两份数据指向了同一个内存地址，当一个变量修改了内存里面的值之后，另一个变量读取的时候就会发现这个变化，这就是浅拷贝，它大大节省了内存空间。

如果赋值的时候，不是简单的修改指针指向，而是重新创建一个内存区域，那么显然两个变量之间就没有任何关系了，这个时候就是深拷贝。

## 解决方案

如何将浅拷贝转换为深拷贝？简单的办法就是使用js的提供的JSON.parse(JSON.stringify())。经过这样的赋值，就是深拷贝，不会修改原变量。

```javascript
export default {
    data() {
        return {
            data:{},
            dataCopy:{}
        };
    },
    mounted() {
        let obj = {
            name: "张三",
            sex: "男",
            age: 20,
        }
        this.data = obj
        this.dataCopy = JSON.parse(JSON.stringify(this.data))
        this.dataCopy.name = "李四"
        console.log(data, dataCopy)
    },
};
```

## 总结

其实这个深浅拷贝不是vue的问题，是js本身就存在的问题，只不过在vue中，我们习惯了数据绑定，导致这个问题被放大了。所以平时对于数据对象的复制，还是需要考虑一下深浅拷贝的问题的。