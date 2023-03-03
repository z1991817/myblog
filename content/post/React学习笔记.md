---
title: "React学习笔记"
date: 2023-03-03T11:00:58+08:00
draft: false
---

### React学习笔记

#### 目前学习基于hooks开发 + TypeScript开发，开始初学，有问题就记录

*它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性。*

1. 定义组件，react组件名称首字母必须大写

   ``` javascript
   const Myapp = ()=>{
     return(
     	<div>hello,world</div>
     )
   }
   ```

    ``` return ``` 可以直接写jsx函数


2. 组件中初始化的 ``` data ```值，每个组件都有一些自己的值，首先需要定义出来

   ``` useState ``` 来定义初始化的值

   ``` javascript
   // 定义一个数字
   const [count,setCount] = useState(0)
   // 定义一个对象或空对象
   const [mayObj,setMyobj] = useState({})
   const [mayObj1,setMyobj1] = useState({
     name:'xxx',
     ...
   })
   // 定义一个数组
   const [mayArr,setMyarr] = ([])
   /**
   *这种 JavaScript 语法叫数组解构。它意味着我们同时创建了 count 和 setCount 两个变量，count 的值为 useState 返回的第一个值，setCount 是返回的第二个值。它等价于下面的代码：
   */
   var fruitStateVariable = useState('banana'); // 返回一个有两个元素的数组
   var count = fruitStateVariable[0]; // 数组里的第一个值
   var setCount = fruitStateVariable[1]; // 数组里的第二个值
   /**
   *当我们使用 useState 定义 state 变量时候，它返回一个有两个值的数组。第一个值是当前的 state，第二个值是更新 state 的函数。使用 [0] 和 [1] 来访问有点令人困惑，因为它们有特定的含义。这就是我们使用数组解构的原因。
   */
   ```

   修改值

   ``` javascript
   // 普通变量
   setCount(3)
   // 对象
   setMyobj({
     name:'哈哈',
     age:39
   })
   // 数组的增删改查
   /**
   * 增加
   * 因为JavaScript中对象和数组是引用类型，将一个引用类型赋值给另一个变量只是将变量的引用指向原对象或数组，而不是创建一个新的副本。这意味着在修改temp变量时，也会修改dataSource数组。
   * setArray函数是异步执行的，所以在更新数组之后，不能立即依赖数组的最新值进行下一步操作。如果需要对更新后的数组进行操作，可以使用useEffect hook监听数组的变化并执行相关操作。
   * 这样就可以在不直接修改原数组的情况下，添加新的元素
   */
   setArray([...dataSource, obj]);
   /**
   * 修改
   * 在React中修改数组的某个元素，建议使用不可变性（immutability）的方式，即先创建一个数组副本进行修改，然后将修改后的数组副本作为新的状态更新到组件中。
   *如果要修改数组的第一个元素的某个属性，可以使用数组的map方法来实现。
   */

   const temp = myArray.map((item,index)=>{
     if(index === record.key - 1){
       return { ...item, name: 'xiugaile' + index };
     }
     return item;
   });
   setArray(temp);

   /**
   * 删除
   * 修改数组时，使用不可变性的方式，即先创建一个新的数组副本进行修改，然后将修改后的数组副本作为新的状态更新到组件中
   */

   const index = myArray.findIndex(item => item.key === record.key);
   if (index !== -1) {
     const temp = [...myArray];
     temp.splice(index, 1);
     setArray(temp);
   }
   ```

1. 组件通信

    大致流程：父组件```=>```新增打开模态框``` => ```把新增的数据传入父组件```=>```父组件传入子组件```=>```子组件监听``` props``` 有数据后给数组加入一条
    ``` javaScript
    //父组件
   <div>
     <Button onClick={handleAdd}>增加</Button>
   	<Mytable data={person}></Mytable>
   	<Mymodal status={status} close={handleClose} addItem={getAddItem}></Mymodal>
   </div>
   // 打开模态框
   const handleAdd = () => {
      setStatus(true)
   }
   // 父组件定义getAddItem方法接受modal回传过来的参数
   const getAddItem = (obj)=>{
      setPerson(obj)
   }

   // modal组件回传数据 react数据传递是直接传入一个方法与vue是有一定区别的
   const onFinish = (values) => {
      props.addItem(values)
   }

   // table组件接受值并且添加到组件后面,加入判断是第一次渲染时也会加入空数据,有数据在添加
   useEffect(() => {
       if(data.hasOwnProperty('name')){
         data.key = uuidv4();
         setArray(prevArray => [...prevArray, data]);
       }
     }, [data]);
    ```
   简单版,第一次上手react简单记录下.