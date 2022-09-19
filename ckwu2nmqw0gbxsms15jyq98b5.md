## Most Frequently asked Java Streams coding answers - Part 2 - Object

Hey Guys,

Welcome back to my blog.

Note: Please give me credits before re sharing this article. You can mention my LinkedIn profile  [Shiva Prasad Gurram](https://www.linkedin.com/in/shivaprasadgurram/) 

In my last article I provided answers for **Input - 1** questions, In this article I'm going to provide answers for **Input - 2** questions. You can find questions list at below link.

**Questions:**  [Most Frequently asked Java Streams coding questions - Part 1](https://shivaprasadgurram.hashnode.dev/most-frequently-asked-java-streams-coding-questions-part-1) 

# Input - 2

Given an **Employee** class which consists below properties. There may be one or more employees who works for a single organization but in different departments.

**Employee Class**


```
public class Employee {

    private int emp_id;
    private String emp_name;
    private int emp_age;
    private String emp_gender;
    private String emp_dept;
    private int emp_doj;
    private double emp_salary;

    public Employee(int emp_id, String emp_name, int emp_age, String emp_gender, 
    String emp_dept, int emp_doj, double emp_salary) {
        this.emp_id = emp_id;
        this.emp_name = emp_name;
        this.emp_age = emp_age;
        this.emp_gender = emp_gender;
        this.emp_dept = emp_dept;
        this.emp_doj = emp_doj;
        this.emp_salary = emp_salary;
    }

    public int getEmp_id() {
        return emp_id;
    }

    public String getEmp_name() {
        return emp_name;
    }

    public int getEmp_age() {
        return emp_age;
    }

    public String getEmp_gender() {
        return emp_gender;
    }

    public String getEmp_dept() {
        return emp_dept;
    }

    public int getEmp_doj() {
        return emp_doj;
    }

    public double getEmp_salary() {
        return emp_salary;
    }

   @Override
    public String toString() {
        return "Employee{" +
                "emp_id=" + emp_id +
                ", emp_name='" + emp_name + '\'' +
                ", emp_age=" + emp_age +
                ", emp_gender='" + emp_gender + '\'' +
                ", emp_dept='" + emp_dept + '\'' +
                ", emp_doj=" + emp_doj +
                ", emp_salary=" + emp_salary +
                '}';
    }
}
``` 

**Main Class**

```
public class StreamsQuestionsAnswers2 {

    static List<Employee> employeeList = new ArrayList<Employee>();
    
    public static void main(String[] args) {

        employeeList.add(new Employee(111, "Jiya Brein", 32, "Female", "HR", 2011, 25000.0));
        employeeList.add(new Employee(122, "Paul Niksui", 25, "Male", "Sales And Marketing", 2015, 13500.0));
        employeeList.add(new Employee(133, "Martin Theron", 29, "Male", "Infrastructure", 2012, 18000.0));
        employeeList.add(new Employee(144, "Murali Gowda", 28, "Male", "Product Development", 2014, 32500.0));
        employeeList.add(new Employee(155, "Nima Roy", 27, "Female", "HR", 2013, 22700.0));
        employeeList.add(new Employee(166, "Iqbal Hussain", 43, "Male", "Security And Transport", 2016, 10500.0));
        employeeList.add(new Employee(177, "Manu Sharma", 35, "Male", "Account And Finance", 2010, 27000.0));
        employeeList.add(new Employee(188, "Wang Liu", 31, "Male", "Product Development", 2015, 34500.0));
        employeeList.add(new Employee(199, "Amelia Zoe", 24, "Female", "Sales And Marketing", 2016, 11500.0));
        employeeList.add(new Employee(200, "Jaden Dough", 38, "Male", "Security And Transport", 2015, 11000.5));
        employeeList.add(new Employee(211, "Jasna Kaur", 27, "Female", "Infrastructure", 2014, 15700.0));
        employeeList.add(new Employee(222, "Nitin Joshi", 25, "Male", "Product Development", 2016, 28200.0));
        employeeList.add(new Employee(233, "Jyothi Reddy", 27, "Female", "Account And Finance", 2013, 21300.0));
        employeeList.add(new Employee(244, "Nicolus Den", 24, "Male", "Sales And Marketing", 2017, 10700.5));
        employeeList.add(new Employee(255, "Ali Baig", 23, "Male", "Infrastructure", 2018, 12700.0));
        employeeList.add(new Employee(266, "Sanvi Pandey", 26, "Female", "Product Development", 2015, 28900.0));
        employeeList.add(new Employee(277, "Anuj Chettiar", 31, "Male", "Product Development", 2012, 35700.0));

    }
}
``` 

# Answers

**1) How many male and female employees are there in the organization?**

**Approach:**  We can use **Collectors.groupingBy** to group the employees based upon their gender.


```
Map<String, Long> noOfFemaleAndMaleEmployees = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_gender,Collectors.counting()));
System.out.println("No.of Females and Males: "+noOfFemaleAndMaleEmployees);
``` 

output

```
No.of Females and Males: {Male=11, Female=6}
``` 

**2) Print the name of all departments in the organization.**

