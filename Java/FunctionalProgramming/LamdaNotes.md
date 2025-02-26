# Lambda Notes

## Important Notes about Lambda:
- Lambda expression can access **local variables** only if they are **fina**l or they are **never modified** inside the method.
- Whereas **instance variables** are allowed to be modifed and access inside the lambda.
    - **Example:**  
        ```java        
        class Test {   
            int temp=10;
            public static void main(String[] args) {
                int count = 0;
                mylambda ml=()->{            
                    system.out.println("count"+count); // right  [x]
                    system.out.println("temp"+(++temp)); // right  [x]
                    count ++; // Wrong <span style="color: red;">x</span>
                }
            }
        }
        ```
- Lambda expression can be send as a parameter if the method is taking a functional interfaces as parameter.
    - **Example:**  ` useLambda.callLambda(()->{System.out.println("Hello Lambda");});`
    - **Lambda as parameter:** [code](Code/FunctionalInterface/LamdaExamples/LambdaMultiParamExample.java)
       