import random

first_names = ["Alice","Bob","Charlie","Diana","Evan"]
last_names = ["Smith","Jones","Lee","Patel","Khan"]
def random_student():
    name = random.choice(first_names) + " " + random.choice(last_names)
    age = random.randint(15, 22)
    grades = [random.randint(50, 100) for _ in range(random.randint(2, 5))]
    return name, age, grades
import random

# 1. Student class
class Student:
    def __init__(self, name, age, grades=None):
        self.name = name
        self.age = age
        self.grades = grades or []
    def add_grade(self, g):
        self.grades.append(g)
    def average(self):
        return sum(self.grades)/len(self.grades) if self.grades else 0
    def display(self):
        print(f"{self.name:<20} Age: {self.age:<2} Grades: {self.grades} Avg: {self.average():.2f}")

# 2. Course class
class Course:
    def __init__(self, title):
        self.title = title
        self.students = []
    def enroll(self, student: Student):
        if student not in self.students:
            self.students.append(student)
    def display_students(self):
        print(f"\nCourse: {self.title}\n" + "-"*30)
        if not self.students:
            print("No students enrolled.")
        else:
            for s in self.students:
                s.display()
                
# 3. Generate random data
first_names = ["Alice","Bob","Charlie","Diana","Evan"]
last_names  = ["Smith","Jones","Lee","Patel","Khan"]

def random_student():
    n = random.choice(first_names) + " " + random.choice(last_names)
    age = random.randint(15, 22)
    grades = [random.randint(50, 100) for _ in range(random.randint(2, 5))]
    return Student(n, age, grades)

students = [random_student() for _ in range(5)]
course = Course("Physics 101")
for s in students[:3]:
    course.enroll(s)

# 4. Demo output
print("=== All Random Students ===")
for s in students:
    s.display()

course.display_students()

# 5. Interactive console menu
def menu():
    print("\nMenu:")
    print("1. Add Student")
    print("2. Display All Students")
    print("3. Enroll Student in Course")
    print("4. Display Course Roster")
    print("5. Exit")
    return input("Choose: ").strip()

while True:
    choice = menu()
    if choice == "1":
        n = input("Name: ")
        a = int(input("Age: "))
        grades = list(map(int, input("Grades (space-separated): ").split()))
        students.append(Student(n, a, grades))
        print("✅ Student added.")
    elif choice == "2":
        print("\n-- ALL STUDENTS --")
        for s in students:
            s.display()
    elif choice == "3":
        name = input("Enter student name to enroll: ")
        found = next((s for s in students if s.name.lower() == name.lower()), None)
        if found:
            course.enroll(found)
            print("✅ Enrolled.")
        else:
            print("❌ Not found.")
    elif choice == "4":
        course.display_students()
    elif choice == "5":
        print("Bye!")
        break
    else:
        print("Invalid choice, try again.")
