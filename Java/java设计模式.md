# 设计模式

[toc]

> ## 设计模式遵循的原则有6个：

1. 开闭原则（Open Close Principle）

   对扩展开放，对修改关闭

2. 里氏代换原则（Liskov Substitution Principle）

   只有当衍生类可以替换掉基类，软件单位的功能不受到影响时，基类才能真正被复用，而衍生类也能够在基类的基础上增加新的行为。

3. 依赖倒转原则（Dependence Inversion Principle）

   这个是开闭原则的基础，对接口编程，依赖于抽象而不依赖于具体。

4. 接口隔离原则（Interface Segregation Principle）

   使用多个隔离的借口来降低耦合度。

5. 迪米特法则（最少知道原则）（Demeter Principle）

   一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立。

6. 合成复用原则（Composite Reuse Principle）

   原则是尽量使用合成/聚合的方式，而不是使用继承。继承实际上破坏了类的封装性，超类的方法可能会被子类修改。

## 工厂模式

Java中的工厂模式是一种创建型设计模式，其主要目的是将对象的创建过程封装起来，隐藏具体的创建逻辑，使得客户端代码无需直接指定要创建对象的确切类，而是通过调用工厂方法来获取所需的对象实例。工厂模式有助于解耦对象的创建过程与使用过程，提升代码的灵活性、可扩展性和可维护性。

工厂模式通常包含以下几种变体：

### 1. 简单工厂模式

**组成部分**：
- 抽象产品（接口或抽象类）：定义产品的一组通用接口或行为。
- 具体产品（类）：实现抽象产品，提供具体的产品实现。
- 工厂类（通常是静态方法或单例类）：包含创建产品对象的逻辑，根据传入的参数或其他条件决定创建并返回何种具体产品的实例。

**工作原理**：
客户端不直接创建产品对象，而是调用工厂类提供的静态方法或通过工厂类的唯一实例调用方法，传递必要的参数（如产品类型标识）。工厂方法根据这些参数判断应该创建哪个具体产品的实例，并返回该实例给客户端。客户端只知道如何使用抽象产品接口，对具体产品的创建细节无感知。

### 2. 工厂方法模式

**组成部分**：

- 抽象产品（接口或抽象类）：同简单工厂模式。
- 具体产品（类）：同简单工厂模式。
- 抽象工厂（接口或抽象类）：声明一个创建产品的方法，通常命名为`createProduct()`。
- 具体工厂（类）：实现抽象工厂，提供创建具体产品的方法。

**工作原理**：
与简单工厂模式的区别在于，工厂方法模式将工厂类进一步抽象为接口或抽象类，然后由各个具体的工厂类来实现这个接口或继承抽象类，每个具体工厂负责创建一种具体产品。客户端不再依赖单一的工厂类，而是依赖抽象工厂，可以根据需求实例化相应的具体工厂，然后通过工厂对象调用`createProduct()`方法获取产品实例。这样，如果需要添加新的产品类型，只需新增一个具体产品类和对应的工厂类即可，无需修改已有代码。

在 Java 中实现简单工厂模式（也称为工厂方法模式的简化版本）通常涉及到创建一个工厂类，这个类负责根据某些条件返回不同类型的对象实例。下面是一个简单的例子，我们将创建一个形状接口 `Shape` 和几个实现这个接口的具体形状类，如 `Circle`、`Rectangle` 和 `Square`。然后，我们创建一个 `ShapeFactory` 类来根据用户的需求返回这些形状的实例。

首先，定义 `Shape` 接口：

```java
public interface Shape {
    void draw();
}
```

接着，创建几个具体的形状类，它们都实现了 `Shape` 接口：

```java
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

public class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a square");
    }
}
```

现在，我们创建 `ShapeFactory` 类，它有一个静态方法 `getShape`，这个方法接收一个字符串参数，根据这个参数返回相应的形状实例：

```java
public class ShapeFactory {
    public static Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("RECTANGLE")) {
            return new Rectangle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        }
        return null;
    }
}
```

最后，在主程序中使用 `ShapeFactory` 来获取形状实例并调用它们的 `draw` 方法：

```java
public class Main {
    public static void main(String[] args) {
        Shape circle = ShapeFactory.getShape("CIRCLE");
        circle.draw();

        Shape rectangle = ShapeFactory.getShape("RECTANGLE");
        rectangle.draw();

        Shape square = ShapeFactory.getShape("SQUARE");
        square.draw();
    }
}
```

