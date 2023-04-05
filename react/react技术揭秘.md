### 第三章 render

mount beginWork
创建当前fiber节点的第一个子元素的fiber节点

mount completeWork
创建当前filber节点的dom及属性的初始化，并且挂在到父dom里



beginwork中看能否直接复用current.fiber(bailoutOnAlreadyFinishedWork)是根据memoizedProps===pendingProps, 这个pendignprops（是执行完setstate后的节点的props）是从哪里获取的？





### 第四章commit

flushPassiveEffects() // 执行上一次useeffect的销毁函数和这一次useeffect的回调函数（要在本次commit阶段之前遗留的useeffect给执行完 ）
// 这里遗留的useeffect也不太清楚具体是咋遗留的？

beforemutation
1. 执行一些dom相关的比如blur，可以先不关注
2. 执行 classcomponents里的getSnapShotBeforeUpdate()
3. scheduleCallback(normalpriorty, ()=> {flushPassiveEffects()  }) // 给useeffect的回调函数一个优先级，**异步**执行该回调函数



mutation
遍历有effecttag的fiber,根据其类型进行dom操作：插入、更新、删除、etc，有一些细节点需要注意
1. 在update时，如果是functioncomponentfiber节点， 需要先调用uselayouteffect的销毁函数，然后再更新各个属性
2. 在deletion时，会递归的删除这个fiber的子节点，而不是直接删除 ，如果是functioncomponentfiber节点，还会执行useeffect的销毁函数 ，如果是classcomponentfiber,会执行componentwillunmoount生命周期 


layout
1. 对于classcomponent,执行componentdidmount/componentdidupdate
2. 对于functioncomponentfiber,会执行uselayout的回调函数
3. 执行classcomponent的this.setState()的第二个参数/React.render()的第三个参数
4. 把useeffect的销毁、回调函数添加到一个数组中，便于异步调用  （这的异步调用useeffect就是在beforemutation里创建的）
