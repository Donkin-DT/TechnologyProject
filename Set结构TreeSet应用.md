###### Set结构TreeSet应用

main

```java
package com.atguigu.test2;

import java.util.TreeSet;

public class Test {
	public static void main(String[] args) {
		TreeSet<Employee> employees = new TreeSet<Employee>();

		employees.add(new Employee("小刚", new MyDate(1991, 9, 18)));
		employees.add(new Employee("小红", new MyDate(1995, 7, 1)));
		employees.add(new Employee("小强", new MyDate(1997, 12, 8)));
		employees.add(new Employee("小强", new MyDate(1997, 12, 9)));
		employees.add(new Employee("小刚", new MyDate(1991, 9, 18)));
		employees.add(new Employee("小刚", new MyDate(1991, 8, 18)));

		for (Employee employee : employees) {
			System.out.println(employee);
		}
	}
}
```

Employee

```java
class Employee implements Comparable<Employee> {
	private String name;
	private MyDate birthday;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public MyDate getBirthday() {
		return birthday;
	}

	public void setBirthday(MyDate birthday) {
		this.birthday = birthday;
	}

	public Employee() {
		super();
	}

	public Employee(String name, MyDate birthday) {
		super();
		this.name = name;
		this.birthday = birthday;
	}

	@Override
	public String toString() {
		return "姓名： " + name + " 生日：" + birthday;
	}

	@Override
	public int compareTo(Employee o) {
		if(name.compareTo(o.name) != 0)return name.compareTo(o.name);
		return this.birthday.compareTo(o.getBirthday());
	}
}
```

MyDate

```java
class MyDate implements Comparable<MyDate>{
	private int year;
	private int month;
	private int day;

	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	public int getMonth() {
		return month;
	}

	public void setMonth(int month) {
		this.month = month;
	}

	public int getDay() {
		return day;
	}

	public void setDay(int day) {
		this.day = day;
	}

	public MyDate() {
		super();
	}

	public MyDate(int year, int month, int day) {
		super();
		this.year = year;
		this.month = month;
		this.day = day;
	}
    
	@Override
	public String toString() {
		return "年：" + year + " 月" + month + " 日" + day;
	}
    
	@Override
	public int compareTo(MyDate o) {
		if(Integer.compare(year, o.year) != 0) return Integer.compare(year, o.year);
		if(Integer.compare(month, o.month) != 0) return Integer.compare(month, o.month);
		return Integer.compare(day, o.day);
	}
}
```

Console

```java
姓名： 小刚 生日：年：1991 月8 日18
姓名： 小刚 生日：年：1991 月9 日18
姓名： 小强 生日：年：1997 月12 日8
姓名： 小强 生日：年：1997 月12 日9
姓名： 小红 生日：年：1995 月7 日1
```