**Approach: ** We can use **map()** to get only department names. I'm going to use **Set** because I want to display only unique department names.


```
Set<String> departmentNames = employeeList.stream().map(emp -> emp.getEmp_dept()).collect(Collectors.toSet());
System.out.println("Department Names: "+departmentNames);
``` 

output

```
Department Names: [Product Development, Sales And Marketing, Security And Transport, Infrastructure, HR, Account And Finance]
``` 

**3) What is the average age of male and female employees?**

**Approach: ** We can use **Collectors.groupingBy** and **Collectors.averagingInt** to get average based on genders.


```
Map<String, Double> avgAgeOfFemaleAndMaleEmployees = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_gender,Collectors.averagingInt(Employee::getEmp_age)));
System.out.println("Average age of male and female employees: "+avgAgeOfFemaleAndMaleEmployees);
``` 

output

```
Average age of male and female employees: {Male=30.181818181818183, Female=27.166666666666668}
``` 

**4) Get the details of highest paid employee in the organization**

**Approach: ** We can use **Collectors.maxBy** and **Comparator.comparingDouble** to compare the salaries and get max.


```
Optional<Employee> highestPaidEmployee = employeeList.stream().collect(Collectors.maxBy(Comparator.comparingDouble(Employee::getEmp_salary)));
System.out.println("Highest paid employee: " +highestPaidEmployee);
``` 

output

```
Highest paid employee: Optional[Employee{emp_id=277, emp_name='Anuj Chettiar', emp_age=31, emp_gender='Male', emp_dept='Product Development', emp_doj=2012, emp_salary=35700.0}]

``` 

**5) Get the names of all employees who have joined after 2015**

**Approach: ** We can use **filter()** and **map()** to filter the employees based on their DOJ and get only names.


```
List<String> whoJoinedAfter2015 = employeeList.stream().filter(emp -> emp.getEmp_doj()>2015).map(Employee::getEmp_name).collect(Collectors.toList());
System.out.println("Employees who joined after 2015: " + whoJoinedAfter2015);
``` 

output

```
Employees who joined after 2015: [Iqbal Hussain, Amelia Zoe, Nitin Joshi, Nicolus Den, Ali Baig]
``` 

**6) Count the number of employees in each department**

**Approach: ** We can use **Collectors.groupingBy** and **Collectors.counting** to group employees based on department and count.

```
Map<String, Long> noOfEmployeesInEachDepartment = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_dept,Collectors.counting()));
System.out.println("Employees in each department: "+ noOfEmployeesInEachDepartment);
``` 

output

```
Employees in each department: {Product Development=5, Security And Transport=2, Sales And Marketing=3, Infrastructure=3, HR=2, Account And Finance=2}
``` 

