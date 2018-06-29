##### java获取当前系统日期和时间
```java
import java.util.Date;
import java.text.SimpleDateFormat;

public class NowString {
    public static void main(String[] args) { 
        SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//设置日期格式
        System.out.println(df.format(new Date()));// new Date()为获取当前系统时间
    }
}

//java中获取当前日期和时间的方法
    Calendar c = Calendar.getInstance();//可以对每个时间域单独修改

    int year = c.get(Calendar.YEAR); 
    int month = c.get(Calendar.MONTH); 
    int date = c.get(Calendar.DATE); 
    int hour = c.get(Calendar.HOUR_OF_DAY); 
    int minute = c.get(Calendar.MINUTE); 
    int second = c.get(Calendar.SECOND); 
    System.out.println(year + "/" + month + "/" + date + " " +hour + ":" +minute + ":" + second); 

// 获取系统当前毫秒数
System.currentTimeMillis()
    
// 给当前时间添加若干分钟/小时
SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss");
Timestamp timestamp = new Timestamp(System.currentTimeMillis());
timestamp.setHours(timestamp.getHours() + 1);
System.out.println(timestamp);

Calendar calendar = Calendar.getInstance();
calendar.set(calendar.HOUR_OF_DAY, calendar.get(calendar.HOUR_OF_DAY) + 1);
System.out.println(sdf.format(calendar.getTime()));
```

