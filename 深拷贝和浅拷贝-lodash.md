## 深拷贝与浅拷贝的区别，实现深拷贝的几种方法

**就是假设B复制了A，当修改A时，看B是否会发生变化，如果B也跟着变了，说明这是浅拷贝，拿人手短，如果B没变**

- 基本数据类型有哪些，**number，string，boolean，null，undefined，symbol**以及未来ES10新增的**BigInt**(任意精度整数)七类。

- 引用数据类型(Object类)有常规名值对的无序对象{a:1}，数组[1,2,3]，以及函数等。

**a.基本类型--名值存储在栈内存中**，例如let a=1;

![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124130901890-511917244.jpg)

当你b=a复制时，栈内存会新开辟一个内存，例如这样：

​                                                                        ![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124131822437-430949998.jpg)

##### 所以当你此时修改a=2，对b并不会造成影响，因为此时的b已自食其力，翅膀硬了，不受a的影响了。当然，let a=1,b=a;虽然b不受a影响，但这也算不上深拷贝，因为深拷贝本身只针对较为复杂的object类型数据。

**b.引用数据类型--名存在栈内存中，值存在于堆内存中，但是栈内存会提供一个引用的地址指向堆内存中的值**，我们以上面浅拷贝的例子画个图：

![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124133428359-1292133331.jpg)

当b=a进行拷贝时，其实复制的是a的引用地址，而并非堆里面的值。

![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124133647796-1390255671.jpg)

而当我们**a[0]=1**时进行数组修改时，由于a与b指向的是同一个地址，所以自然b也受了影响，这就是所谓的浅拷贝了。

​                                   ![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124133934328-67216865.jpg)

那，要是在堆内存中也开辟一个新的内存专门为b存放值，就像基本类型那样，岂不就达到深拷贝的效果了

![img](https://images2018.cnblogs.com/blog/1213309/201711/1213309-20171124140906203-2099568933.jpg)

### **深拷贝，是拷贝对象各个层级的属性**

```js
let a=[1,2,3,4],
    b=a.slice();
```

```js
let a=[0,1,[2,3],4],
        b=a.slice();
a[0]=1;
a[2][0]=1;
console.log(a,b);
```

b对象的一级属性确实不受影响了，但是二级属性还是没能拷贝成功，仍然脱离不了a的控制，说明slice根本不是真正的深拷贝。

concat方法与slice也存在这样的情况，他们都不是真正的深拷贝，这里需要注意。

#### JSON.stringify与JSON.parse实现深拷贝

```js
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
}  
```

#### lodash的deepClone 深拷贝

```js
let a=[0,1,[2,3],4],
    b=deepClone(a);
```

### **JQ的extend方法**

**$.extend( [deep ], target, object1 [, objectN ] )**

**deep**表示是否深拷贝，为true为深拷贝，为false，则为浅拷贝

**target** **Object**类型 目标对象，其他对象的成员属性将被附加到该对象上。

**object1  objectN**可选。 Object类型 第一个以及第N个被合并的对象。 

```js
let a=[0,1,[2,3],4],
    b=$.extend(true,[],a);
```

## 浅拷贝

#### object.assign (obj, obj1)

#### Array.slice() 不传参数

#### 在实际开发中也是非常有用的。例如后台返回了一堆数据，你需要对这堆数据做操作，但多人开发情况下，你是没办法明确这堆数据是否有其它功能也需要使用，直接修改可能会造成隐性问题，深拷贝能帮你更安全安心的去操作数据，根据实际情况来使用深拷贝

# lodash

#### javascript库

提供了很多内置对象没有的方法功能的扩展

lodash通常用（_）下划线来表示

$ jequery

##### _clone(value) 浅拷贝

##### _cloneDeep(value) 深拷贝

##### _isEqual(value, other)  执行深比较确定两者的值是否相等

##### _.now() 返回时间戳 1970年到现在的毫秒数