**7) What is the average salary of each department?**

**Approach: ** We can use **Collectors.groupingBy** and **Collectors.averagingDouble** to group employees by their department and get average.

```
Map<String, Double> avgSalaryOfEachDepartment = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_dept,Collectors.averagingDouble(Employee::getEmp_salary)));
System.out.println("Average salary of each department: "+ avgSalaryOfEachDepartment);
``` 

output

```
Average salary of each department: {Product Development=31960.0, Security And Transport=10750.25, Sales And Marketing=11900.166666666666, Infrastructure=15466.666666666666, HR=23850.0, Account And Finance=24150.0}
``` 

**8) Who has the most working experience in the organization?**

**Approach: ** We can do this in 2 ways

- Using **min()**

- Using **sorted()**

**Way1: **

```
Optional<Employee> mostWorkingExperience = employeeList.stream().min(Comparator.comparingInt(Employee::getEmp_doj));
System.out.println("Most working experience: "+mostWorkingExperience);
``` 

output

```
Most working experience: Optional[Employee{emp_id=177, emp_name='Manu Sharma', emp_age=35, emp_gender='Male', emp_dept='Account And Finance', emp_doj=2010, emp_salary=27000.0}]
``` 

**Way2: **

```
Optional<Employee> mostWorkingExperience2 = employeeList.stream().sorted(Comparator.comparing(Employee::getEmp_doj)).findFirst();
System.out.println("Most working experience: "+mostWorkingExperience2);
``` 

output

```
Most working experience: Optional[Employee{emp_id=177, emp_name='Manu Sharma', emp_age=35, emp_gender='Male', emp_dept='Account And Finance', emp_doj=2010, emp_salary=27000.0}]
``` 

**9) Get the details of youngest male employee in the each department.**

**Approach: ** Here we need to do 3 things

- filter the employees based on gender(male)
- group them based on department(groupingBy method) on filtered data
- use maxBy to compare their DOJ.

```
Map<String, Optional<Employee>> youngestEmployeesInEachDept = employeeList.stream().filter(e->e.getEmp_gender()=="Male").collect(Collectors.groupingBy(Employee::getEmp_dept,Collectors.maxBy(Comparator.comparingInt(Employee::getEmp_doj))));
System.out.println("Youngest employee in each department: "+ youngestEmployeesInEachDept);
``` 

output

```
Youngest employee in each department: {Product Development=Optional[Employee{emp_id=222, emp_name='Nitin Joshi', emp_age=25, emp_gender='Male', emp_dept='Product Development', emp_doj=2016, emp_salary=28200.0}], Security And Transport=Optional[Employee{emp_id=166, emp_name='Iqbal Hussain', emp_age=43, emp_gender='Male', emp_dept='Security And Transport', emp_doj=2016, emp_salary=10500.0}], Sales And Marketing=Optional[Employee{emp_id=244, emp_name='Nicolus Den', emp_age=24, emp_gender='Male', emp_dept='Sales And Marketing', emp_doj=2017, emp_salary=10700.5}], Infrastructure=Optional[Employee{emp_id=255, emp_name='Ali Baig', emp_age=23, emp_gender='Male', emp_dept='Infrastructure', emp_doj=2018, emp_salary=12700.0}], Account And Finance=Optional[Employee{emp_id=177, emp_name='Manu Sharma', emp_age=35, emp_gender='Male', emp_dept='Account And Finance', emp_doj=2010, emp_salary=27000.0}]}
``` 


**10) What is the average salary and total salary of the whole organization?**

**Approach: ** We can use **DoubleSummaryStatistics** class to get complete statistics of employees based on their salary.

```
DoubleSummaryStatistics employeesTotalandAvgSalary = employeeList.stream().collect(Collectors.summarizingDouble(Employee::getEmp_salary));
System.out.println("Average Salary of organization:  " + employeesTotalandAvgSalary.getAverage());
System.out.println("Total Salary of organization:  "+employeesTotalandAvgSalary.getSum());
``` 

