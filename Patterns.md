Паттерн - шаблон - это именованное эффективное решение характерной задачи проектирования ПО.

# Factory Methos (фабричный метод)

Пример: 
Есть такая ситуация. Нам нужны программисты, которые пишут код. Каждый программист - это отдельный класс. Java, Cpp и так далее. Если вдруг понадобится еще один программист, придется опять создавать класс, вместо этого можно воспользоваться фабричным методом. Который будет для нас создавать объекты, при этом мы заранее можем не знать какие эти объекты.
 ```JAVA
 class JavaDeveloper{
    public void getCode(){
        System.out.println("Code");
    }
}

class CppDeveloper{
    public void getCode(){
        System.out.println("Code");
    }
}

public class MyFactoryMethod {
    public static void main(String[] args) {
        JavaDeveloper jdeveloper = new JavaDeveloper();
        jdeveloper.getCode();

        CppDeveloper cppDeveloper = new CppDeveloper();
        cppDeveloper.getCode();
    }
}
```

Использование Интерфейса:
Создаем интерфейс в котором будет прописан шаблон классов, которые будут создаваться.
Затем создаем классы, которые реализуют этот интерфейс - теперь можно создвать новые объекты, исопльзуя этот интерфейс.
Но даже при такой реализации нам приходится вручную создавать Developer-а в программе, это не очень гибко.
```Java
interface Developer {
    void getCode();
}

class KotlinDeveloper implements Developer {
    @Override
    public void getCode() {
        System.out.println("Kotlin code");
    }

    public void getAdditionalCode(){
        System.out.println("Additional");
    }
}

class CsharpDeveloper implements Developer {
    @Override
    public void getCode() {
        System.out.println("Csharp code");
    }
}

public class MyFactoryMethodSolution {
    public static void main(String[] args) {
        Developer kotlinDeveloper = new KotlinDeveloper();
        kotlinDeveloper.getCode();

        KotlinDeveloper kotlinDeveloper1 = new KotlinDeveloper();
        kotlinDeveloper1.getCode();
        kotlinDeveloper1.getAdditionalCode();

        Developer csharpDeveloper = new CsharpDeveloper();
        csharpDeveloper.getCode();
    }
}
```

Использование паттерна:
Для использования паттерна создаем Интерфейс фабрику каждого из разрабов. Затем фабрику каждого разраба и создаем с помощью нее. 
```Java
package Patterns.FactoryMethod;

interface DeveloperFactory {
    Developer createDeveloper();
}

final class KotlinDeveloperFactory implements DeveloperFactory {
    @Override
    public Developer createDeveloper() {
        return new KotlinDeveloper();
    }
}

final class CsharpDeveloperFactory implements DeveloperFactory{
    @Override
    public Developer createDeveloper() {
        return new CsharpDeveloper();
    }
}

interface Developer {
    void getCode();
}

class KotlinDeveloper implements Developer {
    @Override
    public void getCode() {
        System.out.println("Kotlin code");
    }

    public void getAdditionalCode() {
        System.out.println("Additional");
    }
}

class CsharpDeveloper implements Developer {
    @Override
    public void getCode() {
        System.out.println("Csharp code");
    }
}

public class MyFactoryMethodSolution {
    public static void main(String[] args) {
        DeveloperFactory kotlinDeveloperFactory = new KotlinDeveloperFactory();
        DeveloperFactory CsharpDeveloperFactory = new CsharpDeveloperFactory();

        Developer kotlinDeveloper = kotlinDeveloperFactory.createDeveloper();
        Developer csharpDeveloper = CsharpDeveloperFactory.createDeveloper();

        kotlinDeveloper.getCode();

        KotlinDeveloper kotlinDeveloper1 = new KotlinDeveloper();
        kotlinDeveloper1.getAdditionalCode();
    }
}
```
