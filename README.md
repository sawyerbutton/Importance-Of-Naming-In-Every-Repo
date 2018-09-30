# ImportanceOfNamingInEveryRepo

## 命名和项目代码一样重要

> 对于一个项目来说,代码固然是非常重要的部分,代码承载了业务逻辑,承载了系统设计,没有代码,你甚至无法传达开发者的设计理念和思想。
> 只是仅仅拥有代码对一个项目来说是完全不够的,良好的命名规则同样占据了和代码本身一样的地位。
> 混乱,错误,毫无规则的命名规则不仅让代码难以理解,更有可能在撰写代码和后期维护中曲解代码本身的含义。
> 良好的命名规则却可以让代码通俗易懂,更准确和快速地向开发者传达代码所代表的事物和逻辑本质,极大地增强了代码的可维护性
> 命名规则和代码对于一个项目而言是一样重要的

## 良好的命名规则会帮助我们修正可能存在的错误

> 当使用良好标准的命名习惯时,开发者会更加严格地对待每一个概念的名称,会思考这个名称所表达的概念是否正确,该名称是否正确表达了事物的本质或是否正确反映了某个行为的逻辑
> 比如：已经编写完的代码中有一些命名不够准确,在之后的编写中发现某个概念或对象更适合该命并且更合理,开发者可能就会通过这个机会发现之前的代码中可能存在的逻辑不准确或逻辑错误,如果开发者一直都在遵循尽可能准确代表某些概念或逻辑的命名方式,命名方式反过来会帮助开发者发现项目中潜在的错误

### 命名混乱或错误的可能原因

1. 没有理解对象或逻辑的本质
2. 理解了对象或逻辑的本质,但是没有规范命名的习惯
3. 理解了对象或逻辑的本质,也拥有了规范命名的意识,但是没有规范化命名的能力

### 如何养成良好的命名习惯

1. 严格自律,编写代码时时时刻刻保持着谨慎的态度对每个对象或逻辑进行命名
2. 分析和思考当前被命名的事物或逻辑的本质,基础设施决定上层建筑
3. 注意命名的方法技巧,清楚何时用动词,名词和形容词,良好的命名最终会是一句话或是一个有含义的名词
4. 确保被命名的属性或逻辑(方法)与其所代表或包含的含义一致
5. 时刻牢记代码不是一次性的产物,开发者的代码决定了后期维护的难易程度
6. 保持同一项目中,命名规则始终一致,不要`一会大写一会小写`,`一会全称一会简写`,`一会儿Pascal命名法一会儿camel命名法或匈牙利命名法`
7. 不要出现重复的命名,如果存在命名的嵌套关系,那么如果在外层已经命名的部分在内层就不要再重复表达
8. 对于属性或类名,名词总是应该在最后,形容词或形容词短语在名词之前,形容词/形容词短语+名词代表了属性的本质,比如说有一个数据的服务,我们就可以通过dataService来表述这首先是一个服务,其次这是一个获取数据的服务
9. 对于方法/逻辑,应该总是以动词开头,名词结尾,比如`addItem()` 以add作为动词开头,item作为名词结尾代表添加某种对象
10. 一般而言,开发者会选择camel或Pascal或kabab命名法
11. `camel命名法`形如 `aaaBbbCcc`或`aaa_bbb_ccc` , `Pascal命名法`形如`AaaBbbCcc`, `kabab命名法`形如`aaa-bbb-ccc`

### 良好命名习惯的反例

> 通过具体的代码来说明命名习惯

```typescript
ngOnInit() {
    this.dishservice.GetDishIds()
      .subscribe(dishIds => this._dishIds = dishIds);

    this.route.params
      .switchMap((params: Params) => {
        this._visibility = 'hidden';
        return this.dishservice.getDish(+params['id']);
      })
      .subscribe(dish => {
        this._dish = dish;
        this.dishcopy = dish;
        this.setPrevNext(dish.id);
        this._visibility = 'shown';
      },

        errmess => { this.dish = null; this.errMess = <any>errmess; });
  }
```

> `GetDishIds` 作为一个方法遵循了Pascal命名法,`setPrevNext`和`getDish`作为方法遵循了camel命名法,而`dishservice`作为一个服务没有遵循任何一种命名法, 在一个钩子中使用了三种方法的命名方式
> `_dishIds`,`_visibility`和`_dish`这三个属性以下划线开头,而其他属性则却以没有下划线开头
> `subcribe`方法的倒数第二行出现了多余的空行
> 对上述的代码改动一下

```typescript
ngOnInit() {
    this.dishService.getDishIds()
      .subscribe(dishIds => this.dishIds = dishIds);

    this.route.params
      .switchMap((params: Params) => {
        this.visibility = 'hidden';
        return this.dishservice.getDish(+params['id']);
      })
      .subscribe(dish => {
        this.dish = dish;
        this.dishcopy = dish;
        this.setPrevNext(dish.id);
        this.visibility = 'shown';
      },
        errmess => { this.dish = null; this.errMess = <any>errmess; });
  }
```

> 通过以上简单的例子就能发现,仅仅是通过细节就能发现很多问题
> 开发者在写代码时只要多细心,多注意排版是否美观一致、命名是否统一,那么就可以写出简洁美观的代码

### 其他一些小tips

> 使用`for in`和`for of` 时, 前者的参数永远是后者实体的单数形式, 例如

```javascript
for(let initItem of initOrderItem) {}
// initItem 和 initOrderItem 并不是同一个实体的单复数关系
for(let initOrderItem of initOrderItems) {}
// initOrderItem 是 initOrderItems的单数表达
```

> 在使用模板表达式或者是普通的+运算时, `+`的两边总是空一格

```javascript
let total = total + 1;
let name = `${firstName} + ${lastName}`
```

> 注意不要混淆动词和形容词的含义

```javascript
private createUser: string;
// createUser  的含义是 创造一个用户 更适合作为一个方法而存在
// 如果希望表达 创建的用户 应该使用
private createdUser: string;
```

> 在使用typescipt时, 尽量申明参数的类型和返回值的类型, 利用强类型语言有的优势, 当不确定类型时可以选择用any暂时代替

```typescript
//  定义接口的时候可以选择用大写表示该类型不会再程序中改变, 也可以使用Pascal命名法达到一样的目的
export interface USER {
    name: string;
    age: any;
}
private user: USER;
ngOnInit() {
    const createdUser = initUser('Ana', 18);
    console.log(createdUser);
}
public initUser(name: sting, age: any): USER {
    this.user.name = name;
    this.user.age = age;
    return this.user
}
```

## 总结

> 开发者在不经意间多写了`一个空格`或者`一个空行`或者`一个字母的大小写不一致`都会导致命名的不一致

> 如果开发者没有养成良好的命名习惯,那么写出来的代码`可读性`和`专业性`都会随之降低

> 以上举出的例子都是最简单的例子, 在实际的开发过程中`如何做到命名和其背后的本质完全一致`是一个开发者在职业生涯中需要不断考虑的问题

> 归根结底,开发者需要
1. 意识到命名规范的重要性
2. 端正态度认真命名
3. 尽可能确保命名的准确性
4. 时刻注意命名的一致性

> 养成良好的命名习惯是提高自身编程修养和逻辑能力的必经之路
