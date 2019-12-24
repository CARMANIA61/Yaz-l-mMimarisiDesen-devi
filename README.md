## Yazılım Mimarisi ve Tasarımı


## Builder Tasarım Deseni
Builder Deseninin mantığı adım adım yaklaşımı kullanarak basit nesnelerden karmaşık bir nesne oluşturmaktır.

Çoğunlukla karmaşık bir nesnenin serileştirilmesinde olduğu gibi nesne tek adımda oluşturulamadığında kullanılır.

Builder deseninin ana avantajları şunlardır:

Bir nesnenin yapısı ve temsili arasında açık bir ayrım sağlar.
İnşa süreci üzerinde daha iyi kontrol sağlar.
Nesnelerin iç tasarımını değiştirmeyi destekler.

!
```java
public interface Packing {  
            public String pack();  
            public int price();  
}  


public abstract class CD implements Packing{  
public abstract String pack();  
}  
//Paketleme arabirimini uygulayacak soyut bir sınıf CD'si oluşturun.


public abstract class Company extends CD{  
   public abstract int price();  
}


public class Sony extends Company{  
    @Override  
        public int price(){   
                        return 20;  
      }  
    @Override  
    public String pack(){  
             return "Sony CD";  
        }         
}//Sony sınıfının sonu.  


public class Samsung extends Company {  
    @Override  
        public int price(){   
                        return 15;  
    }  
    @Override  
    public String pack(){  
             return "Samsung CD";  
        }         
}//Samsung sınıfının sonu. 


import java.util.ArrayList;  
import java.util.List;  
public class CDType {  
             private List<Packing> items=new ArrayList<Packing>();  
             public void addItem(Packing packs) {    
                    items.add(packs);  
             }  
             public void getCost(){  
              for (Packing packs : items) {  
                        packs.price();  
              }   
             }  
             public void showItems(){  
              for (Packing packing : items){  
             System.out.print("CD name : "+packing.pack());  
             System.out.println(", Price : "+packing.price());  
          }       
            }     
}//CDType sınıfının sonu.  


public class CDBuilder {  
                  public CDType buildSonyCD(){   
                     CDType cds=new CDType();  
                     cds.addItem(new Sony());  
                     return cds;  
              }  
              public CDType buildSamsungCD(){  
             CDType cds=new CDType();  
             cds.addItem(new Samsung());  
             return cds;  
              }  
}//CDBuilder sınıfının sonu.


public class BuilderDemo{  
 public static void main(String args[]){  
   CDBuilder cdBuilder=new CDBuilder();  
   CDType cdType1=cdBuilder.buildSonyCD();  
   cdType1.showItems();  
  
   CDType cdType2=cdBuilder.buildSamsungCD();  
   cdType2.showItems();  
 }  
}  


/* Çıktı örneği:
CD name : Sony CD, Price : 20  
CD name : Samsung CD, Price : 15   */

```
