```java
package com.atguigu.test1;

/**
 * 1.编写Order类，有int型的orderId，String型的OrderName，相应的getter()和setter()方法，两个参数的构	造器，
 * 重写父类的equals()方法：public boolean equals(Object obj)，并判断测试类中创建的两个对象是否相等。
 */
public class Order {
	private int orderId;
	private String orderName;

	public int getOrderId() {
		return orderId;
	}

	public void setOrderId(int orderId) {
		this.orderId = orderId;
	}

	public String getOrderName() {
		return orderName;
	}

	public void setOrderName(String orderName) {
		this.orderName = orderName;
	}

	public Order() {
		super();
	}

	public Order(int orderId, String orderName) {
		super();
		this.orderId = orderId;
		this.orderName = orderName;
	}

	/**
	 * 重写Object类的equals方法:(默认的 equals方法：)
	 * public boolean equals(Object obj) { 
	 * 		return (this == obj); 
	 * }
	 */
	public boolean equals(Object obj) {
		// 判断传入的obj 是否为一个地址：
		if (this == obj)
			return true;

		// 判断传入的obj是否为this的同一个类型：
		if (!(obj instanceof Order))
			return false;

		// 判断传入的是目标类型，再进行强转后判断具体的值 ：
		return orderId == ((Order) obj).getOrderId()
				&& orderName.equals(((Order) obj).getOrderName());
	}

	// 重写Object类的toString方法：
	/**
	 * 默认的Object类的toString方法： public String toString() { return
	 * getClass().getName() + "@" + Integer.toHexString(hashCode()); }
	 */
	public String toString() {
		return "订单号：" + orderId + " 订单名：" + orderName;
	}
}
```

