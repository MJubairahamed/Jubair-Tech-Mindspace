# Lambda Notes

- Lambda expression can access **local variables** only if they are **fina**l or they are **never modified** inside the method.
- Whereas **instance variables** are allowed to be modifed and access inside the lambda.
    - **Example:**  
        ```java        
        class Test {   
            int temp=10;
            public static void main(String[] args) {
                int count = 0;
                mylambda ml=()->{ 
                    int i=o;
                    system.out.println("i"+(++i)); // right  ✅                              
                    system.out.println("temp"+(++temp)); // right  ✅
                    count ++; // Wrong ❌
                }
            }
        }
        ```
- Lambda expression can be send as a parameter if the method is taking a functional interfaces as parameter.
    - **Example:**  ` useLambda.callLambda(()->{System.out.println("Hello Lambda");});`
    - **Lambda as parameter:** [code](https://github.com/MJubairahamed/JavaLearningCodeRepo/blob/main/Code/FunctionalInterface/LamdaExamples/LambdaMultiParamExample.java)
       