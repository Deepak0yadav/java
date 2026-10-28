Program 1
1A) Original: StudentCollection.java
java
import java.util.*;

public class StudentCollection {
    public static void main(String[] args) {

        // 1. LIST - Store Student Objects
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student(103, "Rahul", 82.5));
        students.add(new Student(101, "Ananya", 91.0));
        students.add(new Student(104, "Kiran", 75.5));
        students.add(new Student(102, "Bhavya", 88.0));

        System.out.println("===== STUDENT RECORDS =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // 2. COMPARABLE - Sort by Roll Number
        Collections.sort(students);
        System.out.println("\n===== SORTED BY ROLL NUMBER =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // 3. COMPARATOR - Sort by Name
        Collections.sort(students, new NameComparator());
        System.out.println("\n===== SORTED BY NAME =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // 4. ITERATOR
        System.out.println("\n===== ITERATOR =====");
        Iterator<Student> itr = students.iterator();
        while (itr.hasNext()) {
            Student s = itr.next();
            System.out.println(s);
        }

        // 5. MAP - Roll Number as Key
        Map<Integer, Student> studentMap = new HashMap<>();
        for (Student s : students) {
            studentMap.put(s.rollNo, s);
        }

        System.out.println("\n===== STUDENT MAP =====");
        for (Map.Entry<Integer, Student> entry : studentMap.entrySet()) {
            System.out.println("Roll No: " + entry.getKey() + " -> " + entry.getValue());
        }

        // 6. SEARCH USING MAP
        int searchRoll = 102;
        System.out.println("\n===== SEARCH STUDENT =====");
        if (studentMap.containsKey(searchRoll)) {
            System.out.println("Student found: " + studentMap.get(searchRoll));
        } else {
            System.out.println("Student not found!");
        }

        // 7. RANDOMACCESS
        System.out.println("\n===== RANDOMACCESS =====");
        if (students instanceof RandomAccess) {
            System.out.println("ArrayList supports RandomAccess.");
            System.out.println("Student at index 0: " + students.get(0));
            System.out.println("Student at index 2: " + students.get(2));
        } else {
            System.out.println("ArrayList does not support RandomAccess.");
        }
    }
}

// Student class
class Student implements Comparable<Student> {
    int rollNo;
    String name;
    double marks;

    Student(int rollNo, String name, double marks) {
        this.rollNo = rollNo;
        this.name = name;
        this.marks = marks;
    }

    public String toString() {
        return "Roll No: " + rollNo + ", Name: " + name + ", Marks: " + marks;
    }

    // Comparable - Sort by Roll Number
    public int compareTo(Student s) {
        return this.rollNo - s.rollNo;
    }
}

// Comparator - Sort by Name
class NameComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return s1.name.compareToIgnoreCase(s2.name);
    }
}
1B) With Modification: StudentCollection.java
java
import java.util.*;

public class StudentCollection {
    public static void main(String[] args) {

        // 1. LIST - Store Student Objects
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student(103, "Rahul", 82.5));
        students.add(new Student(101, "Ananya", 91.0));
        students.add(new Student(104, "Kiran", 75.5));
        students.add(new Student(102, "Bhavya", 88.0));

        System.out.println("===== STUDENT RECORDS =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // 2. COMPARABLE - Sort by Roll Number
        Collections.sort(students);
        System.out.println("\n===== SORTED BY ROLL NUMBER =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // 3. COMPARATOR - Sort by Name
        Collections.sort(students, new NameComparator());
        System.out.println("\n===== SORTED BY NAME =====");
        for (Student s : students) {
            System.out.println(s);
        }

        // NEW: Sort by Marks (Descending)
        Collections.sort(students, new MarksComparator());
        System.out.println("\n===== SORTED BY MARKS (DESCENDING) =====");
        System.out.println("Roll No\tName\tMarks");
        for (Student s : students) {
            System.out.println(s.rollNo + "\t" + s.name + "\t" + s.marks);
        }

        // 4. ITERATOR
        System.out.println("\n===== ITERATOR =====");
        Iterator<Student> itr = students.iterator();
        while (itr.hasNext()) {
            Student s = itr.next();
            System.out.println(s);
        }

        // 5. MAP - Roll Number as Key
        Map<Integer, Student> studentMap = new HashMap<>();
        for (Student s : students) {
            studentMap.put(s.rollNo, s);
        }

        System.out.println("\n===== STUDENT MAP =====");
        for (Map.Entry<Integer, Student> entry : studentMap.entrySet()) {
            System.out.println("Roll No: " + entry.getKey() + " -> " + entry.getValue());
        }

        // 6. SEARCH USING MAP
        int searchRoll = 102;
        System.out.println("\n===== SEARCH STUDENT =====");
        if (studentMap.containsKey(searchRoll)) {
            System.out.println("Student found: " + studentMap.get(searchRoll));
        } else {
            System.out.println("Student not found!");
        }

        // 7. RANDOMACCESS
        System.out.println("\n===== RANDOMACCESS =====");
        if (students instanceof RandomAccess) {
            System.out.println("ArrayList supports RandomAccess.");
            System.out.println("Student at index 0: " + students.get(0));
            System.out.println("Student at index 2: " + students.get(2));
        } else {
            System.out.println("ArrayList does not support RandomAccess.");
        }
    }
}

// Student class
class Student implements Comparable<Student> {
    int rollNo;
    String name;
    double marks;

