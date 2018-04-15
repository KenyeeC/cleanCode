### bad case
```java
public Money calculatePay(Employee e) thorws InvalidEmployeeType {  
  switch(e.type)  {  
    case COMMISSIONED:  
      return calculateCommissionedPay(e);  
    case HOURLY:  
      return calculateHourlyPay(e);  
    case SALARIED:  
      return calculateSalariedPay(e);  
    default:  
      throw new InvalidEmployeeType(e.type);  
  }  
```

### good case
```java
public interface Employee{  
  public boolean isPayday();  
  public Money calculatePay();  
  public void deliverPay(Money pay);  
}  
public interface EmployeeFactory{  
  public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;  
}  
public class EmployeeFactoryImpl implements EmployeeFactory{  
  public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType{  
    switch(r.type){  
    case COMMISSIONED:  
      return new CommissionedEmployee(r);  
    case HOURLY:  
      return new HourlyEmployee(r);  
    case SALARIED:  
      return new SalariedEmployee(r);  
    default:  
      throw new InvalidEmployeeType(r.type);  
    }  
  }  
}  
```