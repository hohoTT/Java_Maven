# Java_Maven

用于JAVA的MAVEN练习

依赖的第一部分讲解：
maven-a、maven-b、maven-c  三个项目的一开关系为：

1. maven-a 依赖于 maven-b
2. maven-c 依赖于maven-a

所以 
3. maven-c 依赖于 maven-b


依赖的第二部分讲解：（越接近依赖与哪一个）
c - >  a - > b
2.0   2.0   2.4

maven-b 中使用的版本为 2.4
maven-a 中使用的版本为 2.0
因为maven-c离maven-a近，所以版本为2.0
maven-c 中使用的版本为 2.0


依赖的第三部分讲解：（距离相同时，依赖与加载的顺序，先加载先依赖）


依赖的继承：
实现maven项目中的依赖继承关系，创建一个父maven项目maven-parent，使得maven-b继承与maven-parent，实现代码的复用


