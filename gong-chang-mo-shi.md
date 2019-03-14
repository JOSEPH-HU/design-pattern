# 工厂模式的定义
    定义一个用于创建对象的接口，让子类决定实例化那个类。工厂方法使一个类的实例化延迟到子类
  
![](/assets/唯秘截图_20190313091341.png)

# 工厂模式有点
    1.良好的封装性，代码结构清晰，只要知道产品的类型，不需要知道创建对象的艰辛过程，降低模块间的耦合性
    2.工厂模式的扩展性比较好
    3.屏蔽产品类。产品类如何变化，调用者都不需要关心，它只需要关心产品的接口，只要接口不变，系统中的上层模块就不要发生变化
    4.工厂模式是典型的解耦框架
# 工厂模式使用场景
    1.工厂模式是new一个对象的替代品，所以在所有需要生成对象的地方都可以使用，但是需要确定是否增加一个工厂类进行管理，增加代
    码复杂度
    2.需要灵活、可扩展的框架时，可以考虑采用工厂模式
    3.工厂模式可以用在异构项目中
    4.可以使用在测试驱动开发的框架下
# 简单工厂模式
    一个模块仅需要一个工厂类，没有必要把它生产出来，使用静态的方法就可以
![](/assets/唯秘截图_20190314090513.png)
    HumanFactory仅有两个地方发生变化：去掉了继承并且加上static。简单工厂模式也叫静态工厂模式
# 升级为多工厂模式
    当我们在做一个复杂的项目时，会遇到初始化一个对象很耗费时间，所有的产品类放到一个工厂方法进行初始化会使代码结构不够清晰.
![](/assets/唯秘截图_20190314091340.png)
    在复杂的应用中一般采用多工厂的方法，然后在增加一个协调类，避免调用者与各个子工厂交流，协调类的作用是封装子工厂类，对高层模块提供统一的接口.
# 替代单例模式
![](/assets/唯秘截图_20190314092145.png)
```
public class SingletonFactory {
    private static Singleton singleton;

    static {
        try {
            Class c1 = Class.forName(Singleton.class.getName());
            Constructor constructor = c1.getDeclaredConstructor();
            constructor.setAccessible(true);
            singleton = (Singleton) constructor.newInstance();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
    }
}
```
    以上通过工厂模式创建一个单例对象，该框架可以继续扩展，在一个项目红可以产生一个单例构造器，所需要生产单例的类都遵循
    构造方法是私有的，通过上面的方法可以只要输入一个类就可以获得一个唯一的一个实例.
# 延迟初始化
    延迟初始化就是一个对象被消费完毕后，并不立刻释放，工厂类保持初始化状态，等待再次被使
![](/assets/唯秘截图_20190314093443.png)
    通过定一个一个Map容器，容纳所有的对象，如果在map中已经有对象，直接取出返回；如果没有，产生一个放到map中下次使用
    