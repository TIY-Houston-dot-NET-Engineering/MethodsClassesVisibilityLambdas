Notes/Code from Today - Wednesday, October 5th:

```cs
namespace MySpace {
    struct Calc {
        double previousResult;
        string name;
        public void Add(int x, int y) {
            this.previousResult = x+y;
        }
        public void Mult(int x, int y){
            this.previousResult = x*y;
        }
        public void Div(int x, int y){
            this.previousResult = x/y;
        }
    }

    class Calculator {
        double previousResult;
        static string name;
        public void Add(int x, int y) {
            this.previousResult = x+y;
        }
        public void Mult(int x, int y){
            this.previousResult = x*y;
        }
        public void Div(int x, int y){
            this.previousResult = x/y;
        }
    }
}


// int x = 1;
// ...same thing under the hood...
// Int32 x = new Int32(1);
```

```cs
using MySpace;
namespace FaceSpace {
    class BookFace {
        public static void Main(){
            // Calculator.Add -> Error, Add not static
            Calculator tim = new Calculator();
            var bob = new Calculator();
            tim.Add(1,2);
            bob.Mult(4,5);
            tim.previousResult; // 3
            bob.previousResult; // 20

            Calculator.name = "Tim";
            Calculator.name; // "Tim"

            Calc fred = new Calc();
            fred.Add(1,2);
            fred.previousResult; // 3

            int[] x = { 1,2,3 };

            Calculator test1 = new Calculator { previousResult = 1 };
            test1.previousResult; // 1
            // test1.someValue = 2; // Error, not a property of Calculator

            Calc test2 = new Calc { previousResult = 2, name = "Tim" };
            test2.previousResult; // 2
        }
    }
}
```

```cs
class Student {
    private string middle = "A";
    public string first;
    public string getFullName() { return first + middle; }
    public void setFullName(string n){
        string?[] names = n.Split(new char[]{' '});
        first = names?[0] ?? "None";
        middle = names?[1] ?? "__";
    }
    public update(string n) { last = n; }
    public string last {get; private set;}
}
```

```cs
namespace Classroom
{
    struct Student {
        string firstname;
        string lastname;
        public string fullname(){
            return firstname+" "+lastname;
        }
    }

    class Program {
        public static void Main(){
            Student[] students = new Student[50];
            students; // { {firstname="", lastname=""}, ... }

            for(int i = 0; i < 50; i++){
                students[i] = new Student { firstname = i.ToString("Person #") }
            }

            var v = new { Amount = 108, Message = "Hello" }; // read-only
            Console.WriteLine(v.Amount + v.Message);

            Object[] stuff = new Object[50];

            for(int i = 0; i < 50; i++){
                if(i % 2 == 0) {
                    stuff[i] = new { Name = "Matt", placeInLine = i };
                } else {
                    stuff[i] = new { FullName = "Matt", placeInLine = i }; // ERROR, not homogenous
                }
            }
        }
    }
}
```

```cs
namespace FunctionExamples {
    class Example {
        int add(int a, int b){ return a+b; } // BEST
        int add(a, b){ return a+b; } // OK
        int add (int a, int b, int c) => a+b+c; // MATT'S FAV

        void add(int a, int b){ // no return type, so no return statement below
            int c = a+b;
        }

        Func<int, int, int> sum = (a, b) => a+b; // can also set instance properties, which just happen to be lambda expressions
        Action<int, int> sum2 = (a,b) => a+b; // Actions don't return anything, still a lambda expression
    }
}
```

```cs
namespace Calc2 {
    class Calculator {
        public double previousResult { get; private set;}
        Action<int, int> Add = (a,b) => { previousResult = a+b; };
        Action<int, int> Mult = (a,b) => { previousResult = a*b; };
        Action<int, int> Div = (a,b) => { previousResult = a/b; };

        Func<int, int, int> add = (a,b) => a+b;
        int add(int a, int b) => a+b;
    }
}
```