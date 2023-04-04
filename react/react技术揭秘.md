### 第三章 render

mount beginWork
创建当前fiber节点的第一个子元素的fiber节点

mount completeWork
创建当前filber节点的dom及属性的初始化，并且挂在到父dom里



beginwork中看能否直接复用current.fiber(bailoutOnAlreadyFinishedWork)是根据memoizedProps===pendingProps, 这个pendignprops（是执行完setstate后的节点的props）是从哪里获取的？





