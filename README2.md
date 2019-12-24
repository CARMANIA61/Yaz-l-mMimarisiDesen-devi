## Yazılım Mimarisi ve Tasarımı


## Durum Deseni

Bir Durum Düzeni "sınıf davranışının durumuna göre değiştiğini" söyler. Durum Deseni'nde, çeşitli durumları temsil eden nesneler ve durum nesnesi değiştikçe davranışı değişen bir bağlam nesnesi oluştururuz.

Yararları:
Duruma özgü davranışı korur.
Herhangi bir durum geçişini açık hale getirir.

Kullanımı:
Nesnenin davranışı durumuna bağlı olduğunda ve çalışma zamanındaki davranışını yeni duruma göre değiştirebiliyor olmalıdır.
İşlemler, bir nesnenin durumuna bağlı olan büyük, çok parçalı koşullu ifadelere sahip olduğunda kullanılır.

```java

public interface Connection {  
  
       public void open();  
       public void close();  
       public void log();  
       public void update();  
}//Interface bağlantısının sonu.  


public class Accounting implements Connection {  
      
       @Override  
       public void open() {  
          System.out.println("muhasebe için açık veritabanı");  
       }  
       @Override  
       public void close() {  
          System.out.println("veritabanını kapat");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("giriş aktiviteleri");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("muhasebe güncellendi");  
       }  
}//Accounting sınıfının sonu. 


public class Sales implements Connection {  
      
      @Override  
       public void open() {  
          System.out.println("satışlar için açık veritabanı");  
       }  
       @Override  
       public void close() {  
          System.out.println("veritabanını kapat");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("giriş aktiviteleri");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("satışlar güncellendi");  
       }  
  
}// Sales sınıfının sonu.  


public class Management implements Connection {  
      
      @Override  
       public void open() {  
          System.out.println("yönetim için açık veritabanı");  
       }  
       @Override  
       public void close() {  
          System.out.println("veritabanını kapat");  
       }  
         
       @Override  
       public void log() {  
          System.out.println("giriş aktiviteleri");  
       }  
         
       @Override  
       public void update() {  
           System.out.println("yönetim güncellendi");  
       }  
  
}  
 //Management sınıfının sonu.  



public class Controller {  
      
       public static Accounting acct;  
       public static Sales sales;  
       public static Management management;  
         
       private static Connection con;  
         
       Controller() {  
           acct = new Accounting();  
           sales = new Sales();  
           management = new Management();  
       }  
      
       public void setAccountingConnection() {  
           con = acct;  
       }  
       public void setSalesConnection() {  
           con  = sales;  
       }  
       public void setManagementConnection() {  
           con  = management;  
       }  
       public void open() {  
           con .open();  
       }  
       public void close() {  
           con .close();  
       }  
       public void log() {  
           con .log();  
       }  
       public void update() {  
           con .update();  
       }  
         
}//Controller sınıfının sonu.  



public class StatePattern {  
  
       Controller controller;  
       StatePatternDemo(String con) {  
          controller = new Controller();  
          //kullanıcı tarafından aşağıdaki seçim yapılmalıdır.  
          if(con.equalsIgnoreCase("yönetim"))  
             controller.setManagementConnection();  
          if(con.equalsIgnoreCase("satışlar"))  
             controller.setSalesConnection();  
          if(con.equalsIgnoreCase("muhasebe"))  
                 controller.setAccountingConnection();  
          controller.open();  
          controller.log();  
          controller.close();  
          controller.update();  
       }  
         
         
       public static void main(String args[]) {  
  
           new StatePatternDemo(args[0]);  
             
       }  
  
}//StatePattern sınıfının sonu. 










































