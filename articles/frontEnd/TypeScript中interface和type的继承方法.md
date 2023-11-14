## interface 继承

`interface` 可以通过 `extends` 继承一个或者多个接口，例如：

```typescript
interface Person {
  name: string;
  age: number;
}

interface Teacher extends Person {
  subject: string;
  teachingYear: number;
}
```

## type 继承

`type` 继承和 `interface` 不一样，它不能继承 `interface`，只能用交叉类型`&`来继承其他 `type`。例如：

```typescript
type Person = {
  name: string;
  age: number;
};

type Teacher = Person & {
  subject: string;
  teachingYear: number;
};
```
