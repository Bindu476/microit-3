# microit-3
student management system
class Student:
    def __init__(self, student_id, name):
        self.student_id = student_id
        self.name = name
        self.attendance = []
        self.grades = {}

    def mark_attendance(self, present=True):
        self.attendance.append(present)

    def add_grade(self, subject, grade):
        self.grades[subject] = grade

    def get_average_grade(self):
        if not self.grades:
            return 0
        return sum(self.grades.values()) / len(self.grades)

    def __str__(self):
        return f"ID: {self.student_id}, Name: {self.name}"


class StudentManagementSystem:
    def __init__(self):
        self.students = {}

    def enroll_student(self, student_id, name):
        if student_id in self.students:
            print("Student ID already exists.")
            return
        self.students[student_id] = Student(student_id, name)
        print(f"Student {name} enrolled successfully.")

    def mark_attendance(self, student_id, present=True):
        student = self.students.get(student_id)
        if student:
            student.mark_attendance(present)
            print(f"Attendance marked for {student.name}.")
        else:
            print("Student not found.")

    def add_grade(self, student_id, subject, grade):
        student = self.students.get(student_id)
        if student:
            student.add_grade(subject, grade)
            print(f"Grade added for {student.name}.")
        else:
            print("Student not found.")

    def view_student_info(self, student_id):
        student = self.students.get(student_id)
        if student:
            print(student)
            print("Attendance Record:", student.attendance)
            print("Grades:", student.grades)
            print("Average Grade:", student.get_average_grade())
        else:
            print("Student not found.")


# Sample usage
sms = StudentManagementSystem()
sms.enroll_student(1, "Alice")
sms.enroll_student(2, "Bob")

sms.mark_attendance(1)
sms.mark_attendance(2, False)

sms.add_grade(1, "Math", 90)
sms.add_grade(1, "Science", 85)
sms.add_grade(2, "Math", 78)

sms.view_student_info(1)
sms.view_student_info(2)