当运行上面的 `Main` 类时，控制台会输出每个形状被绘制的信息。这就是简单工厂模式的基本应用，它允许你在不修改客户端代码的情况下添加新的形状类型，只需要在 `ShapeFactory` 中添加对应的逻辑即可。然而，如果需要添加大量不同的类型，这种方法可能会导致 `ShapeFactory` 的 `getShape` 方法变得非常庞大和难以维护。这时，考虑使用更高级的设计模式，如工厂方法模式或抽象工厂模式，可能更为合适。

### 3. 抽象工厂模式

**组成部分**：

- 抽象产品族（接口或抽象类）：定义产品族中不同类型的抽象产品，如`AbstractProductA`和`AbstractProductB`。
- 具体产品族（类）：实现抽象产品族中的各个产品接口，如`ConcreteProductA1`、`ConcreteProductA2`、`ConcreteProductB1`、`ConcreteProductB2`等。
- 抽象工厂（接口或抽象类）：声明创建产品族中各类型产品的方法，如`createProductA()`和`createProductB()`。
- 具体工厂（类）：实现抽象工厂，提供创建某一特定产品族中各类型产品的方法。

**工作原理**：
抽象工厂模式用于处理具有多种产品族（即相关或相互依赖的产品集合）的情况。客户端依赖于抽象工厂，通过具体工厂来获取一个完整的产品族（即一系列相关的产品对象）。当需要更换整个产品族时，只需要改变具体工厂的实例即可，无需修改客户端代码。这种模式适用于需要支持多种不同平台或环境，每个平台或环境都需要一套特定产品组合的情况。

总结来说，Java中的工厂模式通过引入一个专门负责对象创建的工厂角色，将对象的创建过程从客户端代码中分离出来，实现了对象的创建与使用之间的解耦。简单工厂模式、工厂方法模式和抽象工厂模式分别针对不同复杂度和需求场景提供了不同程度的抽象和封装，帮助开发者构建更灵活、易于维护和扩展的软件系统。

## 代理模式

Java中的代理模式（Proxy Pattern）是一种结构型设计模式，它允许你在访问一个对象时，通过另一个称为“代理”的对象来间接地操作目标对象。代理模式的核心思想是在不改变原始类代码的情况下，通过引入代理类来给原始类附加功能。代理模式在Java中通常用于以下几种情况：

1. **控制对对象的访问**：
   - 代理可以检查权限，决定是否允许客户端访问目标对象。
   - 代理可以缓存结果，避免重复计算或访问昂贵的资源。

2. **远程代理**：
   - 当目标对象位于不同的地址空间时，代理可以作为本地代表。

3. **虚拟代理**：
   - 代理可以用于延迟加载大对象或资源密集型对象，直到真正需要时才加载。

4. **智能引用**：
   - 代理可以追踪对象的引用次数，实现自动垃圾回收。

代理模式通常涉及以下三个角色：

- **Subject（抽象主题）**：这是所有代理对象和真实对象都应该实现的接口。它定义了一个公共接口，以便在任何时候都可以用一个代理对象替换一个真实对象。

- **RealSubject（真实主题）**：这是代理所代表的真实对象，实现了Subject接口，并包含具体的业务逻辑。

- **Proxy（代理）**：这也是一个实现了Subject接口的对象，它的职责是在访问真实对象之前或之后执行一些额外的操作，如权限检查、缓存、日志记录等。

在Java中，代理模式可以通过静态代理或动态代理来实现：

### 静态代理

**静态代理**：需要手动编写代理类，代理类和真实对象都实现相同的接口或继承相同的抽象类。这种方式比较直接，但是每增加一个接口都需要创建一个代理类。

在Java中实现静态代理相对直接。静态代理的主要特点是代理类和被代理的接口或类是在编译时就已经确定的，而不是像动态代理那样在运行时生成的。下面我将展示如何为一个简单的接口`MyService`创建一个静态代理类。

首先，我们定义`MyService`接口：

```java
public interface MyService {
    void doSomething();
    String doAnything(String input);
}
```

接着，实现`MyService`接口：

```java
public class MyServiceImpl implements MyService {
    @Override
    public void doSomething() {
        System.out.println("Doing something...");
    }

    @Override
    public String doAnything(String input) {
        return "Result of doing anything with: " + input;
    }
}
```

然后，创建一个静态代理类`MyServiceProxy`，它也实现了`MyService`接口，并在其方法中调用真实对象的方法：

```java
public class MyServiceProxy implements MyService {
    private final MyService realService;

    public MyServiceProxy(MyService realService) {
        this.realService = realService;
    }

    @Override
    public void doSomething() {
        System.out.println("Before doSomething");
        realService.doSomething();
        System.out.println("After doSomething");
    }

    @Override
    public String doAnything(String input) {
        System.out.println("Before doAnything");
        String result = realService.doAnything(input);
        System.out.println("After doAnything");
        return result;
    }
}
```

