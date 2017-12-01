# Software-Engineering
# Assignment
* First have the students work individually for some time to develop their own diagram (~20 min).  Then, have them work in a group and compare and improve their diagrams  (~20min).  At end show mine as a possible solution.

# Project Description
* In a course the instructor has a class of students. The instructor gives exams, including a final exam, with multiple, sometimes 4, questions. The students take the final, grudgingly. The questions are first checked by the teaching assistant, then returned to the instructor who assigns points. The final is then given back to the teaching assistant who totals the scores and enters them into the gradebook. The finals are given back to the instructor, who returns them to the student. A summary of scores is provided to a course coordinator.

# Hints
* First identify the classes, then add the methods and associations between them.
* Limit yourself to what is described in the system.

# Afterwards
* Project descriptions are always ambiguous.
* There is no real perfect design (there are flaws with mine), many possible designs are possible.  Can spend endless amounts of time trying to find it, but may never.  Point is try and come up with a good-enough design.
* There are plenty of problems with this.  For example, how do these interact.  Sequence Diagrams capture this information.
* Many of the dependencies are left out to avoid a cluttered diagram.

<--
[instructor| | + give_exam(); - assign_points(inout exams : exam［*］); - return_exams(exams : exam［*］); - create_summary(id : number) : string; - notify_coordinator(summary : string);]
[class| + grades : gradebook| + give_exam(an_exam : exam) : exam［*］; + return_exams(exams : exam［*］); + notify_coordinator(summary : string);]
[students| + name : string; - exams : exam［*］;  | + take_exam(inout an_exam : exam); + receive_exam(an_exam : exam); ]
[exam| + id : number; + total_points : number; + student_name : string;|+ clone() : exam;]
[question| + description : string; + answer : string; + total_points : number ｛ read-only ｝; + comments : string; + points : number;|]
[teaching_assistant||+ check_exams(inout exams : exam［*］); + total_exams(inout exams : exam［*］); + record_exams(exams : exam［*］);]
[course_coordinator| | + receive_summary(summary : string)]
[instructor]<>->[class]
[instructor]-.->[exam]
[instructor]<>->[teaching_assistant]
[teaching_assistant]<>->[class]
[class]<>->*[students]
[class]<>->[course_coordinator]
[exam]++->*[question]
->>