    Student(int rollNo, String name, double marks) {
        this.rollNo = rollNo;
        this.name = name;
        this.marks = marks;
    }

    public String toString() {
        return "Roll No: " + rollNo + ", Name: " + name + ", Marks: " + marks;
    }

    // Comparable - Sort by Roll Number
    public int compareTo(Student s) {
        return this.rollNo - s.rollNo;
    }
}

// Comparator - Sort by Name
class NameComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return s1.name.compareToIgnoreCase(s2.name);
    }
}

// NEW: Comparator - Sort by Marks (Descending)
class MarksComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return Double.compare(s2.marks, s1.marks);
    }
}
Program 2
2A) Original: EmployeeList.java
java
import java.util.ArrayList;
import java.util.Scanner;

public class EmployeeList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Employee> empList = new ArrayList<>();

        System.out.print("Enter the number of employees: ");
        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            System.out.println("\nEnter details for Employee " + (i + 1));
            System.out.print("Enter ID: ");
            int id = sc.nextInt();
            sc.nextLine();
            System.out.print("Enter Name: ");
            String name = sc.nextLine();
            System.out.print("Enter Salary: ");
            double salary = sc.nextDouble();

            empList.add(new Employee(id, name, salary));
        }

        System.out.println("\n----- Employee Details -----");
        for (Employee e : empList) {
            System.out.println(e);
        }

        sc.close();
    }
}

class Employee {
    int id;
    String name;
    double salary;

    // Constructor
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Salary: " + salary;
    }
}
2B) With Modification: EmployeeList.java
java
import java.util.ArrayList;
import java.util.Scanner;

public class EmployeeList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ArrayList<Employee> empList = new ArrayList<>();

        System.out.print("Enter the number of employees: ");
        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            System.out.println("\nEnter details for Employee " + (i + 1));
            System.out.print("Enter ID: ");
            int id = sc.nextInt();
            sc.nextLine();
            System.out.print("Enter Name: ");
            String name = sc.nextLine();
            System.out.print("Enter Salary: ");
            double salary = sc.nextDouble();

            empList.add(new Employee(id, name, salary));
        }

        System.out.println("\n----- Employee Details -----");
        for (Employee e : empList) {
            System.out.println(e);
        }

        // NEW: Search employee by ID
        System.out.print("\nEnter Employee ID to search: ");
        int searchId = sc.nextInt();
        boolean found = false;

        for (Employee e : empList) {
            if (e.id == searchId) {
                System.out.println("Employee found!");
                System.out.println(e);
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Employee not found");
        }

        sc.close();
    }
}

class Employee {
    int id;
    String name;
    double salary;

    // Constructor
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Salary: " + salary;
    }
}
Program 3
3A) Original: StrCharExtract.java
java
import java.util.Scanner;

public class StrCharExtract {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking String inputs
        System.out.print("Enter first string: ");
        String s1 = sc.nextLine();
        System.out.print("Enter second string: ");
        String s2 = sc.nextLine();
        System.out.print("Enter third string: ");
        String s3 = sc.nextLine();

