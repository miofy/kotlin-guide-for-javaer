

## 可变量与不可变量

- Java

```java
// 可变量
int i = 5;

// 不可变量
final int j = 5;
```

- Kotlin

```kotlin
// 可变量
var i: Int = 5

// 不可变量
val j: Int = 5
```

## 常量

- Java

```java
// 普通类定义常量
class Constants {
    // 具有公有访问权限的静态不可变量，在Java中用于实现常量字面量
    public static final String CONSTANT_NAME = "Daniel Lea";
}

// 抽象类定义常量
abstract class Constants {
    // 与普通类定义方式相同
    public static final String CONSTANT_NAME = "Daniel Lea";
}

// 接口定义常量
interface Constants {
    // 默认使用'public static final'修饰，可省略修饰符 
    String CONSTANT_NAME = "Daniel Lea";
}

// 枚举类定义常量
enum Constants {

    // 常量对象, 内部维护name属性
    CONSTANT_NAME("Daniel Lea"),
    ;

    private final String name;

    Constants(final String name) {
        this.name = name;
    }

    // setter/getter etc.
    ...
}
```

- Kotlin

```kotlin
// 普通类的伴生对象定义常量
class Constants {
    
    companion object A {
        // const关键字声明kotlin常量
        const val CONSTANT_NAME: String = "Daniel Lea"
    }

    companion object B {
        // 使得能按Java方式调用Kotlin常量
        @JVMStatic
        val CONSTANT_NAME: String = "Daniel Lea"
    }
}

// 接口伴生对象定义常量
interface Constants {
    
    companion object {
        // 伴生对象名称可以省略，与普通类使用方式相同
        @JVMStatic
        val CONSTANT_NAME: String = "Daniel Lea"
    }
}

// 单例对象定义常量
object Constants {

    const val CONSTANT_NAME1: String = "Daniel Lea"

    @JVMStatic
    val CONSTANT_NAME2: String = "Daniel Lea"
}

// 全局常量，定义在.kt文件级别(编译后即在xxKt类级别)
const val CONSTANT_NAME: String = "Daniel Lea"

// 枚举类定义常量
enum class Constants constructor(val name: String) {


}
```

## 相等性比较

- Java

```java

```

- Kotlin

```kotlin

```


## 控制语句


## 面向对象

---

## JUnit单元测试

- Java

```java
@RunWith(JUnit4.class)
class JavaHelloWorldTest {

    @Test
    public void testHelloWorld() {
        System.out.println("Hello World!");
    }
}
```

- Kotlin

```kotlin
@RunWith(JUnit4::class)
class KotlinHelloWorldTest {

    /**
     * 当且仅当在测试用例中，可以使用反引号括起来带空格的方法名
     */
    @Test fun `test hello world`() {
        println("Hello World!")
    }

    /**
     * 测试用例中也允许方法名使用下划线
     */
    @Test fun test_hello_world() {
        println("Hello World!")
    }

    /**
     * 一般情况下，测试用例应该与Java方法命名风格一致
     */
    @Test fun testHelloWorld() {
        println("Hello World!")
    }
}
```

---

## Maven编译插件

- Java

```xml
<plugins>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.5.1</version>
        <executions>                
            <execution>
                <id>default-compile</id>
                <phase>none</phase>
            </execution>
            <execution>
                <id>default-testCompile</id>
                <phase>none</phase>
            </execution>
            <execution>
                <id>java-compile</id>
                <phase>compile</phase>
                <goals> <goal>compile</goal> </goals>
            </execution>
            <execution>
                <id>java-test-compile</id>
                <phase>test-compile</phase>
                <goals> <goal>testCompile</goal> </goals>
            </execution>
        </executions>
        <configuration>
            <source>1.8</source> 
            <target>1.8</target>                                                                               
            <encoding>UTF-8</encoding>
            <skipTests>true</skipTests>                                                                         
            <verbose>true</verbose>
        </configuration>
    </plugin>
    ...
</plugins>
```

- Kotlin

```xml
<plugins>
    <plugin>
        <groupId>org.jetbrains.kotlin</groupId>
        <artifactId>kotlin-maven-plugin</artifactId>
        <version>1.3.1</version>
        <executions>
            <execution>
                <id>compile</id>
                <goals> <goal>compile</goal> </goals>
                <configuration>
                    <sourceDirs>
                        <sourceDir>${project.basedir}/src/main/kotlin</sourceDir>
                        <sourceDir>${project.basedir}/src/main/java</sourceDir>
                    </sourceDirs>
                </configuration>
            </execution>
            <execution>
                <id>test-compile</id>
                <goals> <goal>test-compile</goal> </goals>
                <configuration>
                    <sourceDirs>
                        <sourceDir>${project.basedir}/src/test/kotlin</sourceDir>
                        <sourceDir>${project.basedir}/src/test/java</sourceDir>
                    </sourceDirs>
                </configuration>
            </execution>
        </executions>
        <configuration>
            <args>
                <!-- 开启支持协程功能 -->
                <arg>-Xcoroutines=enable</arg>
                <!-- 开启支持JDK8接口默认方法 -->
                <arg>-Xjvm-default=enable</arg>
                <!-- 开启支持内联类 -->
                <arg>-XXLanguage:+InlineClasses</arg>
            </args>
            <jvmTarget>1.8</jvmTarget>
        </configuration>
    </plugin>
    ...
</plugins>       
```

