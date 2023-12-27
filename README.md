# Первое задание:

import java.sql.SQLOutput;
import java.util.*;
import java.util.function.Supplier;

//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    public static void main(String[] args) {
        Calculator calc = Calculator.instance.get();

        try {
            int a = calc.plus.apply(1, 2);
            int b = calc.minus.apply(1, 1);
            int c = calc.devide.apply(4, 0);
            calc.println.accept(c);
        } catch (Exception exception) {
            System.out.printf(("Делить на ноль нельзя!\n " + " Ошибка =>" + exception.getMessage()));
        }
    }
}
import java.util.function.*;

public class Calculator {
    static Supplier<Calculator> instance = Calculator::new;


    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    BinaryOperator<Integer> multiply = (x, y) -> x * y;


    BinaryOperator<Integer> devide = (x, y) -> x / y;

    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;

    Predicate<Integer> isPositive = x -> x > 0;
    Consumer<Integer> println = System.out::println;

}
# второе задание:
import java.util.*;
import java.util.function.Function;

//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {

    public static void main(String[] args) {
        OnTaskDoneListener listener = System.out::println;
        OnTaskErrorListener listener1 = System.out::println;
        Worker worker = new Worker(listener, listener1);
        worker.setErrorCallback();
    }
}

@FunctionalInterface
interface OnTaskDoneListener {
    void onDone(String result);
}

@FunctionalInterface
interface OnTaskErrorListener {
    void onError(String result);
}

import java.util.function.*;

public class Worker {
    private OnTaskErrorListener errorCallback;
    private OnTaskDoneListener callback;

    public Worker(OnTaskDoneListener callback, OnTaskErrorListener errorCallback) {
        this.callback = callback;
        this.errorCallback = errorCallback;
    }


    public void start() {
        for (int i = 0; i < 100; i++) {
            callback.onDone("Task " + i + " is done");
        }
    }
    //TODO: данный метод реализует именно ту задачу которая была поставлена
    public void setErrorCallback() {
        for (int i = 0; i < 34; i++) {
            errorCallback.onError("Task " + i + " is done");
        }
        errorCallback.onError("Task " + "33 " + "is error");
    }
}


