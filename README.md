# student-record-management
import csv
import os
def create():
    #data structure
    #[[rollno,name,mark1,mark2,mark3,mark4,mark5]]
    f=open("student_marks.csv","a",newline='')
    writer=csv.writer(f)
    Student_name=input("Enter name of the student")
    Student_roll=input("enter roll.no") 
    #Lets say there are 5 subjects
    All_Marks=[]
    Subjects=['Physics','Maths','Chemistry','English','Comp.Science']
    for i in range(len(Subjects)):
        mark=input(f"Enter mark of subject {Subjects[i]}")
        All_Marks.append(mark)
    writer.writerow([Student_roll, Student_name] + All_Marks)
    f.close()
    print('Data added')
def read():
    f=open('student_marks.csv','r',newline='')
    reader=csv.reader(f)
    empty = True
    for data in reader:
        print(data)
        empty = False
    if empty:
        print('empty file')
    f.close()
def update(roll_no,subject,new_mark):
    f=open('student_marks.csv','r',newline='')
    reader=csv.reader(f)
    data=[]     
    for i in reader:
        if i[0]==roll_no:
            i[subject]=new_mark
        data.append(i)
    f.close()
    f1=open('student_marks.csv','w',newline='')
    writer=csv.writer(f1)
    writer.writerows(data)
    f1.close()
    print('updated')
def delete_record(roll_no):
    f=open('student_marks.csv','r',newline='')
    reader=csv.reader(f)
    data=[]
    for i in reader:
        if i[0]!=roll_no:
            data.append(i)
    f.close()
    f=open('student_marks.csv','w',newline='')
    writer=csv.writer(f)
    writer.writerows(data)
    f.close()
    print('deleted')
def delete_allrecords():
    f=open('student_marks.csv','w')
    f.close()
def delete_file():
    if os.path.exists("student_marks.csv"):
        os.remove("student_marks.csv")
        print("File deleted")
    else:
        print("File does not exist")

def menu():
    print("1. Create/Add")
    print("2. Read")
    print("3. Update data")
    print("4. Delete a record")
    print("5. delete all records")
    print("6. Delete record")
    c=int(input("enter choice"))
    if c==1:
        create()
    elif c==2:
        read()
    elif c==3:
        roll_no=input("enter roll no")
        print('1.Physics')
        print('2.Maths')
        print('3.Chemistry')
        print('4.English')
        print('5. Computer science')
        subject=int(input("enter subject code"))+1
        new_mark=input("enter new marks")
        update(roll_no,subject,new_mark)
    elif c==4:
        roll_no=input('enter rollno')
        delete_record(roll_no)
    elif c==5:
        delete_allrecords()
    elif c==6:
        delete_file()
    else:
        print('enter valid choice')

while True:
    menu()
    choice=input("do you want to continue, yes/no")
    if choice.lower()=='no':
        print('terminated')
        break
    else:
        continue