output

```
Average Salary of organization:  21141.235294117647
Total Salary of organization:  359401.0
``` 

**11) Separate the employees who are younger or equal to 25 years from those employees who are older than 25 years**

**Approach: ** We can use **Collectors.partitioningBy** to partition a collection based on a condition.

```
Map<Boolean, List<Employee>> partitionByAge = employeeList.stream().collect(Collectors.partitioningBy(e->e.getEmp_age() > 25));
System.out.println("Partitioned employees: "+partitionByAge);
``` 

output

```
Partitioned employees: {false=[Employee{emp_id=122, emp_name='Paul Niksui', emp_age=25, emp_gender='Male', emp_dept='Sales And Marketing', emp_doj=2015, emp_salary=13500.0}, Employee{emp_id=199, emp_name='Amelia Zoe', emp_age=24, emp_gender='Female', emp_dept='Sales And Marketing', emp_doj=2016, emp_salary=11500.0}, Employee{emp_id=222, emp_name='Nitin Joshi', emp_age=25, emp_gender='Male', emp_dept='Product Development', emp_doj=2016, emp_salary=28200.0}, Employee{emp_id=244, emp_name='Nicolus Den', emp_age=24, emp_gender='Male', emp_dept='Sales And Marketing', emp_doj=2017, emp_salary=10700.5}, Employee{emp_id=255, emp_name='Ali Baig', emp_age=23, emp_gender='Male', emp_dept='Infrastructure', emp_doj=2018, emp_salary=12700.0}], true=[Employee{emp_id=111, emp_name='Jiya Brein', emp_age=32, emp_gender='Female', emp_dept='HR', emp_doj=2011, emp_salary=25000.0}, Employee{emp_id=133, emp_name='Martin Theron', emp_age=29, emp_gender='Male', emp_dept='Infrastructure', emp_doj=2012, emp_salary=18000.0}, Employee{emp_id=144, emp_name='Murali Gowda', emp_age=28, emp_gender='Male', emp_dept='Product Development', emp_doj=2014, emp_salary=32500.0}, Employee{emp_id=155, emp_name='Nima Roy', emp_age=27, emp_gender='Female', emp_dept='HR', emp_doj=2013, emp_salary=22700.0}, Employee{emp_id=166, emp_name='Iqbal Hussain', emp_age=43, emp_gender='Male', emp_dept='Security And Transport', emp_doj=2016, emp_salary=10500.0}, Employee{emp_id=177, emp_name='Manu Sharma', emp_age=35, emp_gender='Male', emp_dept='Account And Finance', emp_doj=2010, emp_salary=27000.0}, Employee{emp_id=188, emp_name='Wang Liu', emp_age=31, emp_gender='Male', emp_dept='Product Development', emp_doj=2015, emp_salary=34500.0}, Employee{emp_id=200, emp_name='Jaden Dough', emp_age=38, emp_gender='Male', emp_dept='Security And Transport', emp_doj=2015, emp_salary=11000.5}, Employee{emp_id=211, emp_name='Jasna Kaur', emp_age=27, emp_gender='Female', emp_dept='Infrastructure', emp_doj=2014, emp_salary=15700.0}, Employee{emp_id=233, emp_name='Jyothi Reddy', emp_age=27, emp_gender='Female', emp_dept='Account And Finance', emp_doj=2013, emp_salary=21300.0}, Employee{emp_id=266, emp_name='Sanvi Pandey', emp_age=26, emp_gender='Female', emp_dept='Product Development', emp_doj=2015, emp_salary=28900.0}, Employee{emp_id=277, emp_name='Anuj Chettiar', emp_age=31, emp_gender='Male', emp_dept='Product Development', emp_doj=2012, emp_salary=35700.0}]}

``` 

