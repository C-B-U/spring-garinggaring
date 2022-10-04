## Supplier<T>

Parameter 없이 반환값만 가짐

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}

// 사용 예시
Supplier<String> supplier = () -> "Hello World!";
System.out.println(supplier.get());
```

## Consumer<T>

Parameter은 있으나 반환값이 없음

```java
// 정의
@FunctionalInterface
public interface Consumer<T> {

    void accept(T t);

    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}

// 예시
Consumer<String> consumer = (str) -> System.out.println(str.split(" ")[0]);
consumer.andThen(System.out::println).accept("Hello World");

// 출력
Hello
Hello World
```

## Function<T, R>

Paramenter, 반환값 둘 다 있음

```java
@FunctionalInterface
public interface Function<T, R> {

    R apply(T t);

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

    static <T> Function<T, T> identity() {
        return t -> t;
    }
}

// 예시, 메소드 참조로 간소화 가능(String::length;)
Function<String, Integer> function = str -> str.length();
function.apply("Hello World");
```

## Predicate<T>

Parameter을 받아 Boolean으로 반환

```java
// 정의
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }

}

// 예시
Predicate<String> predicate = (str) -> str.equals("Hello World");
predicate.test("Hello World");
```

# 참고자료

## lambda Interface

https://mangkyu.tistory.com/113

## stream API

https://mangkyu.tistory.com/114

## FlatMap 및 Reduce, Null-Safe, Parallel Stream

https://mangkyu.tistory.com/115