        // CHARACTER EXTRACTION - charAt()
        System.out.println("\n--- Character Extraction Result ---");
        int index;
        while (true) {
            System.out.print("Enter index to find character in s1: ");
            if (sc.hasNextInt()) {
                index = sc.nextInt();
                if (index >= 0 && index < s1.length()) {
                    System.out.println("Character at position " + index
                            + " in s1 is " + s1.charAt(index));
                    break;
                } else {
                    System.out.println("Invalid index! Enter an index between 0 and "
                            + (s1.length() - 1));
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // STRING MODIFICATION - substring()
        System.out.println("\n--- String Modification ---");
        int start, end;
        while (true) {
            System.out.print("Enter starting position for substring in s3: ");
            if (sc.hasNextInt()) {
                start = sc.nextInt();
                System.out.print("Enter ending position for substring in s3: ");
                if (sc.hasNextInt()) {
                    end = sc.nextInt();
                    if (start >= 0 && end <= s3.length() && start < end) {
                        System.out.println("Substring of s3 = "
                                + s3.substring(start, end));
                        break;
                    } else {
                        System.out.println("Invalid range!");
                    }
                } else {
                    System.out.println("Invalid input! Please enter a number.");
                    sc.next();
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // concat()
        System.out.println("\nConcatenate Strings s1 and s3:");
        System.out.println(s1.concat(s3));

        // replace()
        sc.nextLine();
        System.out.print("\nEnter character to replace in s3: ");
        char oldChar = sc.next().charAt(0);
        System.out.print("Enter new character: ");
        char newChar = sc.next().charAt(0);
        System.out.println("After replacement: " + s3.replace(oldChar, newChar));

        // getChars()
        int getStart, getEnd;
        while (true) {
            System.out.print("\nEnter starting position for getChars() in s3: ");
            if (sc.hasNextInt()) {
                getStart = sc.nextInt();
                System.out.print("Enter ending position for getChars() in s3: ");
                if (sc.hasNextInt()) {
                    getEnd = sc.nextInt();
                    if (getStart >= 0 && getEnd <= s3.length() && getStart < getEnd) {
                        int length = getEnd - getStart;
                        char ch[] = new char[length];
                        s3.getChars(getStart, getEnd, ch, 0);
                        System.out.println("Extracted characters are:");
                        System.out.println(ch);
                        break;
                    } else {
                        System.out.println("Invalid range!");
                    }
                } else {
                    System.out.println("Invalid input! Please enter a number.");
                    sc.next();
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // toCharArray()
        char ch[] = s1.toCharArray();
        System.out.println("\nCharacter array of s1 is:");
        for (char c : ch) {
            System.out.println(c);
        }

        // STRING COMPARISON - compareTo()
        System.out.println("\n--- String Comparison ---");
        System.out.println("s1 and s2 = " + s1.compareTo(s2));
        System.out.println("s2 and s3 = " + s2.compareTo(s3));
        System.out.println("s3 and s2 = " + s3.compareTo(s2));

        // STRING SEARCH - indexOf(), lastIndexOf()
        sc.nextLine();
        System.out.print("\nEnter a character to search in s3: ");
        char searchChar = sc.next().charAt(0);
        System.out.println("First index of " + searchChar + " in s3 is " + s3.indexOf(searchChar));
        System.out.println("Last index of " + searchChar + " in s3 is " + s3.lastIndexOf(searchChar));

        sc.close();
    }
}
3B) With Modification: StrCharExtract.java

Original jaisa hi hai, bas end mein // NEW wala block add hai.

java
import java.util.Scanner;

public class StrCharExtract {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking String inputs
        System.out.print("Enter first string: ");
        String s1 = sc.nextLine();
        System.out.print("Enter second string: ");
        String s2 = sc.nextLine();
        System.out.print("Enter third string: ");
        String s3 = sc.nextLine();

        // CHARACTER EXTRACTION - charAt()
        System.out.println("\n--- Character Extraction Result ---");
        int index;
        while (true) {
            System.out.print("Enter index to find character in s1: ");
            if (sc.hasNextInt()) {
                index = sc.nextInt();
                if (index >= 0 && index < s1.length()) {
                    System.out.println("Character at position " + index
                            + " in s1 is " + s1.charAt(index));
                    break;
                } else {
                    System.out.println("Invalid index! Enter an index between 0 and "
                            + (s1.length() - 1));
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // STRING MODIFICATION - substring()
        System.out.println("\n--- String Modification ---");
        int start, end;
        while (true) {
            System.out.print("Enter starting position for substring in s3: ");
            if (sc.hasNextInt()) {
                start = sc.nextInt();
                System.out.print("Enter ending position for substring in s3: ");
                if (sc.hasNextInt()) {
                    end = sc.nextInt();
                    if (start >= 0 && end <= s3.length() && start < end) {
                        System.out.println("Substring of s3 = "
                                + s3.substring(start, end));
                        break;
                    } else {
                        System.out.println("Invalid range!");
                    }
                } else {
                    System.out.println("Invalid input! Please enter a number.");
                    sc.next();
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // concat()
        System.out.println("\nConcatenate Strings s1 and s3:");
        System.out.println(s1.concat(s3));

        // replace()
        sc.nextLine();
        System.out.print("\nEnter character to replace in s3: ");
        char oldChar = sc.next().charAt(0);
        System.out.print("Enter new character: ");
        char newChar = sc.next().charAt(0);
        System.out.println("After replacement: " + s3.replace(oldChar, newChar));

        // getChars()
        int getStart, getEnd;
        while (true) {
            System.out.print("\nEnter starting position for getChars() in s3: ");
            if (sc.hasNextInt()) {
                getStart = sc.nextInt();
                System.out.print("Enter ending position for getChars() in s3: ");
                if (sc.hasNextInt()) {
                    getEnd = sc.nextInt();
                    if (getStart >= 0 && getEnd <= s3.length() && getStart < getEnd) {
                        int length = getEnd - getStart;
                        char ch[] = new char[length];
                        s3.getChars(getStart, getEnd, ch, 0);
                        System.out.println("Extracted characters are:");
                        System.out.println(ch);
                        break;
                    } else {
                        System.out.println("Invalid range!");
                    }
                } else {
                    System.out.println("Invalid input! Please enter a number.");
                    sc.next();
                }
            } else {
                System.out.println("Invalid input! Please enter a number.");
                sc.next();
            }
        }

        // toCharArray()
        char ch[] = s1.toCharArray();
        System.out.println("\nCharacter array of s1 is:");
        for (char c : ch) {
            System.out.println(c);
        }

        // STRING COMPARISON - compareTo()
        System.out.println("\n--- String Comparison ---");
        System.out.println("s1 and s2 = " + s1.compareTo(s2));
        System.out.println("s2 and s3 = " + s2.compareTo(s3));
        System.out.println("s3 and s2 = " + s3.compareTo(s2));

        // STRING SEARCH - indexOf(), lastIndexOf()
        sc.nextLine();
        System.out.print("\nEnter a character to search in s3: ");
        char searchChar = sc.next().charAt(0);
        System.out.println("First index of " + searchChar + " in s3 is " + s3.indexOf(searchChar));
        System.out.println("Last index of " + searchChar + " in s3 is " + s3.lastIndexOf(searchChar));

        // NEW: Sentence modification
        sc.nextLine();   // leftover newline consume
        System.out.print("\nEnter a sentence: ");
        String sentence = sc.nextLine();
        System.out.print("Enter the word to replace: ");
        String oldWord = sc.nextLine();
        System.out.print("Enter the new word: ");
        String newWord = sc.nextLine();

        String trimmed = sentence.trim();                      // leading/trailing spaces remove
        System.out.println("After trim()    : [" + trimmed + "]");
        String replaced = trimmed.replace(oldWord, newWord);   // word replace
        System.out.println("After replace() : " + replaced);
        System.out.println("Uppercase       : " + replaced.toUpperCase());
        System.out.println("Lowercase       : " + replaced.toLowerCase());

        sc.close();
    }
}
Program 4
4A) Original: lab6.java
java
import java.util.Scanner;

public class lab6 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking initial String input
        System.out.print("Enter a string: ");
        String input = sc.nextLine();
        StringBuffer sb = new StringBuffer(input);

        System.out.println("\n--- Initial StringBuffer Details ---");
        System.out.println("Buffer initially = " + sb);
        System.out.println("Buffer length = " + sb.length());
        System.out.println("Buffer capacity = " + sb.capacity());

        // charAt()
        System.out.print("\nEnter an index to find the character: ");
        int index = sc.nextInt();
        if (index >= 0 && index < sb.length()) {
            System.out.println("Character at index " + index + " = " + sb.charAt(index));
        } else {
            System.out.println("Invalid index!");
        }

        // setCharAt()
        System.out.print("\nEnter an index to change the character: ");
        int charIndex = sc.nextInt();
        if (charIndex >= 0 && charIndex < sb.length()) {
            System.out.print("Enter a new character: ");
            char newChar = sc.next().charAt(0);
            sb.setCharAt(charIndex, newChar);
            System.out.println("Buffer after setCharAt() = " + sb);
        } else {
            System.out.println("Invalid index!");
        }

        // setLength()
        System.out.print("\nEnter the new length of the buffer: ");
        int newLength = sc.nextInt();
        if (newLength >= 0) {
            sb.setLength(newLength);
            System.out.println("Buffer after setLength() = " + sb);
        }

        // append()
        System.out.print("\nEnter an integer value to append: ");
        int number = sc.nextInt();
        StringBuffer sb1 = new StringBuffer();
        String result = sb1.append("Number = ")
                .append(number)
                .append("!")
                .toString();
        System.out.println("Result of append() = " + result);

        // insert()
        sc.nextLine(); // consume newline
        System.out.print("\nEnter a string for insert operation: ");
        String insertString = sc.nextLine();
        StringBuffer sb2 = new StringBuffer(insertString);
        System.out.print("Enter the text to insert: ");
        String textToInsert = sc.nextLine();
        System.out.print("Enter the index at which to insert: ");
        int insertIndex = sc.nextInt();
        if (insertIndex >= 0 && insertIndex <= sb2.length()) {
            sb2.insert(insertIndex, textToInsert);
            System.out.println("Result of insert() = " + sb2);
        } else {
            System.out.println("Invalid index!");
        }

        // reverse()
        System.out.println("\nResult of reverse() = " + sb.reverse());

        // delete()
        System.out.print("\nEnter starting index for delete(): ");
        int start = sc.nextInt();
        System.out.print("Enter ending index for delete(): ");
        int end = sc.nextInt();
        if (start >= 0 && end <= sb2.length() && start < end) {
            sb2.delete(start, end);
            System.out.println("After delete() = " + sb2);
        } else {
            System.out.println("Invalid range!");
        }

        // deleteCharAt()
        System.out.print("\nEnter index for deleteCharAt(): ");
        int deleteIndex = sc.nextInt();
        if (deleteIndex >= 0 && deleteIndex < sb2.length()) {
            sb2.deleteCharAt(deleteIndex);
            System.out.println("After deleteCharAt() = " + sb2);
        } else {
            System.out.println("Invalid index!");
        }

        // replace()
        sc.nextLine(); // consume newline
        System.out.print("\nEnter text to replace the buffer: ");
        String replacement = sc.nextLine();
        sb2.replace(0, sb2.length(), replacement);
        System.out.println("After replace() = " + sb2);

        sc.close();
    }
}
4B) With Modification: lab6.java
java
import java.util.Scanner;

public class lab6 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Taking initial String input
        System.out.print("Enter a string: ");
        String input = sc.nextLine();
        StringBuffer sb = new StringBuffer(input);

        System.out.println("\n--- Initial StringBuffer Details ---");
        System.out.println("Buffer initially = " + sb);
        System.out.println("Buffer length = " + sb.length());
        System.out.println("Buffer capacity = " + sb.capacity());

        // charAt()
        System.out.print("\nEnter an index to find the character: ");
        int index = sc.nextInt();
        if (index >= 0 && index < sb.length()) {
            System.out.println("Character at index " + index + " = " + sb.charAt(index));
        } else {
            System.out.println("Invalid index!");
        }

        // setCharAt()
        System.out.print("\nEnter an index to change the character: ");
        int charIndex = sc.nextInt();
        if (charIndex >= 0 && charIndex < sb.length()) {
            System.out.print("Enter a new character: ");
            char newChar = sc.next().charAt(0);
            sb.setCharAt(charIndex, newChar);
            System.out.println("Buffer after setCharAt() = " + sb);
        } else {
            System.out.println("Invalid index!");
        }

        // setLength()
        System.out.print("\nEnter the new length of the buffer: ");
        int newLength = sc.nextInt();
        if (newLength >= 0) {
            sb.setLength(newLength);
            System.out.println("Buffer after setLength() = " + sb);
        }

        // append()
        System.out.print("\nEnter an integer value to append: ");
        int number = sc.nextInt();
        StringBuffer sb1 = new StringBuffer();
        String result = sb1.append("Number = ")
                .append(number)
                .append("!")
                .toString();
        System.out.println("Result of append() = " + result);

        // insert()
        sc.nextLine(); // consume newline
        System.out.print("\nEnter a string for insert operation: ");
        String insertString = sc.nextLine();
        StringBuffer sb2 = new StringBuffer(insertString);
        System.out.print("Enter the text to insert: ");
        String textToInsert = sc.nextLine();
        System.out.print("Enter the index at which to insert: ");
        int insertIndex = sc.nextInt();
        if (insertIndex >= 0 && insertIndex <= sb2.length()) {
            sb2.insert(insertIndex, textToInsert);
            System.out.println("Result of insert() = " + sb2);
        } else {
            System.out.println("Invalid index!");
        }

        // reverse()
        System.out.println("\nResult of reverse() = " + sb.reverse());

        // delete()
        System.out.print("\nEnter starting index for delete(): ");
        int start = sc.nextInt();
        System.out.print("Enter ending index for delete(): ");
        int end = sc.nextInt();
        if (start >= 0 && end <= sb2.length() && start < end) {
            sb2.delete(start, end);
            System.out.println("After delete() = " + sb2);
        } else {
            System.out.println("Invalid range!");
        }

        // deleteCharAt()
        System.out.print("\nEnter index for deleteCharAt(): ");
        int deleteIndex = sc.nextInt();
        if (deleteIndex >= 0 && deleteIndex < sb2.length()) {
            sb2.deleteCharAt(deleteIndex);
            System.out.println("After deleteCharAt() = " + sb2);
        } else {
            System.out.println("Invalid index!");
        }

        // replace()
        sc.nextLine(); // consume newline
        System.out.print("\nEnter text to replace the buffer: ");
        String replacement = sc.nextLine();
        sb2.replace(0, sb2.length(), replacement);
        System.out.println("After replace() = " + sb2);

        // NEW: delete(), deleteCharAt(), reverse() - output after each operation
        System.out.print("\nEnter a string for modification: ");
        StringBuffer sb3 = new StringBuffer(sc.nextLine());
        System.out.println("Initial buffer        = " + sb3);

        System.out.print("Enter starting index for delete(): ");
        int s3 = sc.nextInt();
        System.out.print("Enter ending index for delete(): ");
        int e3 = sc.nextInt();
        if (s3 >= 0 && e3 <= sb3.length() && s3 < e3) {
            sb3.delete(s3, e3);
            System.out.println("After delete()        = " + sb3);
        } else {
            System.out.println("Invalid range!");
        }

        System.out.print("Enter index for deleteCharAt(): ");
        int d3 = sc.nextInt();
        if (d3 >= 0 && d3 < sb3.length()) {
            sb3.deleteCharAt(d3);
            System.out.println("After deleteCharAt()  = " + sb3);
        } else {
            System.out.println("Invalid index!");
        }

        sb3.reverse();
        System.out.println("After reverse()       = " + sb3);

        sc.close();
    }
}
Program 5 (Swing, online compiler pe nahi chalega)
5A) Original: SwDemo.java
java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class SwDemo {
    JLabel jlab;

    SwDemo() {
        JFrame jfrm = new JFrame("An Event Example");
        jfrm.setLayout(new FlowLayout());
        jfrm.setSize(220, 90);
        jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JButton jbtnAlpha = new JButton("Alpha");
        JButton jbtnBeta = new JButton("Beta");

        // Action for Alpha button
        jbtnAlpha.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent ae) {
                jlab.setText("Alpha was pressed.");
            }
        });

        // Action for Beta button
        jbtnBeta.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent ae) {
                jlab.setText("Beta was pressed.");
            }
        });

