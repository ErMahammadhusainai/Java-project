# Java-project
Sem-1 project
import java.util.Scanner;

class StudentProject {
int studentId; String name; int age; String department; String email; String phoneNumber; String address; int[] marks; int markCount;

StudentProject(int studentId, String name, int age, String department, String email, String phoneNumber, String address) {
    this.studentId = studentId;
    this.name = name;
    this.age = age;
    this.department = department;
    this.email = email;
    this.phoneNumber = phoneNumber;
    this.address = address;
    this.marks = new int[10]; // Maximum 10 marks per student
    this.markCount = 0;
}

void addMark(int mark) {
    if (markCount < marks.length) {
        marks[markCount++] = mark;
    } else {
        System.out.println("Maximum marks limit reached!");
    }
}

double calculateAverage() {
    if (markCount == 0) return 0;
    int total = 0;
    for (int i = 0; i < markCount; i++) {
        total += marks[i];
    }
    return (double) total / markCount;
}

void displayDetails() {
    System.out.println("ID : " + studentId +"\n"+ "Name: " + name +"\n"+ "Age: " + age);
    System.out.println("Department: " + department + "\n"+"Email: " + email + "\n"+"Phone: " + phoneNumber);
    System.out.println("Address: " + address + "\n"+"Avg Marks: " + calculateAverage());
}
}

class Main { // Main class to run the program static StudentProject[] students = new StudentProject[10]; // Max 10 students static int studentCount = 0; static Scanner sc = new Scanner(System.in);

public static void main(String[] args) {
    while (true) {
        System.out.println("\n1. Add Student "+"\n"+ "2. Add Marks "+"\n"+ "3. View Details"+"\n"+  "4. Exit");
        System.out.print("Choose : ");
        int choice = sc.nextInt();

        switch (choice) {
            case 1 -> addStudent();
            case 2 -> addMarks();
            case 3 -> viewDetails();
            case 4 -> {
                System.out.println("Thank you for reaching out......");
                return;
            }
            default -> System.out.println("Invalid choice!");
        }
    }
}

static void addStudent() {
    if (studentCount >= students.length) {
        System.out.println("Student limit reached!");
        return;
    }

    System.out.print("Enter ID: ");
    int id = sc.nextInt();
    sc.nextLine(); // Consume newline
    System.out.print("Enter Name: ");
    String name = sc.nextLine();
    System.out.print("Enter Age: ");
    int age = sc.nextInt();
    sc.nextLine();
    System.out.print("Enter Department: ");
    String department = sc.nextLine();
    System.out.print("Enter Email: ");
    String email = sc.nextLine();
    System.out.print("Enter Phone Number: ");
    String phoneNumber = sc.nextLine();
    System.out.print("Enter Address: ");
    String address = sc.nextLine();

    students[studentCount++] = new StudentProject(id, name, age, department, email, phoneNumber, address);
    System.out.println("Student Added!");
}

static void addMarks() {
    System.out.print("Enter Student ID: ");
    int id = sc.nextInt();
    StudentProject student = findStudent(id);
    if (student != null) {
        System.out.print("Enter Marks (-1 to stop): ");
        while (true) {
            int mark = sc.nextInt();
            if (mark == -1) break;
            student.addMark(mark);
        }
        System.out.println("Marks Added!");
    } else {
        System.out.println("Student Not Found!");
    }
}

static void viewDetails() {
    System.out.print("Enter Student ID: ");
    int id = sc.nextInt();
    StudentProject student = findStudent(id);
    if (student != null) {
        student.displayDetails();
    } else {
        System.out.println("Student Not Found!");
    }
}

static StudentProject findStudent(int id) {
    for (int i = 0; i < studentCount; i++) {
        if (students[i].studentId == id) {
            return students[i];
        }
    }
    return null;
}
