###### Set接口HashSet应用

```java
package com.atguigu.test1;

import java.util.HashSet;

/**
 * 定义一个Employee类， 该类包含：private成员变量name, birthday，其中 birthday 为 MyDate类的对象；
 * 并为每一个属性定义 getter, setter 方法； 并重写 toString 方法输出 name, age, birthday 认为
 * name和birthday一样的为同一个员工
 * 
 * @author Administrator
 *
 */
public class Test {
	public static void main(String[] args) {
		HashSet<Employee> employees = new HashSet<Employee>();
		
		employees.add(new Employee("小刚",new MyDate(1991,9,18)));
		employees.add(new Employee("小红",new MyDate(1995,7,1)));
		employees.add(new Employee("小强",new MyDate(1997,12,8)));
		employees.add(new Employee("小刚",new MyDate(1991,9,18)));
		
		for (Employee employee : employees) {
			System.out.println(employee);
		}
	}
}
```

Employee

```java
class Employee{
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
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((birthday == null) ? 0 : birthday.hashCode());
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}
	
	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Employee other = (Employee) obj;
		if (birthday == null) {
			if (other.birthday != null)
				return false;
		} else if (!birthday.equals(other.birthday))
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}
}
```

MyDate

```java
class MyDate {
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
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + day;
		result = prime * result + month;
		result = prime * result + year;
		return result;
	}
    
	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		MyDate other = (MyDate) obj;
		if (day != other.day)
			return false;
		if (month != other.month)
			return false;
		if (year != other.year)
			return false;
		return true;
	}
}
```

employees

```java
姓名： 小强 生日：年：1997 月12 日8
姓名： 小红 生日：年：1995 月7 日1
姓名： 小刚 生日：年：1991 月9 日18
```



