# JavaGenericsWildCardVariant

```java

import java.util.List;
import java.util.ArrayList;

// X
class Creature {
    @Override
    public String toString() {
        return "I am " + this.getClass().getSimpleName();
    }
}

// Y
class Animal extends Creature {
}

// Z
class Fish extends Animal {
}

// A
class Shark extends Fish {
}

// B
class HammerShark extends Shark {
}

// C
class DeadHammerShark extends HammerShark {
}

public class Main {

    public static void main(String[] args) {
        List<Shark> sharks = new ArrayList<>();

        Main.add(sharks);
        Shark shark = Main.get(sharks, 2);
        System.out.println(shark);
    }

    public static void add(List<? super Shark> list) {
        //This is valid because ? is an unknown type that is parent to Shark, so this type can
        // atleast store Shark type
        list.add(new Shark());
        list.add(new HammerShark());
        list.add(new DeadHammerShark());

        //It cant get anything out of it because it doesnt know an exact parent of Shark, it may be Shark, Fish, Animal or Creature
        // Shark s = list.get(0); //compiler error, maybe ? is Animal
        // Animal a = list.get(0)/ //compiler error, mayber ? is Creature
    }


    public static Shark get(List<? extends Shark> list, int index) {
        // This is valid because, ? is an unknown type that is child to Shark, so it will always be type of Shark
        return list.get(index);


        // It can't store anything, because ? is an unknown type that is child to Shark, but which exact child?
        // list.add(new Shark()); // compiler error, ? maybe HammerShark
        // list.add(new HammerShark()); // compiler error, ? maybe DeadHammerShark
        // list.add(new DeadHammerShark()); //compiler error, ? maybe some other class inherit this DeadHammerShark class
    }
}
```
