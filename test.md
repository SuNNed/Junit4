#  package com.mikuscallion.main;  

2.   

3. import static org.junit.Assert.*;  

4.   

5. import org.junit.After;  

6. import org.junit.AfterClass;  

7. import org.junit.Before;  

8. import org.junit.BeforeClass;  

9. import org.junit.Ignore;  

10. import org.junit.Test;  

11. public class CalculatorTest {  

12.     //测试对象  

13.     Calculator calculator =new Calculator();  

14.     //Fixture  

15.     @BeforeClass  

16.     public static void beforeClass(){  

17.         System.out.println("在测试类初始化时，调用一次");  

18.     }  

19.     @AfterClass  

20.     public static void afterClass(){  

21.         System.out.println("在测试类运行结束时，调用一次");  

22.     }  

23.     @Before  

24.     public void before(){  

25.         System.out.println("执行任何测试代码前调用");  

26.         calculator.clear();  

27.     }  

28.     @After  

29.     public void after(){  

30.         System.out.println("执行任何测试代码后调用");  

31.     }  

32.     //Test---------------------------------------------------------------------------------  

33.     @Ignore  

34.     //忽视测试  

35.     public void testMultiply() {  

36.         calculator.multiply(1);  

37.         calculator.multiply(5);  

38.         //断言结果  

39.         assertEquals(5, calculator.getResult());  

40.     }  

41.     @Test(timeout = 1000)  

42.     //限时测试   

43.     public void limitTimeTest(){  

44.         calculator.squareRoot(5);  

45.     }  

46.     @Test(expected = ArithmeticException.class)  

47.     //异常测试  

48.     public void exceptTest(){  

49.         calculator.divide(0);  

50.     }  

51.     @Test  

52.     public void testAdd() {  

53.         calculator.add(1);  

54.         calculator.add(2);  

55.         assertEquals(3, calculator.getResult());  

56.     }  

57.     @Test  

58.     public void testSubstract() {  

59.         calculator.add(10);  

60.         calculator.substract(2);  

61.         assertEquals(8, calculator.getResult());  

62.     }  

63.     @Test  

64.     public void testDivide() {  

65.         calculator.add(8);  

66.         calculator.divide(2);  

67.         assertEquals(4, calculator.getResult());  

68.     }  

69.       

70. }  

 

④参数测试代码

[java] view plain

copy

1. package com.mikuscallion.main;  

2.   

3. import static org.junit.Assert.*;  

4.   

5. import java.util.Arrays;  

6. import java.util.Collection;  

7.   

8. import org.junit.Test;  

9. import org.junit.runner.RunWith;  

10. import org.junit.runners.Parameterized;  

11. import org.junit.runners.Parameterized.Parameters;  

12.   

13. @RunWith(Parameterized.class)  

14. public class SquareTest {  

15.     public Calculator calculator =new Calculator();  

16.     public int param;  

17.     public int result;  

18.       

19.     @Parameters  

20.     public static Collection data(){  

21.         //注意这种写法  

22.         return Arrays.asList(new Object[][]{  

23.                 {2, 4},  

24.                 {0, 0},  

25.                 {-3, 9},  

26.         });  

27.     }  

28.     public SquareTest(int param, int result){  

29.         this.param = param;  

30.         this.result = result;  

31.     }  

32.     @Test  

33.     public void testSquare() {  

34.         calculator.square(param);  

35.         assertEquals(result, calculator.getResult());  

36.     }  

37. }  

⑤批量测试代码

[java] view plain

copy

1. package com.mikuscallion.main;  

2.   

3.   

4. import org.junit.runner.RunWith;  

5. import org.junit.runners.Suite;  

6. import org.junit.runners.Suite.SuiteClasses;  

7. @SuiteClasses({  

8.     SquareTest.class,  

9.     CalculatorTest.class,  

10. })  

11. @RunWith(Suite.class)  

12. public class SuiteTest {  

13.       

14. }  

⑥被测试类代码

[java] view plain

copy

1. package com.mikuscallion.main;  

2. public class Calculator {  

3.           

4.         private static int result; // 静态变量，用于存储运行结果  

5.           

6.         public void add(int n){  

7.             result = result + n;  

8.         }  

9.         public void substract(int n){  

10.             result = result - n; //Bug: 正确的应该是 result =result-n  

11.         }  

12.         public void multiply(int n){  

13.         } // 此方法尚未写好  

14.         public void divide(int n){  

15.         result = result / n;  

16.         }  

17.           

18.         //  

19.         public void square(int n){  

20.             result = n * n;  

21.         }  

22.         public void squareRoot(int n){  

23.             for (; ;) ; //Bug : 死循环  

24.         }  

25.         public void clear(){ // 将结果清零  

26.             result = 0;  

27.         }  

28.         public int getResult(){  

29.             return result;  

30.         }  

31. }   
