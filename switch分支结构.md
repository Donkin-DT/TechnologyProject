##### switch分支结构

```java
import java.util.Scanner;

public class Test4{
	public static void main(String[] args){
		Scanner input = new Scanner(System.in);
		
		//1、輸入一個成績，大於60的爲及格，小於60的爲不及格。這個數字除于60就衹有兩種，1或0.
		System.out.println("請輸入你的成績：");
		double score = input.nextDouble();
		switch((int)score/60){					 //switch:注意：s 是小寫的。
			case 1:System.out.println("合格");break;
			case 0:System.out.println("不合格");break;
		}
		
		//2、輸入一個月份，判斷是哪個季節
		/*System.out.println("請輸入月份：");
		int month = input.nextInt();
		switch(month){							 //switch 中前面的s是小寫的，注意格式
			case 3:
			case 4:
			case 5:System.out.println("春季");break;//注意格式
			case 6:
			case 7:
			case 8:System.out.println("夏季");break;
			case 9:
			case 10:
			case 11:System.out.println("秋季");break;
			case 1:
			case 2:
			case 12:System.out.println("冬季");break;
			default:System.out.println("月份輸入錯誤！");
		}*/
	}
}
```

