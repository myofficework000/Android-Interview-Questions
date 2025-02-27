
Name:	Max marks: 80

1.	Write detailed answers of given questions. (Any 5)                                                                  [ 6 Marks X 5 ]
a.	What is null safety in Kotlin and how is it achieved?.
b.	Write a detailed note on extension functions in Kotlin.
c.	Explain lambda functions and higher order functions in detail.
d.	Explain lateinit and lazy initialization. What are the differences between lateinit and lazy initialization?
e.	What is a companion object? Explain what is the use of @JvmStatic annotation.
f.	Explain types of constructors and init blocks in Kotlin.
2.	Write detailed answers of given questions. (Any 5)                                                                  [ 6 Marks X 5 ]
a.	Explain what is activity and activity lifecycle?
b.	Explain any 10 constraints available for constraint layout.
c.	What is intent? What are the differences between implicit and explicit intent?
d.	Explain working of RecyclerView.
e.	Explain how to send and receive object of a class between activities using Serializable and Parcelable.
f.	In which sequence activity life cycle functions will be executed if launch Activity B from Activity A? In which sequence life cycle functions will be executed if we press the back button from Activity B?
3.	Write the programs for given problem definitions. (Any 4)                                                     [ 5 Marks X 4 ]
a.	Write a program to copy a range of nodes from one linked list to another linked list. For example, copy nodes in the range 3 to 7 from first list and insert it at 4th position.

First list - 20, 50, 30, 60, 70, 40, 20, 55, 99, 200
Second list - 87, 45, 67, 123, 90, 31, 20

After copying elements of first list from the range 3 to 7 and inserting it in the second list, expected output would be:
87, 45, 67, 123, 60, 70, 40, 20, 90, 31, 20

b.	Write a program to find pairs of all elements from int array having sum equal to given target sum. Write the optimized solution.
c.	Write a program to perform addition, subtraction, multiplication and division of two fraction numbers. Create appropriate classes, constructors and methods.
d.	Given a list of employees, where each employee is represented by a data class containing their name, a list of projects they are working on, and a map of their project names to the hours worked on each project. Write a function to perform the following tasks:
Filter out employees who are working on less than 2 projects.
Create a set of all unique projects across all employees.
Create a map where the keys are project names and the values are lists of pairs. Each pair contains an employee's name and the hours they have worked on that project.
For each project in the map, sort the list of pairs by the hours worked in descending order.
Return a map where the keys are project names and the values are the names of the top 3 employees who worked the most hours on that project. If there are fewer than 3 employees, include all of them.
code// 
data class Employee(val name: String, val projects: List<String>, val hoursWorked: Map<String, Int>)
fun analyzeEmployeeProjects(employees: List<Employee>): Map<String, List<String>>
e.	University has various courses and there is eligibility criteria for each course admission as below:
To get admission for Bachelor of Engineering (BE), candidate should have scored 80+ marks in physics, 80+ marks in chemistry and 90+ marks in mathematics, overall percentage obtained in HSC exam should be 85+ and should score 150+ Marks out of 200 in Engineering Entrance Exam. To get admission for Bachelor of Computer Applications (BCA), candidate should have scored 70+ marks in mathematics, overall percentage obtained in HSC exam should be 60+ and should score 70+ marks out of 100 in BCA Entrance exam.
Write Kotlin program to simulate admission process to check if candidate is eligible for BE and BCA admission or not. Create Appropriate abstract classes, abstract methods and appropriate children class to simulate the admission process.

