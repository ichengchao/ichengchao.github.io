---
layout: post
title: JMX3:数据类型
date: 2014-01-24 12:36
author: charles
comments: true
tags:
 - java
 - jmx
---

上两篇已经介绍了jmx的基本知识.
不过在真实的应用场景下,我们经常需要暴露比较复杂的数据类型.
jmx支持吗?
答案是肯定的.
那就写代码试试吧:

```java
//一个简单的数据类
public class MyDataType {
    private String name;
    private int    age;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}

//定义一个MBean
public interface DataTypeMBean {
    int getCount();
    List&lt;String&gt; getNames();
    MyDataType getMyDataType();
    List&lt;MyDataType&gt; getMyDataTypeList();
}

//定义一个实现类
public class DataType implements DataTypeMBean {
    @Override
    public int getCount() {
        return 2014;
    }
    @Override
    public List&lt;String&gt; getNames() {
        return Arrays.asList(&quot;happy&quot;, &quot;new&quot;, &quot;year&quot;);
    }
    @Override
    public MyDataType getMyDataType() {
        MyDataType dataType = new MyDataType();
        dataType.setAge(10);
        dataType.setName(&quot;lucy&quot;);
        return dataType;
    }
    @Override
    public List&lt;MyDataType&gt; getMyDataTypeList() {
        MyDataType lucy = new MyDataType();
        lucy.setAge(10);
        lucy.setName(&quot;lucy&quot;);
        MyDataType lily = new MyDataType();
        lily.setAge(11);
        lily.setName(&quot;lily&quot;);
        return Arrays.asList(lucy,lily);
    }
    public static void main(String[] args) throws Exception {
        MBeanServer mBeanServer = ManagementFactory.getPlatformMBeanServer();
        ObjectName name = new ObjectName(&quot;name.chengchao:type=DataType&quot;);
        DataType mbean = new DataType();
        mBeanServer.registerMBean(mbean, name);
        System.out.println(&quot;started...&quot;);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

打开jconsole验证一下,发现有点问题,只要是自定义的类型显示了不可用.看来这条路子是走不通了.google之.发现jmx支持opentype

主要是用到两个类:
CompositeData:支持自定义类型
TabularData:CompositeData集合

对应上面的例子改造一下:  

```java
//MBean接口的改造
public interface DataTypeMBean {

    int getCount();

    List&lt;String&gt; getNames();

    CompositeData getMyDataType() throws Exception;

    TabularData getMyDataTypeList() throws Exception;
}

//实现的改造:
public class DataType implements DataTypeMBean {

    @Override
    public int getCount() {
        return 2014;
    }

    @Override
    public List&lt;String&gt; getNames() {
        return Arrays.asList(&quot;happy&quot;, &quot;new&quot;, &quot;year&quot;);
    }

    @Override
    public CompositeData getMyDataType() throws Exception {
        String[] itemNames = { &quot;name&quot;, &quot;age&quot; };
        OpenType&lt;?&gt;[] openTypes = new OpenType[] { SimpleType.STRING, SimpleType.INTEGER };
        CompositeType compositeType = new CompositeType(&quot;MyDataType&quot;, &quot;my dataType test&quot;, itemNames, itemNames,
                                                        openTypes);
        Object[] items = { &quot;lucy&quot;, 10 };
        CompositeData dataType = new CompositeDataSupport(compositeType, itemNames, items);
        // MyDataType dataType = new MyDataType();
        // dataType.setAge(10);
        // dataType.setName(&quot;lucy&quot;);
        return dataType;
    }

    @Override
    public TabularData getMyDataTypeList() throws Exception{
        String[] itemNames = { &quot;name&quot;, &quot;age&quot; };
        OpenType&lt;?&gt;[] openTypes = new OpenType[] { SimpleType.STRING, SimpleType.INTEGER };
        CompositeType compositeType = new CompositeType(&quot;MyDataType&quot;, &quot;my dataType test&quot;, itemNames, itemNames,
                                                        openTypes);
        TabularType tabularType = new TabularType(&quot;MyDataListType&quot;, &quot;my dataType List test&quot;, compositeType, itemNames);
        TabularData tabularData = new TabularDataSupport(tabularType);
        CompositeData lucy = new CompositeDataSupport(compositeType, itemNames, new Object[]{&quot;lucy&quot;, 10});
        CompositeData lily = new CompositeDataSupport(compositeType, itemNames, new Object[]{&quot;lily&quot;, 11});
        tabularData.put(lucy);
        tabularData.put(lily);
//        MyDataType lucy = new MyDataType();
//        lucy.setAge(10);
//        lucy.setName(&quot;lucy&quot;);
//        MyDataType lily = new MyDataType();
//        lily.setAge(11);
//        lily.setName(&quot;lily&quot;);
        return tabularData;
    }

    public static void main(String[] args) throws Exception {
        MBeanServer mBeanServer = ManagementFactory.getPlatformMBeanServer();
        ObjectName name = new ObjectName(&quot;name.chengchao:type=DataType&quot;);
        DataType mbean = new DataType();
        mBeanServer.registerMBean(mbean, name);
        System.out.println(&quot;started...&quot;);
        Thread.sleep(Long.MAX_VALUE);
    }
}

```