**12) Who is the oldest employee in the organization? What is his age and which department he belongs to?**

**Approach: ** We can use **max** to get oldest employee details.

```
Optional<Employee> oldestEmployee = employeeList.stream().max(Comparator.comparingInt(Employee::getEmp_age));
System.out.println("Oldest employee in organization: "+ oldestEmployee.get().getEmp_name() +"  "+oldestEmployee.get().getEmp_age()+"  "+oldestEmployee.get().getEmp_dept());
 
``` 

output

```
Oldest employee in organization: Iqbal Hussain  43  Security And Transport
``` 

**13) Find the second highest salary employee details**

**Approach: ** We can use **sorted** to sort in DESC order and use **skip()** to skip first employee, So that we can get second.

```
Optional<Employee> secondHighestSalaryEmployee = employeeList.stream().sorted(Comparator.comparingDouble(Employee::getEmp_salary).reversed()).skip(1).findFirst();
System.out.println("Second Highest Salary Employee: "+secondHighestSalaryEmployee.get());
``` 

output

```
Second Highest Salary Employee: Employee{emp_id=188, emp_name='Wang Liu', emp_age=31, emp_gender='Male', emp_dept='Product Development', emp_doj=2015, emp_salary=34500.0}
``` 

**14) Get the maximum salary of an employee from each department**

**Approach: ** We can use **Collectors.groupingBy** and **Collectors.maxBy** to group them and get max.


```
 Map<String, Optional<Employee>> departmentWiseMaxSalary = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_dept,Collectors.maxBy(Comparator.comparingDouble(Employee::getEmp_salary))));
System.out.println("maximum salary of an employee from each department: "+departmentWiseMaxSalary);
``` 

output

```
maximum salary of an employee from each department: {Product Development=Optional[Employee{emp_id=277, emp_name='Anuj Chettiar', emp_age=31, emp_gender='Male', emp_dept='Product Development', emp_doj=2012, emp_salary=35700.0}], Security And Transport=Optional[Employee{emp_id=200, emp_name='Jaden Dough', emp_age=38, emp_gender='Male', emp_dept='Security And Transport', emp_doj=2015, emp_salary=11000.5}], Sales And Marketing=Optional[Employee{emp_id=122, emp_name='Paul Niksui', emp_age=25, emp_gender='Male', emp_dept='Sales And Marketing', emp_doj=2015, emp_salary=13500.0}], Infrastructure=Optional[Employee{emp_id=133, emp_name='Martin Theron', emp_age=29, emp_gender='Male', emp_dept='Infrastructure', emp_doj=2012, emp_salary=18000.0}], HR=Optional[Employee{emp_id=111, emp_name='Jiya Brein', emp_age=32, emp_gender='Female', emp_dept='HR', emp_doj=2011, emp_salary=25000.0}], Account And Finance=Optional[Employee{emp_id=177, emp_name='Manu Sharma', emp_age=35, emp_gender='Male', emp_dept='Account And Finance', emp_doj=2010, emp_salary=27000.0}]}
``` 

**15) Get the employees count working in each department**

**Approach: ** We can use **Collectors.groupingBy** and **Collectors.counting** to group employees based on department and count.


```
Map<String, Long> noOfEmployeesInEachDepartment = employeeList.stream().collect(Collectors.groupingBy(Employee::getEmp_dept,Collectors.counting()));
System.out.println("Employees in each department: "+ noOfEmployeesInEachDepartment);
``` 

output

```
Employees in each department: {Product Development=5, Security And Transport=2, Sales And Marketing=3, Infrastructure=3, HR=2, Account And Finance=2}
``` 

That's all about this article :)

 [Answers for input - 1 questions](https://shivaprasadgurram.hashnode.dev/most-frequently-asked-java-streams-coding-answers-part-1-numbers) 

You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/) 

Thanks for reading :) Happy Coding :)