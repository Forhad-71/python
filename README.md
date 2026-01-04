# python

class StudentDatabase:
    def __init__(self):
        self.student_list = []  

    def add_student(self, student):
        self.student_list.append(student)


class Student:
    def __init__(self, student_id, name, department, is_enrolled=False):
       
        self.__student_id = student_id
        self.__name = name
        self.__department = department
        self.__is_enrolled = is_enrolled

    def enroll_student(self):
        if self.__is_enrolled:
            print("Student is already enrolled.")
        else:
            self.__is_enrolled = True
            print("Enrollment successful.")

    def drop_student(self):
        if not self.__is_enrolled:
            print("Student is not enrolled, so cannot be dropped.")
        else:
            self.__is_enrolled = False
            print("Drop successful.")

    def view_student_info(self):
        status = "Enrolled" if self.__is_enrolled else "Not Enrolled"
        print("\n--- Student Info ---")
        print("ID:", self.__student_id)
        print("Name:", self.__name)
        print("Department:", self.__department)
        print("Status:", status)
        print("--------------------\n")

    def get_student_id(self):
        return self.__student_id

    def __str__(self):
        status = "Enrolled" if self.__is_enrolled else "Not Enrolled"
        return f"{self.__student_id} | {self.__name} | {self.__department} | {status}"


def find_student(db, student_id):
    for s in db.student_list:
        if s.get_student_id() == student_id:
            return s
    return None



db = StudentDatabase()
db.add_student(Student("101", "Arafat", "CSE", True))
db.add_student(Student("102", "Christian", "BBA", False))
db.add_student(Student("103", "Gab", "EEE", True))
db.add_student(Student("104", "Moi", "CSE", False))



while True:
    print("Menu Options:")
    print("1. View All Students")
    print("2. Enroll Student")
    print("3. Drop Student")
    print("4. Exit")

    choice = input("Enter your choice (1-4): ")

    if choice == "1":
        print("\n--- All Students ---")
        for s in db.student_list:
            print(s)
        print("--------------------\n")

    elif choice == "2":
        sid = input("Enter student ID to enroll: ")
        student = find_student(db, sid)
        if student is None:
            print("Invalid student ID.")
        else:
            student.enroll_student()
            student.view_student_info()

    elif choice == "3":
        sid = input("Enter student ID to drop: ")
        student = find_student(db, sid)
        if student is None:
            print("Invalid student ID.")
        else:
            student.drop_student()
            student.view_student_info()

    elif choice == "4":
        print("Exiting... Goodbye!")
        break

    else:
        print("Invalid choice. Please enter 1, 2, 3, or 4.")