        jfrm.add(jbtnAlpha);
        jfrm.add(jbtnBeta);
        jlab = new JLabel("Press a button.");
        jfrm.add(jlab);
        jfrm.setVisible(true);
    }

    public static void main(String args[]) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new SwDemo();
            }
        });
    }
}
5B) With Modification: SwDemo.java
java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class SwDemo {
    JLabel jlab;

    SwDemo() {
        JFrame jfrm = new JFrame("An Event Example");
        jfrm.setLayout(new FlowLayout());
        jfrm.setSize(300, 100);   // NEW: thoda bada window
        jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JButton jbtnAlpha = new JButton("Alpha");
        JButton jbtnBeta = new JButton("Beta");
        JButton jbtnGamma = new JButton("Gamma");   // NEW

        // Action for Alpha button
        jbtnAlpha.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent ae) {
                jlab.setText("Alpha was pressed.");
            }
        });

        // Action for Beta button
        jbtnBeta.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent ae) {
                jlab.setText("Beta was pressed.");
            }
        });

        // NEW: Action for Gamma button
        jbtnGamma.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent ae) {
                jlab.setText("Gamma was pressed.");
            }
        });

        jfrm.add(jbtnAlpha);
        jfrm.add(jbtnBeta);
        jfrm.add(jbtnGamma);   // NEW
        jlab = new JLabel("Press a button.");
        jfrm.add(jlab);
        jfrm.setVisible(true);
    }

    public static void main(String args[]) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new SwDemo();
            }
        });
    }
}
