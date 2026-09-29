# ==========================================
#       STUDENT ATTENDANCE TRACKER
# ==========================================

students = []

print("=" * 60)
print("             STUDENT ATTENDANCE TRACKER")
print("=" * 60)

# Number of students
n = int(input("\nEnter number of students: "))

# Taking student details
for i in range(n):
    print(f"\n--- Student {i + 1} ---")

    name = input("Enter student name: ")
    roll_no = input("Enter roll number: ")

    total_classes = int(input("Enter total number of classes: "))
    attended_classes = int(input("Enter attended classes: "))

    # Validate input
    if total_classes <= 0:
        print("Total classes must be greater than 0.")
        continue

    if attended_classes < 0:
        attended_classes = 0

    if attended_classes > total_classes:
        print("Attended classes cannot be greater than total classes.")
        attended_classes = total_classes

    # Calculate attendance percentage
    attendance_percentage = (attended_classes / total_classes) * 100

    # Check defaulter status
    if attendance_percentage < 70:
        status = "DEFAULTER"
    else:
        status = "ELIGIBLE"

    # Store student information
    student = {
        "name": name,
        "roll_no": roll_no,
        "total": total_classes,
        "attended": attended_classes,
        "percentage": attendance_percentage,
        "status": status
    }

    students.append(student)


# ==========================================
#              ATTENDANCE REPORT
# ==========================================

print("\n")
print("=" * 90)
print("                       ATTENDANCE REPORT")
print("=" * 90)

print(
    f"{'Roll No.':<12}"
    f"{'Name':<20}"
    f"{'Total':<10}"
    f"{'Present':<10}"
    f"{'Attendance':<15}"
    f"{'Status':<15}"
)

print("-" * 90)

for student in students:
    print(
        f"{student['roll_no']:<12}"
        f"{student['name']:<20}"
        f"{student['total']:<10}"
        f"{student['attended']:<10}"
        f"{student['percentage']:<15.2f}"
        f"{student['status']:<15}"
    )


# ==========================================
#              DEFAULTER LIST
# ==========================================

print("\n")
print("=" * 60)
print("                    DEFAULTER LIST")
print("=" * 60)

defaulters = [
    student for student in students
    if student["percentage"] < 70
]

if len(defaulters) == 0:
    print("No defaulters found.")
else:
    print(f"{'Roll No.':<15}{'Name':<25}{'Attendance':<15}")
    print("-" * 55)

    for student in defaulters:
        print(
            f"{student['roll_no']:<15}"
            f"{student['name']:<25}"
            f"{student['percentage']:.2f}%"
        )


# ==========================================
#                  SUMMARY
# ==========================================

total_students = len(students)
total_defaulters = len(defaulters)
eligible_students = total_students - total_defaulters

print("\n")
print("=" * 60)
print("                       SUMMARY")
print("=" * 60)

print(f"Total Students     : {total_students}")
print(f"Eligible Students  : {eligible_students}")
print(f"Defaulter Students : {total_defaulters}")

print("\nAttendance checking completed successfully!")