在上述代码中，`MyServiceProxy`类持有`MyServiceImpl`的一个引用（或任何实现了`MyService`接口的对象），并在其方法中调用该引用的方法，同时可以添加额外的行为，如日志记录。

最后，在主程序中使用`MyServiceProxy`：

```java
public class Main {
    public static void main(String[] args) {
        // 创建真实的服务实例
        MyService realService = new MyServiceImpl();

        // 创建代理实例
        MyService proxyService = new MyServiceProxy(realService);

        // 通过代理对象调用方法
        proxyService.doSomething();
        String result = proxyService.doAnything("test");
        System.out.println(result);
    }
}
```

当你运行`Main`类时，你会看到在方法调用前后都有日志输出，这表明静态代理正在按预期工作。

静态代理在需要为一组固定的方法添加额外功能时非常有用，但缺点是对于每个接口都需要创建一个代理类，如果接口数量较多，代码量可能会变得较大。

### 动态代理

**动态代理**：利用反射和Java的动态代理机制（如使用`java.lang.reflect.Proxy`类和`InvocationHandler`接口），可以在运行时动态生成代理类。这种方式不需要为每个接口写代理类，但是实现稍微复杂一些。

动态代理有两种主要实现方式：

- **JDK动态代理**：适用于实现了接口的对象。

   在Java中，使用JDK动态代理来创建一个动态代理类是一个常见的需求，尤其是当需要在不修改现有代码的基础上添加新的行为时。下面我将展示如何使用JDK动态代理来实现一个简单的例子。

   假设我们有一个接口`MyService`，它定义了一些方法，而我们想要在不修改这个接口实现的情况下，为这些方法添加日志记录的功能。我们可以使用JDK动态代理来达到这个目的。

   首先，定义`MyService`接口：

   ```java
   public interface MyService {
       void doSomething();
       String doAnything(String input);
   }
   ```

   然后，实现这个接口：

   ```java
   public class MyServiceImpl implements MyService {
       @Override
       public void doSomething() {
           System.out.println("Doing something...");
       }
   
       @Override
       public String doAnything(String input) {
           return "Result of doing anything with: " + input;
       }
   }
   ```

   接下来，我们创建一个代理类，它会使用`java.lang.reflect.InvocationHandler`接口来处理代理对象上的方法调用：

   ```java
   import java.lang.reflect.InvocationHandler;
   import java.lang.reflect.Method;
   
   public class MyServiceProxy implements InvocationHandler {
       private final Object target;
   
       public MyServiceProxy(Object target) {
           this.target = target;
       }
   
       @Override
       public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
           // 在方法调用前的操作，例如日志记录
           System.out.println("Before method call: " + method.getName());
   
           // 调用目标方法
           Object result = method.invoke(target, args);
   
           // 在方法调用后的操作
           System.out.println("After method call: " + method.getName());
   
           return result;
       }
   }
   ```

   最后，我们使用`java.lang.reflect.Proxy`类来创建一个动态代理对象：

   ```java
   import java.lang.reflect.Proxy;
   
   public class Main {
       public static void main(String[] args) {
           // 创建真实的服务实例
           MyService realService = new MyServiceImpl();
   
           // 创建代理处理器
           MyServiceProxy proxyHandler = new MyServiceProxy(realService);
   
           // 使用Proxy类创建动态代理对象
           MyService proxyService = (MyService) Proxy.newProxyInstance(
                   MyService.class.getClassLoader(),
                   new Class[]{MyService.class},
                   proxyHandler
           );
   
           // 通过代理对象调用方法
           proxyService.doSomething();
           String result = proxyService.doAnything("test");
           System.out.println(result);
       }
   }
   ```

   在这个例子中，`MyServiceProxy`类实现了`InvocationHandler`接口，当通过动态代理对象调用任何方法时，都会调用`invoke`方法。在这个方法里，我们可以在实际调用目标方法前后执行任意代码，例如添加日志记录。

   当你运行`Main`类时，你会看到在方法调用前后都有日志输出，这表明动态代理正在按预期工作。

- **CGLIB动态代理**：适用于没有实现接口的对象，通过字节码技术为一个类创建子类。

代理模式在Java开发中非常常见，尤其是在框架中，如Spring的AOP（面向切面编程）就广泛使用了动态代理来实现横切关注点（如事务管理、日志记录等）。
