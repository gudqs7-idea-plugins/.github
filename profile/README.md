# Hello everyone !

# GenerateAllSetter Postfix Completion 是做什么的？

- 是一个 IDEA 插件，仅支持 Java 。
- 参考了 GenerateAllSetter 插件，作为其补充，添加了几个 Postfix 语法，功能与 GenerateAllSetter 基本一致。
- 在 pojo 变量之后通过 `.allset` 生成所有 setter
- 在 pojo 变量之后通过 `.allsetn` 生成所有设置器（但没有默认值）
- 在 pojo 变量之后通过 `.allget` 生成所有 getter
- 在使用 @lombok.Builder 的 pojo 变量之后通过 `.allbuilder` 生成所有 setter 调用链

# 为什么这个项目有用？

- 多一个选择，另外本人认为 Postfix 比较顺手，有助于进一步提高效率。
- 给大家提供一个 Postfix 插件开发模板，希望大家多开发一些提高效率的插件。

# 我该如何开始？

## 1.安装插件
### zip 包安装
从最新的 [Release][latest-release] 页下载 zip 包，然后打开 IDEA，进入 Settings --> Plugins --> 小齿轮 --> Install Plugin from Disk  
![zip](parts/imgs/install-plugin-from-disk.png)

### Marketplace 安装
打开 IDEA，进入 Settings --> Plugins，选中 Marketplace，输入 GenerateAllSetter Postfix Completion 点击 Install  
![Marketplace](parts/imgs/install-from-marketplace.png)


## 2.打开俺提供的示例项目
示例项目地址：[docer-savior-plugin-usage-examples](https://github.com/docer-savior/docer-savior-plugin-usage-examples)  

或  
```shell
git clone https://github.com/docer-savior/docer-savior-plugin-usage-examples
```
下载后，找到 `cn.gudqs.example.genset.GenerateSetterAndGetterUsage` 文件

## 3.插件使用

演示所使用的基础类  
```java

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
class Foo {

    private Integer testInt;

    private Long testLong;

    private Float testFloat;

    private Double testDouble;

    private Boolean testBoolean;

}
```

### 生成 set
```java
public void usage01() {
    // 用法1, 生成所有 set 方法, 带默认值, 通过 postfix
    Foo foo = new Foo();
    // 取消下面的注释, 光标位于 allset 后面, 按下 Tab 键
//        foo.allset
    // 即可得到下面结果, 且 foo.allset 会自动消失
    foo.setTestInt(0);
    foo.setTestLong(0L);
    foo.setTestFloat(0f);
    foo.setTestDouble(0D);
    foo.setTestBoolean(false);
}
```

### 生成 get
```java
public void usage03() {
    // 用法3, 生成所有 get 方法, 通过 postfix
    Foo foo = new Foo();
    // 取消下面的注释, 光标位于 allget 后面, 按下 Tab 键
//        foo.allget
    // 即可得到下面结果, 且 foo.allget 会自动消失
    Integer testInt = foo.getTestInt();
    Long testLong = foo.getTestLong();
    Float testFloat = foo.getTestFloat();
    Double testDouble = foo.getTestDouble();
    Boolean testBoolean = foo.getTestBoolean();
}
```


## Lombok 的 @Builder 快速生成所有赋值方法的调用链

```java
public void usage04() {
    // 用法4, 生成所有 set 方法, 通过 builder, 通过 postfix
    // 取消下面的注释, 光标位于 allbuilder 后面, 按下 Tab 键
//        Foo.builder().allbuilder
    // 即可得到下面结果
    Foo foo = Foo.builder()
            .testInt(0)
            .testLong(0L)
            .testFloat(0f)
            .testDouble(0D)
            .testBoolean(false)
            .build();
}
```

## 根据一段含有源对象（a）/目标对象（b）的 b.setXxx(a.getXxx()) 方法代码生成所有 set 方法以快速实现对象转换

```java
public void usage05() {
    // 用法5, 将 src 的数据赋值给 dest, 常用于两个不同类直接进行 convert(需字段名称相同), 通过 postfix
    Foo src = new Foo();
    Foo dest = new Foo();
    // 取消下面的注释, 光标位于 convert 后面, 按下 Tab 键
//        dest.setTestInt(src.getTestInt());.convert
    // 即可得到下面结果
    dest.setTestInt(src.getTestInt());
    dest.setTestLong(src.getTestLong());
    dest.setTestFloat(src.getTestFloat());
    dest.setTestDouble(src.getTestDouble());
    dest.setTestBoolean(src.getTestBoolean());
}
```


# 如果需要，我可以从哪里获得更多帮助？

## 通过提交 Issue 来获取帮助
 [点击访问 Github Issue](https://github.com/docer-savior/getter-setter-postfix-idea-plugin/issues)  
> 欢迎大家提问，欢迎大家一起完善它！

**另外，我接入了 IDEA 的错误处理组件，因此当发现插件报错提示时，按照 IDEA 提示，可查看错误信息，并一键上报给我（即自动生成一个 Issue）**

## 通过查看 Wiki 来获取更多说明

- [入门教程](https://github.com/docer-savior/getter-setter-postfix-idea-plugin/wiki/%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B)

## 贡献指南
 [贡献指南](CONTRIBUTING_CN.md)

# 致谢名单

- [Github intellij-generateAllSetMethod](https://github.com/gejun123456/intellij-generateAllSetMethod)
- [Github genSets](https://github.com/yoke233/genSets)
