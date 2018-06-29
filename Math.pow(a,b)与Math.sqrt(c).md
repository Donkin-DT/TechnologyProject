##### Math.pow(a,b)与Math.sqrt(c)

```java
import java.util.Scanner;
/*
Math.pow(a,b):求a的b次幂
Math.sqrt(c):求c的算术平方根
*/
public class Test2{
	public static void main(String[] args){
		Scanner input = new Scanner(System.in);
		System.out.println("请输入一个数a：");
		double a = input.nextDouble();
		System.out.println("请输入一个数b：");
		double b = input.nextDouble();
		System.out.println("请输入一个数c：");
		double c = input.nextDouble();
		//方程：ax^2 + bx + c = 0;
		double result = b*b - 4*a*c;
		if(result > 0){
			double x1 = (-b+Math.sqrt(result))/2 * a;
			double x2 = (-b-Math.sqrt(result))/2 * a;
			System.out.printf("方程：ax^2 + bx + c = 0 有两个不同的实数根" + "x1= " + x1 + " x2= " + x2 );
		}else if(result == 0){
			double x1 = (-b+Math.sqrt(result))/2 * a; //此处一样可以定义x1，因为变量的作用范围在一对大括号内。
			System.out.printf("方程：ax^2 + bx + c = 0 有两个相同的实数根"  + "x1 = x2= " + x1);
		}else{
			System.out.println("方程：ax^2 + bx + c = 0 没有实数根");
		}
 	}
}
```

